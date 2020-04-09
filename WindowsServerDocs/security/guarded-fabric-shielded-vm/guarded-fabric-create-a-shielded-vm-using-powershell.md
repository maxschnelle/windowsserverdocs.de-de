---
title: Erstellen einer abgeschirmten VM mithilfe von PowerShell
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: 09e09fa30a38ef5f6046f623e24be0bc7b6ce87e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856753"
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

Wenn Sie sich in einer Unternehmensumgebung befinden und mit dem HGS-Server kommunizieren können, finden Sie die Überwachungs Metadaten unter *http://\<hgsclustername\>/KeyProtection/Service/Metadata/2014-07/Metadata.XML*

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

Wenn die Antwortdatei für die Schutz Daten Spezialisierungs Werte enthält, können Sie die Ersatzwerte für New-shieldedvm bereitstellen. In diesem Beispiel wird die Antwortdatei mit Platzhalterwerten für eine statische IPv4-Adresse konfiguriert.

```powershell
$specializationValues = @{
    "@IP4Addr-1@" = "192.168.1.10/24"
    "@MacAddr-1@" = "Ethernet"
    "@Prefix-1-1@" = "24"
    "@NextHop-1-1@" = "192.168.1.254"
}
New-ShieldedVM -Name 'MyStaticIPVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -SpecializationValues $specializationValues -Wait

```

Wenn Ihr Vorlagen Datenträger ein Linux-basiertes Betriebssystem enthält, schließen Sie beim Ausführen des Befehls das `-Linux`-Flag ein:

```powershell
New-ShieldedVM -Name 'MyLinuxVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait -Linux
```

Überprüfen Sie den Hilfe Inhalt mithilfe `Get-Help New-ShieldedVM -Full`, um mehr über andere Optionen zu erfahren, die Sie an das Cmdlet übergeben können.

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