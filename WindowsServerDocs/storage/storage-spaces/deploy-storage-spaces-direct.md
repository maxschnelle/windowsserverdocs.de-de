---
title: Bereitstellen von direkte Speicherplätze
ms.prod: windows-server
manager: eldenc
ms.author: stevenek
ms.technology: storage-spaces
ms.topic: get-started-article
ms.assetid: 20fee213-8ba5-4cd3-87a6-e77359e82bc0
author: stevenek
ms.date: 06/07/2019
description: Eine Schritt-für-Schritt-Anleitung zum Bereitstellen von Software definiertem Speicher mit direkte Speicherplätze in Windows Server als hyperkonvergierte Infrastruktur oder konvergierte Infrastruktur (auch als disaggiert bezeichnet).
ms.localizationpriority: medium
ms.openlocfilehash: 0ab96f737f7700e202c9d0382c06859c4ea84118
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402815"
---
# <a name="deploy-storage-spaces-direct"></a>Bereitstellen von direkte Speicherplätze

> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält Schritt-für-Schritt-Anweisungen zum Bereitstellen von [direkte Speicherplätze](storage-spaces-direct-overview.md).

> [!Tip]
> Sie möchten eine hyperkonvergierte Infrastruktur erwerben? Microsoft empfiehlt, eine überprüfte Hardware-/Softwarelösung unserer Partner zu erwerben, die Bereitstellungs Tools und-Verfahren umfasst. Diese Lösungen wurden mit unserer Referenzarchitektur entworfen, zusammengestellt und überprüft, um Kompatibilität und Zuverlässigkeit sicherzustellen, sodass Sie schnell loslegen können. Informationen zu Windows Server 2019-Lösungen finden Sie auf der [Azure Stack HCI Solutions-Website](https://azure.microsoft.com/overview/azure-stack/hci). Informationen zu Windows Server 2016-Lösungen finden Sie unter [Windows Server-Software definiert](https://microsoft.com/wssd).

> [!Tip]
> Sie können virtuelle Hyper-V-Computer (einschließlich in Microsoft Azure) verwenden, um [direkte Speicherplätze ohne Hardware auszuwerten](storage-spaces-direct-in-vm.md). Sie können auch die praktischen [Windows Server-schnell-Lab-Bereitstellungs Skripts](https://aka.ms/wslab)überprüfen, die wir zu Schulungszwecken verwenden.

## <a name="before-you-start"></a>Bevor Sie beginnen

Überprüfen Sie die [direkte Speicherplätze Hardwareanforderungen](Storage-Spaces-Direct-Hardware-Requirements.md) , und lesen Sie dieses Dokument, um sich mit dem allgemeinen Ansatz und wichtigen Notizen vertraut zu machen, die mit einigen Schritten verknüpft sind.

Sammeln Sie die folgenden Informationen:

- **Bereitstellungs Option.** Direkte Speicherplätze unterstützt [zwei Bereitstellungs Optionen: hyperkonvergiert und konvergiert](storage-spaces-direct-overview.md#deployment-options), auch als disaggregierte bezeichnet. Machen Sie sich mit den Vorteilen der einzelnen Maßnahmen vertraut, um zu entscheiden, welches für Sie geeignet ist. Die unten aufgeführten Schritte 1-3 gelten für beide Bereitstellungs Optionen. Schritt 4 ist nur für die konvergierte Bereitstellung erforderlich.

- **Server Namen.** Machen Sie sich mit den Benennungs Richtlinien Ihrer Organisation für Computer, Dateien, Pfade und andere Ressourcen vertraut. Sie müssen mehrere Server bereitstellen, die jeweils über eindeutige Namen verfügen.

- **Domänen Name.** Machen Sie sich mit den Richtlinien Ihrer Organisation für Domänen Namen und Domänen Beitritt vertraut.  Sie werden die Server zu Ihrer Domäne hinzufügen, und Sie müssen den Domänen Namen angeben. 

- **RDMA-Netzwerk.** Es gibt zwei Arten von RDMA-Protokollen: IWarp und ROCE. Beachten Sie, welche der Netzwerkadapter verwendet und ob ROCE auch die Version (v1 oder v2) beachten soll. Beachten Sie für ROCE auch das Modell Ihres Top-of-Rack-Schalters.

- **VLAN-ID.** Beachten Sie die VLAN-ID, die für Verwaltungs Betriebssystem-Netzwerkadapter auf den Servern verwendet werden soll, sofern vorhanden. Diese sollten Sie von Ihrem Netzwerkadministrator erhalten.

## <a name="step-1-deploy-windows-server"></a>Schritt 1: Bereitstellen von Windows Server

### <a name="step-11-install-the-operating-system"></a>Schritt 1,1: Installieren des Betriebssystems

Der erste Schritt besteht darin, Windows Server auf allen Servern zu installieren, die sich im Cluster befinden. Direkte Speicherplätze erfordert Windows Server 2016 Datacenter Edition. Sie können die Server Core-Installationsoption oder Server mit Desktop Darstellung verwenden.

Wenn Sie Windows Server mithilfe des Setup-Assistenten installieren, können Sie zwischen *Windows Server* (bezieht sich auf Server Core) und *Windows Server (Server mit Desktop Darstellung)* wählen. Dies entspricht der Option für die *vollständige* Installation. verfügbar in Windows Server 2012 R2. Wenn Sie nicht auswählen, erhalten Sie die Server Core-Installationsoption. Weitere Informationen finden Sie unter [Installationsoptionen für Windows Server 2016](../../get-started/Windows-Server-2016.md).

### <a name="step-12-connect-to-the-servers"></a>Schritt 1,2: Verbindung mit den Servern herstellen

Dieser Leitfaden konzentriert sich auf die Server Core-Installationsoption und die Remote Bereitstellung/Verwaltung von einem separaten Verwaltungssystem, das Folgendes aufweisen muss:

- Windows Server 2016 mit denselben Updates wie die von ihm verwalteten Server
- Netzwerk Konnektivität zu den verwalteten Servern
- Mitglied der gleichen Domäne oder einer voll vertrauenswürdigen Domäne
- Remoteserver-Verwaltungstools (RSAT) und PowerShell-Module für Hyper-V und Failoverclustering. RSAT-Tools und PowerShell-Module sind unter Windows Server verfügbar und können ohne Installation anderer Features installiert werden. Sie können die [Remoteserver-Verwaltungstools](https://www.microsoft.com/download/details.aspx?id=45520) auch auf einem Windows 10-Verwaltungs-PC installieren.

Installieren Sie auf dem Verwaltungssystem den Failovercluster sowie Hyper-V-Verwaltungstools. Dies kann über Server Manager mithilfe des Assistenten zum **Hinzufügen von Rollen und Features**. Wählen Sie auf der Seite **Features** die Option **Remoteserver-Verwaltungstools** und dann die zu installierenden Tools aus.

Geben Sie die PS-Sitzung ein, und verwenden Sie entweder den Servernamen oder die IP-Adresse des Knotens, mit dem Sie eine Verbindung herstellen möchten. Nachdem Sie diesen Befehl ausgeführt haben, werden Sie zur Eingabe eines Kennworts aufgefordert. Geben Sie das Administrator Kennwort ein, das Sie beim Einrichten von Windows angegeben haben.

   ```PowerShell
   Enter-PSSession -ComputerName <myComputerName> -Credential LocalHost\Administrator
   ```

   Im folgenden finden Sie ein Beispiel dafür, wie Sie das gleiche in Skripts nutzen können, falls Sie dies mehr als einmal tun müssen:

   ```PowerShell
   $myServer1 = "myServer-1"
   $user = "$myServer1\Administrator"

   Enter-PSSession -ComputerName $myServer1 -Credential $user
   ```

> [!TIP]
> Wenn Sie eine Remote Bereitstellung von einem Verwaltungssystem aus durchführt, erhalten Sie möglicherweise eine Fehlermeldung wie *WinRM kann die Anforderung nicht verarbeiten.* Um dieses Problem zu beheben, fügen Sie mithilfe von Windows PowerShell jeden Server der Liste vertrauenswürdiger Hosts auf dem Verwaltungs Computer hinzu:  
>   
> `Set-Item WSMAN:\Localhost\Client\TrustedHosts -Value Server01 -Force`
>  
> Hinweis: die Liste der vertrauenswürdigen Hosts unterstützt Platzhalter, wie z. b. `Server*`.
>
> Geben Sie `Get-Item WSMAN:\Localhost\Client\TrustedHosts` ein, um die Liste der vertrauenswürdigen Hosts anzuzeigen.  
>   
> Geben Sie `Clear-Item WSMAN:\Localhost\Client\TrustedHost` ein, um die Liste zu leeren.  

### <a name="step-13-join-the-domain-and-add-domain-accounts"></a>Schritt 1,3: Beitreten zur Domäne und Hinzufügen von Domänen Konten

Bisher haben Sie die einzelnen Server mit dem lokalen Administrator Konto konfiguriert, `<ComputerName>\Administrator`.

Um direkte Speicherplätze zu verwalten, müssen Sie die Server einer Domäne hinzufügen und ein Active Directory Domain Services Domänen Konto verwenden, das sich in der Gruppe "Administratoren" auf jedem Server befindet.

Öffnen Sie aus dem Verwaltungssystem eine PowerShell-Konsole mit Administrator Rechten. Verwenden Sie `Enter-PSSession`, um eine Verbindung zu den einzelnen Servern herzustellen, und führen Sie das folgende Cmdlet aus. ersetzen Sie dabei ihre eigenen Computernamen, Domänen Namen und Domänen Anmelde Informationen

```PowerShell  
Add-Computer -NewName "Server01" -DomainName "contoso.com" -Credential "CONTOSO\User" -Restart -Force  
```

Wenn Ihr Speicher Administrator Konto kein Mitglied der Gruppe "Domänen-Admins" ist, fügen Sie das Speicher Administrator Konto der lokalen Gruppe "Administratoren" auf jedem Knoten hinzu, oder fügen Sie die Gruppe, die Sie für Speicher Administratoren verwenden, hinzu. Sie können den folgenden Befehl verwenden (oder eine Windows PowerShell-Funktion schreiben, um weitere Informationen zu erhalten. Weitere Informationen finden Sie unter [Verwenden von PowerShell zum Hinzufügen von Domänen Benutzern zu einer lokalen Gruppe](http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/19/use-powershell-to-add-domain-users-to-a-local-group.aspx) ):

```
Net localgroup Administrators <Domain\Account> /add
```

### <a name="step-14-install-roles-and-features"></a>Schritt 1,4: Installieren von Rollen und Features

Der nächste Schritt besteht darin, Server Rollen auf jedem Server zu installieren. Hierfür können Sie das [Windows Admin Center](../../manage/windows-admin-center/use/manage-servers.md), [Server-Manager](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)) oder PowerShell verwenden. Folgende Rollen müssen installiert werden:

- Failoverclustering
- Hyper-V
- Datei Server (wenn Sie Dateifreigaben hosten möchten, z. b. für eine konvergierte Bereitstellung)
- Daten-Center-Bridging (Wenn Sie RoCEv2 anstelle von iWARP Netzwerkadaptern verwenden)
- RSAT-Clustering-PowerShell
- Hyper-V-PowerShell

Verwenden Sie das [install-Windows Feature-](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature) Cmdlet, um die Installation über PowerShell durchführen zu können. Sie können Sie auf einem einzelnen Server wie dem folgenden verwenden:

```PowerShell
Install-WindowsFeature -Name "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"
```

Wenn Sie den Befehl auf allen Servern im Cluster gleichzeitig ausführen möchten, verwenden Sie dieses kleine Skript, indem Sie die Liste der Variablen am Anfang des Skripts so ändern, dass Sie Ihrer Umgebung entspricht.

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"
$FeatureList = "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"

# This part runs the Install-WindowsFeature cmdlet on all servers in $ServerList, passing the list of features into the scriptblock with the "Using" scope modifier so you don't have to hard-code them here.
Invoke-Command ($ServerList) {
    Install-WindowsFeature -Name $Using:Featurelist
}
```

## <a name="step-2-configure-the-network"></a>Schritt 2: Konfigurieren des Netzwerks

Wenn Sie direkte Speicherplätze in virtuellen Computern bereitstellen, überspringen Sie diesen Abschnitt.

Direkte Speicherplätze erfordert Netzwerkverbindungen mit geringer Bandbreite zwischen Servern im Cluster. Mindestens 10 GbE-Netzwerke sind erforderlich, und es wird der Remote Zugriff auf den direkten Speicher (RDMA) empfohlen. Sie können entweder IWarp oder ROCE verwenden, solange es das Windows Server 2016-Logo aufweist, aber IWarp ist in der Regel einfacher einzurichten.

> [!Important]
> Abhängig von ihrer Netzwerkausrüstung und vor allem mit ROCE v2 ist möglicherweise eine Konfiguration des Top-of-Rack-Schalters erforderlich. Die richtige Switchkonfiguration ist wichtig, um die Zuverlässigkeit und Leistung von direkte Speicherplätze sicherzustellen.

Windows Server 2016 führt Switch-Embedded-Team Vorgang (Set) im virtuellen Hyper-V-Switch ein. Dies ermöglicht die Verwendung derselben physischen NIC-Ports für den gesamten Netzwerk Datenverkehr bei Verwendung von RDMA, wodurch die Anzahl erforderlicher physischer NIC-Ports reduziert wird. Der Switch-Embedded-Team Vorgang wird für direkte Speicherplätze empfohlen.

Umgeschaltete oder switchlose Knoten Verbindungen
- Einschalten Netzwerk Switches müssen ordnungsgemäß für die Handhabung der Bandbreite und des Netzwerk Typs konfiguriert werden. Wenn Sie RDMA verwenden, das das ROCE-Protokoll implementiert, ist die Netzwerkgeräte-und Switchkonfiguration noch wichtiger.
- Switchlos: Knoten können mithilfe direkter Verbindungen miteinander verbunden werden, sodass die Verwendung eines Schalters vermieden wird. Es ist erforderlich, dass jeder Knoten über eine direkte Verbindung mit allen anderen Knoten des Clusters verfügt.

Anweisungen zum Einrichten von Netzwerken für direkte Speicherplätze finden Sie unter [Windows Server 2016 konvergierte NIC und Bereitstellungs Handbuch für Gast-RDMA](https://github.com/Microsoft/SDN/blob/master/Diagnostics/S2D%20WS2016_ConvergedNIC_Configuration.docx).

## <a name="step-3-configure-storage-spaces-direct"></a>Schritt 3: Konfigurieren von „Direkte Speicherplätze“

Die folgenden Schritte werden auf einem Verwaltungssystem durchgeführt, das über die gleiche Version wie die zu konfigurierenden Server verfügt. Die folgenden Schritte sollten nicht remote mithilfe einer PowerShell-Sitzung ausgeführt werden, sondern stattdessen in einer lokalen PowerShell-Sitzung auf dem Verwaltungssystem mit Administrator Berechtigungen ausgeführt werden.

### <a name="step-31-clean-drives"></a>Schritt 3,1: Laufwerke bereinigen

Stellen Sie vor dem Aktivieren von direkte Speicherplätze sicher, dass Ihre Laufwerke leer sind: keine alten Partitionen oder andere Daten. Führen Sie das folgende Skript aus, indem Sie Ihre Computernamen ersetzen, um alle alten Partitionen oder andere Daten zu entfernen.

> [!Warning]
> Mit diesem Skript werden alle Daten auf anderen Laufwerken als dem Betriebssystem-Start Laufwerk dauerhaft entfernt!

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"

Invoke-Command ($ServerList) {
    Update-StorageProviderCache
    Get-StoragePool | ? IsPrimordial -eq $false | Set-StoragePool -IsReadOnly:$false -ErrorAction SilentlyContinue
    Get-StoragePool | ? IsPrimordial -eq $false | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$false -ErrorAction SilentlyContinue
    Get-StoragePool | ? IsPrimordial -eq $false | Remove-StoragePool -Confirm:$false -ErrorAction SilentlyContinue
    Get-PhysicalDisk | Reset-PhysicalDisk -ErrorAction SilentlyContinue
    Get-Disk | ? Number -ne $null | ? IsBoot -ne $true | ? IsSystem -ne $true | ? PartitionStyle -ne RAW | % {
        $_ | Set-Disk -isoffline:$false
        $_ | Set-Disk -isreadonly:$false
        $_ | Clear-Disk -RemoveData -RemoveOEM -Confirm:$false
        $_ | Set-Disk -isreadonly:$true
        $_ | Set-Disk -isoffline:$true
    }
    Get-Disk | Where Number -Ne $Null | Where IsBoot -Ne $True | Where IsSystem -Ne $True | Where PartitionStyle -Eq RAW | Group -NoElement -Property FriendlyName
} | Sort -Property PsComputerName, Count
```

Die Ausgabe sieht wie folgt aus, wobei **count** die Anzahl der Laufwerke der einzelnen Modelle in jedem Server ist:

```
Count Name                          PSComputerName
----- ----                          --------------
4     ATA SSDSC2BA800G4n            Server01
10    ATA ST4000NM0033              Server01
4     ATA SSDSC2BA800G4n            Server02
10    ATA ST4000NM0033              Server02
4     ATA SSDSC2BA800G4n            Server03
10    ATA ST4000NM0033              Server03
4     ATA SSDSC2BA800G4n            Server04
10    ATA ST4000NM0033              Server04
```

### <a name="step-32-validate-the-cluster"></a>Schritt 3,2: Überprüfen des Clusters

In diesem Schritt führen Sie das Cluster Validierungs Tool aus, um sicherzustellen, dass die Server Knoten ordnungsgemäß konfiguriert sind, um einen Cluster mit direkte Speicherplätze zu erstellen. Wenn die Cluster Überprüfung (`Test-Cluster`) vor der Erstellung des Clusters ausgeführt wird, werden die Tests ausgeführt, mit denen überprüft wird, ob die Konfiguration für eine erfolgreiche Funktion als Failovercluster geeignet ist. Im folgenden Beispiel wird der Parameter "`-Include`" verwendet, und anschließend werden die spezifischen Testkategorien angegeben. Dadurch wird sichergestellt, dass die für „Direkte Speicherplätze“ spezifischen Tests in der Validierung enthalten sind.

Verwenden Sie den folgenden PowerShell-Befehl, um eine Gruppe von Servern zu überprüfen, die als Cluster für „Direkte Speicherplätze“ verwendet werden soll.

```PowerShell
Test-Cluster –Node <MachineName1, MachineName2, MachineName3, MachineName4> –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
```

### <a name="step-33-create-the-cluster"></a>Schritt 3,3: Erstellen des Clusters

In diesem Schritt erstellen Sie mit dem folgenden PowerShell-Cmdlet einen Cluster mit den Knoten, die Sie im vorherigen Schritt für die Cluster Erstellung überprüft haben.

Beim Erstellen des Clusters erhalten Sie eine Warnung mit dem Hinweis, dass beim Erstellen der Cluster Rolle Probleme aufgetreten sind, die den Start verhindern können. Weitere Informationen finden Sie in der folgenden Berichtsdatei.“ Sie können diese Warnung ignorieren. Die Ursache dieser Warnung liegt darin, dass keine Datenträger für das Clusterquorum verfügbar sind. Es wird empfohlen, nach der Erstellung des Clusters einen Dateifreigabe- oder Cloudzeugen zu konfigurieren.

> [!Note]
> Wenn die Server statische IP-Adressen verwenden, ändern Sie den folgenden Befehl so, dass die statische IP-Adresse reflektiert wird. Fügen Sie dazu den folgenden Parameter hinzu, und geben Sie die IP-Adresse an: „–StaticAddress &lt;X.X.X.X&gt;“.
> Im folgenden Befehl sollte der Platzhalter „ClusterName“ durch einen eindeutigen, aus maximal 15 Zeichen bestehenden NetBIOS-Namen ersetzt werden.
> ```PowerShell
> New-Cluster –Name <ClusterName> –Node <MachineName1,MachineName2,MachineName3,MachineName4> –NoStorage
> ```

Nach der Erstellung des Clusters kann es einige Zeit dauern, bis der DNS-Eintrag für den Clusternamen repliziert wurde. Wie lange, hängt von der Umgebung und der Konfiguration der DNS-Replikation ab. Wird der Clusters nicht erfolgreich aufgelöst, können Sie den Vorgang in den meisten Fällen erfolgreich ausführen, indem Sie anstelle des Clusternamens den Computernamen eines Knotens verwenden, der ein aktives Mitglied des Clusters ist.

### <a name="step-34-configure-a-cluster-witness"></a>Schritt 3,4: Konfigurieren eines Cluster Zeugen

Es wird empfohlen, einen Zeugen für den Cluster zu konfigurieren, sodass Cluster mit drei oder mehr Servern den Ausfall oder das offline schalten von zwei Servern überstehen können. Eine Bereitstellung mit zwei Servern erfordert einen Cluster Zeugen. andernfalls wird der andere Server auch offline geschaltet. Bei diesen Systemen können Sie eine Dateifreigabe als Zeugen bzw. Cloudzeugen verwenden. 

Weitere Informationen finden Sie unter den folgenden Themen:

- [Konfigurieren und Verwalten des Quorums](../../failover-clustering/manage-cluster-quorum.md)
- [Bereitstellen eines cloudzeugen für einen Failovercluster](../../failover-clustering/deploy-cloud-witness.md)

### <a name="step-35-enable-storage-spaces-direct"></a>Schritt 3,5: Aktivieren von „Direkte Speicherplätze“

Verwenden Sie nach dem Erstellen des Clusters das PowerShell-Cmdlet "`Enable-ClusterStorageSpacesDirect`", mit dem das Speichersystem in den direkte Speicherplätze Modus versetzt wird, und führen Sie die folgenden Schritte automatisch aus:

-   **Erstellen eines Pools:** Erstellt einen einzelnen großen Pool mit einem Namen wie "S2D on Cluster1".

-   **Konfiguriert die direkte Speicherplätze Caches:** Wenn mehr als ein Medien-(Laufwerktyp) für die direkte Speicherplätze Verwendung verfügbar ist, werden die schnellsten as-Cache Geräte aktiviert (in den meisten Fällen Lese-und Schreibvorgänge).

-   **Wirft** Erstellt zwei Ebenen als Standard Ebenen. Eine mit der Bezeichnung „Kapazität“, die andere mit der Bezeichnung „Leistung“. Das Cmdlet analysiert die Geräte und konfiguriert jede Ebene mit der Kombination aus Gerätetypen und Ausfallsicherheit (Resilienz).

Starten Sie aus dem Verwaltungssystem heraus den folgenden Befehl in einem PowerShell-Befehlsfenster, das mit Administratorrechten geöffnet wurde. Der Clustername ist der Name des Clusters, den Sie in den vorherigen Schritten erstellt haben. Wenn dieser Befehl lokal auf einem der Knoten ausgeführt wird, ist der Parameter -CimSession nicht erforderlich.

```PowerShell
Enable-ClusterStorageSpacesDirect –CimSession <ClusterName>
```

Um „Direkte Speicherplätze“ mit dem oben stehenden Befehl zu aktivieren, können Sie auch den Knotennamen anstelle des Clusternamens verwenden. Die Verwendung des Knotennamens ist unter Umständen zuverlässiger, da bei einem neu erstellten Clusternamen Verzögerungen bei der DNS-Replikation auftreten können.

Wenn die Ausführung des Befehls beendet ist, was einige Minuten dauern kann, ist das System bereit für die Erstellung von Volumes.

### <a name="step-36-create-volumes"></a>Schritt 3,6: Erstellen von Volumes

Es wird empfohlen, das Cmdlet "`New-Volume`" zu verwenden, da es die schnellste und einfachste Möglichkeit bietet. Dieses einzelne Cmdlet erstellt, partitioniert und formatiert automatisch den virtuellen Datenträger, erstellt das Volume mit demselben Namen und fügt es freigegebenen Clustervolumes hinzu – alles in einem einfachen Schritt.

Weitere Informationen finden Sie unter [Erstellen von Volumes in Direkte Speicherplätze](create-volumes.md).

### <a name="step-37-optionally-enable-the-csv-cache"></a>Schritt 3,7: Aktivieren Sie optional den CSV-Cache.

Optional können Sie den CSV-Cache (Cluster Shared Volume) für die Verwendung von System Arbeitsspeicher (RAM) als Schreibvorgang auf Blockebene von Lesevorgängen aktivieren, die nicht bereits vom Windows-Cache-Manager zwischengespeichert wurden. Dies kann die Leistung für Anwendungen wie Hyper-V verbessern. Der CSV-Cache kann die Leistung von Lese Anforderungen steigern und ist auch für Dateiserver mit horizontaler Skalierung-Szenarien nützlich.

Wenn Sie den CSV-Cache aktivieren, verringert sich der Arbeitsspeicher, der für die Ausführung von VMS in einem hyperkonvergenten Cluster verfügbar ist. Daher müssen Sie die Speicherleistung mit dem für VHDs verfügbaren Arbeitsspeicher ausgleichen.

Öffnen Sie zum Festlegen der Größe des CSV-Caches eine PowerShell-Sitzung auf dem Verwaltungssystem mit einem Konto, das über Administrator Berechtigungen für den Speicher Cluster verfügt, und verwenden Sie dieses Skript, um die Variablen "`$ClusterName`" und "`$CSVCacheSize`" nach Bedarf zu ändern (in diesem Beispiel wird 2 festgelegt. GB-CSV-Cache pro Server):

```PowerShell
$ClusterName = "StorageSpacesDirect1"
$CSVCacheSize = 2048 #Size in MB

Write-Output "Setting the CSV cache..."
(Get-Cluster $ClusterName).BlockCacheSize = $CSVCacheSize

$CSVCurrentCacheSize = (Get-Cluster $ClusterName).BlockCacheSize
Write-Output "$ClusterName CSV cache size: $CSVCurrentCacheSize MB"
```

Weitere Informationen finden Sie unter [Verwenden des CSV-Speichers im Arbeitsspeicher im Arbeitsspeicher](csv-cache.md).

### <a name="step-38-deploy-virtual-machines-for-hyper-converged-deployments"></a>Schritt 3,8: Bereitstellen von virtuellen Computern für hyperkonvergierte bereit Stellungen

Wenn Sie einen hyperkonvergierten Cluster bereitstellen, besteht der letzte Schritt darin, virtuelle Maschinen auf dem direkte Speicherplätze Cluster bereitzustellen.

Die Dateien der virtuellen Maschine sollten im CSV-Namespace des Systems gespeichert werden (Beispiel: c: \\clusterstorage @ no__t-1volume1), genau wie gruppierte VMs in Failoverclustern.

Sie können die in-Box-Tools oder andere Tools verwenden, um den Speicher und die virtuellen Maschinen zu verwalten, z. b. System Center Virtual Machine Manager.

## <a name="step-4-deploy-scale-out-file-server-for-converged-solutions"></a>Schritt 4: Bereitstellen von Dateiserver mit horizontaler Skalierung für konvergierte Lösungen

Wenn Sie eine konvergierte Lösung bereitstellen, ist der nächste Schritt das Erstellen einer Dateiserver mit horizontaler Skalierung Instanz und das Einrichten einiger Dateifreigaben. Wenn Sie einen hyperkonvergierten Cluster bereitstellen, sind Sie fertig und benötigen diesen Abschnitt nicht.

### <a name="step-41-create-the-scale-out-file-server-role"></a>Schritt 4,1: Erstellen der Dateiserver mit horizontaler Skalierung Rolle

Der nächste Schritt beim Einrichten der Cluster Dienste für den Dateiserver ist das Erstellen der Cluster Dateiserver-Rolle. Dies ist der Fall, wenn Sie die Dateiserver mit horizontaler Skalierung Instanz erstellen, auf der die fortlaufend verfügbaren Dateifreigaben gehostet werden.

#### <a name="to-create-a-scale-out-file-server-role-by-using-server-manager"></a>So erstellen Sie eine Dateiserver mit horizontaler Skalierung Rolle mithilfe von Server-Manager

1. Wählen Sie in Failovercluster-Manager den Cluster aus, navigieren Sie zu **Rollen**, und klicken Sie dann auf **Rolle konfigurieren...** .<br>Der Assistent für hohe Verfügbarkeit wird angezeigt.
2. Klicken Sie auf der Seite **Rolle auswählen** auf **Datei Server**.
3. Klicken Sie auf der Seite **Datei Servertyp** auf **Dateiserver mit horizontaler Skalierung für Anwendungsdaten**.
4. Geben Sie auf der Seite **Client Zugriffspunkt** einen Namen für das Dateiserver mit horizontaler Skalierung ein.
5. Überprüfen Sie, ob die Rolle erfolgreich eingerichtet wurde, indem Sie zu **Rollen** wechseln und sicherstellen, dass in der Spalte **Status** neben der erstellten Cluster Dateiserver-Rolle **ausgeführt** wird, wie in Abbildung 1 dargestellt.

   ![Screenshot der Failovercluster-Manager, die die Dateiserver mit horizontaler Skalierung](media/Hyper-converged-solution-using-Storage-Spaces-Direct-in-Windows-Server-2016/SOFS_in_FCM.png "Failovercluster-Manager anzeigt, die die Dateiserver mit horizontaler Skalierung")

    **Abbildung 1** Failovercluster-Manager mit dem Status "wird ausgeführt" Dateiserver mit horizontaler Skalierung angezeigt

> [!NOTE]
>  Nach dem Erstellen der Cluster Rolle können einige Verzögerungen bei der Netzwerk Weitergabe auftreten, die das Erstellen von Dateifreigaben für ein paar Minuten oder potenziell länger verhindern können.  
  
#### <a name="to-create-a-scale-out-file-server-role-by-using-windows-powershell"></a>So erstellen Sie eine Dateiserver mit horizontaler Skalierung Rolle mithilfe von Windows PowerShell

 Geben Sie in einer Windows PowerShell-Sitzung, die mit dem Dateiserver Cluster verbunden ist, die folgenden Befehle ein, um die Dateiserver mit horizontaler Skalierung-Rolle zu erstellen, und ändern Sie den *fscluester* so, dass er dem Namen Ihres Clusters entspricht, und *sofs* entsprechend dem Namen, den Sie dem Dateiserver mit horizontaler Skalierung Rolle:

```PowerShell
Add-ClusterScaleOutFileServerRole -Name SOFS -Cluster FSCLUSTER
```

> [!NOTE]
>  Nach dem Erstellen der Cluster Rolle können einige Verzögerungen bei der Netzwerk Weitergabe auftreten, die das Erstellen von Dateifreigaben für ein paar Minuten oder potenziell länger verhindern können. Wenn die sofs-Rolle nicht sofort ausfällt und nicht gestartet werden kann, liegt dies möglicherweise daran, dass das Computer Objekt des Clusters nicht über die Berechtigung zum Erstellen eines Computer Kontos für die sofs-Rolle verfügt. Hilfe hierzu finden Sie in diesem Blogbeitrag: [Dateiserver mit horizontaler Skalierung Rolle kann nicht mit den Ereignis-IDs 1205, 1069 und 1194 gestartet](http://www.aidanfinn.com/?p=14142)werden.

### <a name="step-42-create-file-shares"></a>Schritt 4,2: Erstellen von Dateifreigaben

Nachdem Sie die virtuellen Datenträger erstellt und den csvs hinzugefügt haben, ist es an der Zeit, Dateifreigaben auf diesen zu erstellen, eine Dateifreigabe pro CSV und virtuellem Datenträger. System Center Virtual Machine Manager (VMM) ist wahrscheinlich die schwierigste Methode, da Sie die Berechtigungen für Sie erledigt, aber wenn Sie Sie nicht in Ihrer Umgebung haben, können Sie die Bereitstellung mithilfe von Windows PowerShell teilweise automatisieren.

Verwenden Sie die Skripts in der [SMB-Freigabe Konfiguration für Hyper-V-Arbeits Auslastungs](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) Skripts, die den Prozess zum Erstellen von Gruppen und Freigaben teilweise automatisiert. Sie wird für Hyper-V-Arbeits Auslastungen geschrieben. Wenn Sie also andere Workloads bereitstellen, müssen Sie möglicherweise die Einstellungen ändern oder weitere Schritte ausführen, nachdem Sie die Freigaben erstellt haben. Wenn Sie z. b. Microsoft SQL Server verwenden, muss dem SQL Server-Dienst Konto Vollzugriff auf die Freigabe und das Dateisystem gewährt werden.

> [!NOTE]
>  Sie müssen die Gruppenmitgliedschaft aktualisieren, wenn Sie Cluster Knoten hinzufügen, es sei denn, Sie verwenden System Center Virtual Machine Manager, um Ihre Freigaben zu erstellen.

Gehen Sie folgendermaßen vor, um Dateifreigaben mithilfe von PowerShell-Skripts zu erstellen:

1. Laden Sie die in der [SMB-Freigabe Konfiguration für Hyper-V-Arbeits Auslastungen](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) enthaltenen Skripts auf einen der Knoten des Dateiserver Clusters herunter.
2. Öffnen Sie eine Windows PowerShell-Sitzung mit Anmelde Informationen des Domänen Administrators auf dem Verwaltungssystem, und erstellen Sie dann mit dem folgenden Skript eine Active Directory Gruppe für die Hyper-V-Computer Objekte. ändern Sie die Werte für die Variablen entsprechend Ihren Umgebung

    ```PowerShell
    # Replace the values of these variables
    $HyperVClusterName = "Compute01"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of script itself
    CD $ScriptFolder
    .\ADGroupSetup.ps1 -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName -HyperVClusterName $HyperVClusterName
    ```
3. Öffnen Sie eine Windows PowerShell-Sitzung mit Administrator Anmelde Informationen auf einem der Speicher Knoten, und verwenden Sie dann das folgende Skript, um Freigaben für jede CSV-Datei zu erstellen und der Gruppe "Domänen-Admins" und dem Computecluster Administrator Berechtigungen zu erteilen.

    ```PowerShell
    # Replace the values of these variables
    $StorageClusterName = "StorageSpacesDirect1"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $SOFSName = "SOFS"
    $SharePrefix = "Share"
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of the script itself
    CD $ScriptFolder
    Get-ClusterSharedVolume -Cluster $StorageClusterName | ForEach-Object
    {
        $ShareName = $SharePrefix + $_.SharedVolumeInfo.friendlyvolumename.trimstart("C:\ClusterStorage\Volume")
        Write-host "Creating share $ShareName on "$_.name "on Volume: " $_.SharedVolumeInfo.friendlyvolumename
        .\FileShareSetup.ps1 -HyperVClusterName $StorageClusterName -CSVVolumeNumber $_.SharedVolumeInfo.friendlyvolumename.trimstart("C:\ClusterStorage\Volume") -ScaleOutFSName $SOFSName -ShareName $ShareName -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName
    }
    ```

### <a name="step-43-enable-kerberos-constrained-delegation"></a>Schritt 4,3 Aktivieren der eingeschränkten Kerberos-Delegierung

Wenn Sie die eingeschränkte Kerberos-Delegierung für die Remote szenarioverwaltung einrichten und die Livemigration Sicherheit erhöhen möchten, verwenden Sie auf einem der Speicher Cluster Knoten das in der [SMB-Freigabe Konfiguration für Hyper-V-Arbeits Auslastungen](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)enthaltene Skript kcdsetup. ps1. Hier ist ein kleines Wrapper für das Skript:

```PowerShell
$HyperVClusterName = "Compute01"
$ScaleOutFSName = "SOFS"
$ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

CD $ScriptFolder
.\KCDSetup.ps1 -HyperVClusterName $HyperVClusterName -ScaleOutFSName $ScaleOutFSName -EnableLM
```

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie den Cluster Dateiserver bereitgestellt haben, empfiehlt es sich, die Leistung Ihrer Lösung mithilfe synthetischer Workloads zu testen, bevor Sie echte Workloads bereitstellen. Auf diese Weise können Sie überprüfen, ob die Lösung ordnungsgemäß funktioniert, und alle veralteten Probleme beheben, bevor Sie die Komplexität von Workloads hinzufügen. Weitere Informationen finden Sie unter [Testen der Leistung von Speicherplätzen mithilfe synthetischer Workloads](https://technet.microsoft.com/library/dn894707.aspx).

## <a name="see-also"></a>Siehe auch

-   [Direkte Speicherplätze in Windows Server 2016](storage-spaces-direct-overview.md)
-   [Grundlegendes zum Cache in direkte Speicherplätze](understand-the-cache.md)
-   [Planen von Volumes in direkte Speicherplätze](plan-volumes.md)
-   [Fehlertoleranz bei Speicherplätzen](storage-spaces-fault-tolerance.md)
-   [Direkte Speicherplätze Hardware Anforderungen](Storage-Spaces-Direct-Hardware-Requirements.md)
-   [To RDMA, or not to RDMA – that is the question](https://blogs.technet.microsoft.com/filecab/2017/03/27/to-rdma-or-not-to-rdma-that-is-the-question/) (RDMA oder kein RDMA – das ist hier die Frage) (TechNet-Blog)
