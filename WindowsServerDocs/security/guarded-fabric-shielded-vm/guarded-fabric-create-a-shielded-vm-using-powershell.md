---
title: Erstellen einer abgeschirmten VM mithilfe von PowerShell
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 888177c1288216c28f7d4c0a667fd81e93bdce8c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402399"
---
# <a name="create-a-shielded-vm-using-powershell"></a>Erstellen einer abgeschirmten VM mithilfe von PowerShell

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In der Produktionsumgebung verwenden Sie in der Regel einen Fabric-Manager (z. b. VMM), um abgeschirmte VMS bereitzustellen. Die unten dargestellten Schritte ermöglichen Ihnen jedoch, das gesamte Szenario ohne Fabric-Manager bereitzustellen und zu überprüfen.

Kurz gesagt, erstellen Sie einen Vorlagen Datenträger, eine geschützte Datendatei, eine Antwortdatei für die unbeaufsichtigte Installation und andere Sicherheits Artefakte auf einem beliebigen Computer. Kopieren Sie diese Dateien dann auf einen überwachten Host, und stellen Sie die abgeschirmte VM bereit.

## <a name="create-a-signed-template-disk"></a>Erstellen einer signierten Vorlagen Festplatte

Zum Erstellen einer neuen abgeschirmten VM benötigen Sie zunächst einen abgeschirmten VM-Vorlagen Datenträger, der mit dem zugehörigen Betriebssystem Volume (bzw. Start-und Stamm Partitionen unter Linux) vorverschlüsselt ist.
Befolgen Sie die nachstehenden Links, um weitere Informationen zum Erstellen eines Vorlagen Datenträgers zu finden.

- [Windows-Vorlagen Datenträger vorbereiten](guarded-fabric-create-a-shielded-vm-template.md)
- [Einen Linux-Vorlagen Datenträger](guarded-fabric-create-a-linux-shielded-vm-template.md)

Außerdem benötigen Sie eine Kopie des volumesignaturkatalogs des Datenträgers, um die Schutz Datendatei zu erstellen.
Zum Speichern dieser Datei führen Sie den folgenden Befehl auf dem Computer aus, auf dem Sie den Vorlagen Datenträger erstellt haben:

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath "C:\temp\MyTemplateDisk.vhdx" -VolumeSignatureCatalogPath "C:\temp\MyTemplateDiskCatalog.vsc"
```

## <a name="download-guardian-metadata"></a>Überwachungs Metadaten herunterladen

Für jedes virtualisierungsfabrics, in dem Sie Ihre abgeschirmte VM ausführen möchten, müssen Sie die Überwachungs Metadaten für die HGS-Cluster des Fabrics abrufen.
Ihr Hostinganbieter sollte diese Informationen für Sie bereitstellen können.

Wenn Sie sich in einer Unternehmensumgebung befinden und mit dem HGS-Server kommunizieren können, sind die Überwachungs Metadaten unter *http://\<hgsclustername @ no__t-2/keyprotection/Service/Metadata/2014-07/Metadata. XML verfügbar.*

## <a name="create-shielding-data-pdk-file"></a>Erstellen einer Datei mit geschützten Daten (PDK)

Geschützte Daten werden erstellt und im Besitz von Mandanten-VM-Besitzern. Sie enthalten Geheimnisse, die zum Erstellen von abgeschirmten VMS erforderlich sind, die vor dem Fabric-Administrator geschützt werden müssen, z. b. das Administrator Kennwort
Geschützte Daten werden so verschlüsselt, dass Sie nur von den HGS-Servern und dem Mandanten entschlüsselt werden können.
Nachdem Sie vom Mandanten/VM-Besitzer erstellt wurde, muss die resultierende PDK-Datei in das geschützte Fabric kopiert werden.
Weitere Informationen finden Sie unter [Was sind geschützte Daten und warum ist es erforderlich?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary).

Außerdem benötigen Sie eine Antwortdatei für die unbeaufsichtigte Installation (Unattend. XML für Windows, variiert für Linux). Eine Anleitung zum Einbeziehen der Antwortdatei finden Sie unter [Erstellen einer Antwortdatei](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file) .

Führen Sie die folgenden Cmdlets auf einem Computer aus, auf dem die Remoteserver-Verwaltungstools für abgeschirmte VMS installiert ist.
Wenn Sie ein PDK für eine Linux-VM erstellen, müssen Sie dies auf einem Server ausführen, auf dem Windows Server, Version 1709 oder höher, ausgeführt wird.

 
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
    
## <a name="provision-shielded-vm-on-a-guarded-host"></a>Bereitstellen einer abgeschirmten VM auf einem überwachten Host
Kopieren Sie die Vorlagen Datenträger-Datei (serveros. vhdx) und die PDK-Datei (". PDK") auf den überwachten Host, um die Bereitstellung vorzubereiten.

Installieren Sie auf dem überwachten Host das PowerShell-Modul für geschützte Fabric-Tools, das das Cmdlet New-shieldedvm enthält, um den Bereitstellungs Prozess zu vereinfachen. Wenn der überwachte Host auf das Internet zugreifen kann, führen Sie den folgenden Befehl aus:

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

Sie können das Modul auch auf einen anderen Computer herunterladen, der über Internet Zugriff verfügt, und das resultierende Modul in `C:\Program Files\WindowsPowerShell\Modules` auf dem überwachten Host kopieren.

```powershell
Save-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0 -Path C:\temp\
```

Nachdem das Modul installiert wurde, können Sie den abgeschirmten virtuellen Computer bereitstellen.

```powershell
New-ShieldedVM -Name 'MyShieldedVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait
```

Wenn Ihr Vorlagen Datenträger ein Linux-basiertes Betriebssystem enthält, schließen Sie beim Ausführen des Befehls das Flag "`-Linux`" ein:

```powershell
New-ShieldedVM -Name 'MyLinuxVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait -Linux
```

Überprüfen Sie den Hilfe Inhalt mithilfe von `Get-Help New-ShieldedVM -Full`, um weitere Informationen zu anderen Optionen zu erhalten, die Sie an das Cmdlet übergeben können.

Nachdem die Bereitstellung des virtuellen Computers abgeschlossen ist, wird er in die betriebssystemspezifische Spezialisierungs Phase eingegeben, in der er zur Verwendung bereit ist.
Stellen Sie sicher, dass Sie die VM mit einem gültigen Netzwerk verbinden, damit Sie eine Verbindung mit dem virtuellen Computer herstellen können, sobald er ausgeführt wird (mithilfe von RDP, PowerShell, SSH oder Ihrem bevorzugten Verwaltungs Tool).

## <a name="running-shielded-vms-on-a-hyper-v-cluster"></a>Ausführen von abgeschirmten VMS auf einem Hyper-V-Cluster

Wenn Sie versuchen, abgeschirmte VMS auf geclusterten überwachten Hosts (mithilfe eines Windows-Failoverclusters) bereitzustellen, können Sie den abgeschirmten virtuellen Computer mit dem folgenden Cmdlet so konfigurieren, dass er hoch verfügbar ist:

```powershell
Add-ClusterVirtualMachineRole -VMName 'MyShieldedVM' -Cluster <Hyper-V cluster name>
```

Der abgeschirmte virtuelle Computer kann nun im Cluster Live migriert werden.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Bereitstellen eines abgeschirmten mithilfe von VMM](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)