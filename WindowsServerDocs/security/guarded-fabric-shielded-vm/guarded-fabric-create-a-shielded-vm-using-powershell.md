---
title: Erstellen Sie eine geschützte VM mithilfe von PowerShell
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 76be26e107bd16165367d5432e1dd757dea2f9b4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855411"
---
# <a name="create-a-shielded-vm-using-powershell"></a>Erstellen Sie eine geschützte VM mithilfe von PowerShell

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In der Produktion in der Regel verwenden einen Fabric-Manager (z. B. VMM) Sie zum Bereitstellen von abgeschirmten VMs. Allerdings können die unten dargestellte Schritte zum Bereitstellen und überprüfen das gesamte Szenario ohne Fabric-Manager.

Kurz gesagt, Sie erstellen einen vorlagendatenträger, eine geschützte Datendatei, eine Antwortdatei für die unbeaufsichtigte Installation und andere sicherheitsartefakte auf jedem Computer, und klicken Sie dann kopieren Sie diese Dateien auf einen bewachten Host und die abgeschirmte VM bereitstellen.

## <a name="create-a-signed-template-disk"></a>Erstellen eines signierten vorlagedatenträgers

Um eine neue geschützte VM zu erstellen, benötigen Sie zuerst einen abgeschirmten VM-Vorlage-Datenträger, der bereits verschlüsselt ist, mit dessen Betriebssystem Volume (oder Start- und Stamm Partitionen unter Linux) signiert ist.
Führen Sie den folgenden Links Weitere Informationen zum Erstellen eines vorlagedatenträgers aus.

- [Vorbereiten eines Windows-vorlagedatenträgers](guarded-fabric-create-a-shielded-vm-template.md)
- [Vorbereiten eines Linux-vorlagedatenträgers](guarded-fabric-create-a-linux-shielded-vm-template.md)

Sie benötigen auch eine Kopie des Datenträgers Volume-signaturkatalogs, um die geschützte Datendatei zu erstellen.
Um diese Datei zu speichern, führen Sie den folgenden Befehl auf dem Computer, auf dem Sie den vorlagendatenträger erstellt:

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath "C:\temp\MyTemplateDisk.vhdx" -VolumeSignatureCatalogPath "C:\temp\MyTemplateDiskCatalog.vsc"
```

## <a name="download-guardian-metadata"></a>Überwachungsmetadaten herunterladen

Für jeden der virtualisierungsfabrics, in dem Sie Ihren geschützten virtuellen Computer ausführen möchten, müssen Sie zum Abrufen der überwachungsmetadaten für die Fabrics Host-Überwachungsdienst-Cluster.
Ihr Hostinganbieter sollte in der Lage, diese Informationen für Sie bereitzustellen.

Wenn Sie in einer unternehmensumgebung und mit der HGS-Server kommunizieren können, ist der überwachungsmetadaten unter *http://\<HGSCLUSTERNAME\>/KeyProtection/service/metadata/2014-07/metadata.xml*

## <a name="create-shielding-data-pdk-file"></a>Schutz von Daten (PDK)-Datei erstellen

Geschützte Daten wird erstellt und im Besitz von Mandanten-VM-Besitzer und enthält Geheimnisse erforderlich, um abgeschirmte VMs zu erstellen, die von der fabricadministrator, wie z. B. die abgeschirmte VM-Administratorkennwort geschützt werden müssen.
Geschützte Daten werden verschlüsselt, sodass nur die Host-Überwachungsdienst-Server und die Mandanten entschlüsselt werden können.
Nachdem vom Mandanten/VM-Besitzer erstellt wird, muss die resultierende PDK-Datei zum überwachten Fabric kopiert werden.
Weitere Informationen finden Sie unter [welche Daten Schutz ist und warum dies erforderlich ist?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary).

Darüber hinaus benötigen Sie eine Antwortdatei für die unbeaufsichtigte Installation ("Unattend.xml" für Windows, variiert für Linux). Finden Sie unter [Erstellen einer Antwortdatei](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file) Anleitungen dazu, was Sie in der Antwortdatei einfügen.

Führen Sie die folgenden Cmdlets auf einem Computer mit dem Remoteserver-Verwaltungstools für abgeschirmte VMs installiert.
Wenn Sie eine PDK für eine Linux-VM erstellen, müssen Sie dies auf einem Server mit Windows Server, Version 1709 oder höher.

 
```powershell
# Create owner certificate, don't lose this!
# The certificate is stored at Cert:\LocalMachine\Shielded VM Local Certificates
$Owner = New-HgsGuardian –Name 'Owner' –GenerateCertificates
 
# Import the HGS guardian for each fabric you want to run your shielded VM
$Guardian = Import-HgsGuardian -Path C:\HGSGuardian.xml -Name 'TestFabric'
 
# Create the PDK file
# The "Policy" parameter describes whether the admin can see the VM's console or not
# Use "EncryptionSupported" if you are testing out shielded VMs and want to debug any issues during the specialization process
New-ShieldingDataFile -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Owner $Owner –Guardian $guardian –VolumeIDQualifier (New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\MyTemplateDiskCatalog.vsc' -VersionRule Equals) -WindowsUnattendFile 'C:\unattend.xml' -Policy Shielded
```
    
## <a name="provision-shielded-vm-on-a-guarded-host"></a>Bereitstellen von abgeschirmten virtuellen Computer auf einem bewachten host
Kopieren Sie die Datenträger-Vorlagendatei (ServerOS.vhdx) und die PDK-Datei (contoso.pdk) auf den überwachten Host, für die Bereitstellung vorzubereiten.

Installieren Sie auf dem überwachten Host die überwachten Fabric-Tools PowerShell-Modul, das Cmdlet "New-shieldedvm", um die Bereitstellung zu vereinfachen. Wenn Ihre überwachte Host Zugriff auf das Internet hat, führen Sie den folgenden Befehl aus:

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

Sie können auch das Modul auf einem anderen Computer mit Internet zugreifen, und kopieren Sie das resultierende Modul herunterladen `C:\Program Files\WindowsPowerShell\Modules` auf dem überwachten Host.

```powershell
Save-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0 -Path C:\temp\
```

Nachdem das Modul installiert ist, können Sie sich zum Bereitstellen der abgeschirmten VM.

```powershell
New-ShieldedVM -Name 'MyShieldedVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait
```

Wenn Ihre vorlagendatenträger auf einem Linux-basierten Betriebssystem enthält, schließen Sie die `-Linux` zu kennzeichnen, wenn der Befehl ausgeführt wird:

```powershell
New-ShieldedVM -Name 'MyLinuxVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait -Linux
```

Überprüfen Sie die Hilfe von Inhalten mit `Get-Help New-ShieldedVM -Full` erfahren Sie mehr über weitere Optionen können Sie an das Cmdlet übergeben.

Nach Abschluss der VM-Bereitstellung, wird es die Spezialisierungsphase betriebssystemspezifischen, geben Sie nach der sie verwendet werden.
Achten Sie darauf, dass Sie den virtuellen Computer mit einem gültigen Netzwerk verbinden, damit Sie darauf zugreifen können, sobald es ausgeführt wird (mithilfe von RDP, PowerShell, SSH- oder Ihr bevorzugtes Verwaltungstool).

## <a name="running-shielded-vms-on-a-hyper-v-cluster"></a>Abgeschirmte VMs in einem Hyper-V-Cluster ausgeführt.

Wenn Sie abgeschirmte VMs auf gruppierten überwachten Hosts (mit einem Windows-Failovercluster) bereitstellen möchten, können Sie hohe Verfügbarkeit mit dem folgenden Cmdlet die abgeschirmte VM konfigurieren:

```powershell
Add-ClusterVirtualMachineRole -VMName 'MyShieldedVM' -Cluster <Hyper-V cluster name>
```

Die abgeschirmte VM kann jetzt live werden innerhalb des Clusters migriert.

## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Bereitstellen einer geschützten mithilfe von VMM](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)