---
title: Bereitstellen von direkte Speicherplätze
ms.prod: windows-server-threshold
manager: eldenc
ms.author: stevenek
ms.technology: storage-spaces
ms.topic: get-started-article
ms.assetid: 20fee213-8ba5-4cd3-87a6-e77359e82bc0
author: stevenek
ms.date: 06/07/2019
description: Schrittweise Anleitungen zum Bereitstellen von Software-definiertem Speicher mit Storage Spaces Direct in Windows Server als hyperkonvergenten Infrastruktur oder konvergierte (auch bekannt als disaggregierten)-Infrastruktur.
ms.localizationpriority: medium
ms.openlocfilehash: a4159c85be23025ef57084b47dcc77d4f749888f
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812355"
---
# <a name="deploy-storage-spaces-direct"></a>Bereitstellen von direkte Speicherplätze

> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält schrittweise Anweisungen zum Bereitstellen von ["direkte Speicherplätze"](storage-spaces-direct-overview.md).

> [!Tip]
> Suche nach Hyper-Converged Infrastruktur? Microsoft empfiehlt, erwerben eine überprüfte Hardware/Software-Lösung von unseren Partnern, die von Bereitstellungstools und Verfahren enthalten. Diese Lösungen werden entworfen, zusammengesetzt und für unsere Referenzarchitektur, um sicherzustellen, dass Kompatibilität und Zuverlässigkeit, damit Sie Sie nutzen und schnell überprüft. 2019 für Windows Server-Lösungen finden Sie auf die [Solutions-Website für Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci). Für Windows Server 2016-Lösungen, erfahren Sie mehr unter [Windows Server-Software-Defined](https://microsoft.com/wssd).

> [!Tip]
> Sie können Hyper-V-VMs, einschließlich der in Microsoft Azure zu verwenden, ["direkte Speicherplätze" auswerten, ohne Hardware](storage-spaces-direct-in-vm.md). Sie sollten auch die praktische überprüfen [Bereitstellungsskripts für Windows Server-schnelle Lab](https://aka.ms/wslab), der für trainingszwecke verwendet.

## <a name="before-you-start"></a>Bevor Sie beginnen

Überprüfen Sie die ["direkte Speicherplätze" hardwareanforderungen](Storage-Spaces-Direct-Hardware-Requirements.md) und Überfliegen Sie dieses Dokument, um sich mit den allgemeinen Ansatz und die wichtigen Hinweise zu bestimmten Schritten vertraut zu machen.

Erfassen Sie die folgende Informationen an:

- **Bereitstellungsoption.** "Direkte Speicherplätze" unterstützt [zwei Bereitstellungsoptionen: hyper-konvergiert und zusammengeführte](storage-spaces-direct-overview.md#deployment-options), auch bekannt als disaggregierten. Machen Sie sich mit den Vorteilen der einzelnen entscheiden, was für Sie geeignet ist. Schritte 1 bis 3 unten gelten für beide Optionen. Schritt 4 ist nur für konvergente Bereitstellung erforderlich.

- **Server-Namen.** Machen Sie mit den Benennungskonventionen Ihrer Organisation für Computer, Dateien, Pfade und andere Ressourcen vertraut. Sie müssen zum Bereitstellen von mehreren Servern, jeweils eindeutige Namen.

- **Domänenname.** Mit den Richtlinien Ihres Unternehmens für benennungs- und Domänenbeitritt vertraut.  Sie werden die Server werden mit der Domäne beitreten, und Sie müssen den Domänennamen angeben. 

- **RDMA-Netzwerk.** Es gibt zwei Arten von RDMA-Protokollen: iWarp und RoCE. Beachten Sie die Ihre Netzwerkadapter verwenden, und wenn RoCE, beachten Sie auch die Version (v1 oder v2). Beachten Sie außerdem für RoCE das Modell des Top-of-Rack-Switches.

- **VLAN-ID.** Beachten Sie die VLAN-ID für das Verwaltungsbetriebssystem-Netzwerkadaptern auf den Servern verwendet werden, sofern vorhanden. Diese sollten Sie von Ihrem Netzwerkadministrator erhalten.

## <a name="step-1-deploy-windows-server"></a>Schritt 1: Bereitstellen von WindowsServer

### <a name="step-11-install-the-operating-system"></a>Schritt 1.1: Installieren des Betriebssystems

Der erste Schritt ist zum Installieren von Windows Server auf jedem Server, die im Cluster. "Direkte Speicherplätze" ist Windows Server 2016 Datacenter Edition erforderlich. Sie können die Server Core-Installationsoption oder den Server mit Desktopdarstellung verwenden.

Wenn Sie Windows-Server mithilfe des Setup-Assistenten installieren, können Sie zwischen *WindowsServer* (in Bezug auf Server Core) und *Windows Server (Server mit Desktopdarstellung)* , entspricht von der *vollständige* Installationsoption in Windows Server 2012 R2 verfügbar. Wenn Sie nicht auswählen, erhalten Sie die Server Core-Installationsoption. Weitere Informationen finden Sie unter [Installation Optionen für Windows Server 2016](../../get-started/Windows-Server-2016.md).

### <a name="step-12-connect-to-the-servers"></a>Schritt 1.2: Eine Verbindung mit Server herstellen

Dieser Leitfaden konzentriert sich die Server Core-Installationsoption und Bereitstellen von/Verwalten von einem separaten Managementsystem aufweisen muss:

- Windows Server 2016 mit den gleichen Updates wie die verwalteten Server
- Über eine Netzwerkverbindung mit den verwalteten Servern
- Der gleichen Domäne oder einer voll vertrauenswürdigen Domäne angehören
- Remoteserver-Verwaltungstools (RSAT) und PowerShell-Module für Hyper-V und Failoverclustering. RSAT-Tools und PowerShell-Module sind auf Windows Server verfügbar und können ohne weitere Features installiert werden. Sie können auch installieren, die [Remoteserver-Verwaltungstools](https://www.microsoft.com/download/details.aspx?id=45520) auf einem Windows 10-Management-PC.

Installieren Sie auf dem Verwaltungssystem den Failovercluster sowie Hyper-V-Verwaltungstools. Dies kann über Server Manager mithilfe des Assistenten zum **Hinzufügen von Rollen und Features**. Wählen Sie auf der Seite **Features** die Option **Remoteserver-Verwaltungstools** und dann die zu installierenden Tools aus.

Geben Sie die PS-Sitzung ein, und verwenden Sie entweder den Servernamen oder die IP-Adresse des Knotens, mit dem Sie eine Verbindung herstellen möchten. Sie werden zur Kennworteingabe aufgefordert werden, nachdem Sie diesen Befehl ausführen, geben Sie das Administratorkennwort, die Sie beim Einrichten von Windows angegeben.

   ```PowerShell
   Enter-PSSession -ComputerName <myComputerName> -Credential LocalHost\Administrator
   ```

   Hier ist ein Beispiel von etwas, was auf eine Weise, die in Skripts, die nützlicher ist für den Fall, dass Sie dies mehrere Male ausführen müssen:

   ```PowerShell
   $myServer1 = "myServer-1"
   $user = "$myServer1\Administrator"

   Enter-PSSession -ComputerName $myServer1 -Credential $user
   ```

> [!TIP]
> Wenn Sie Remote von einem Verwaltungssystem bereitstellen, erhalten Sie möglicherweise eine Fehlermeldung wie *WinRM die Anforderung nicht verarbeiten kann.* Um dieses Problem zu beheben, verwenden Sie Windows PowerShell, um die Liste mit vertrauenswürdigen Hosts auf dem Verwaltungscomputer jeder Server hinzuzufügen:  
>   
> `Set-Item WSMAN:\Localhost\Client\TrustedHosts -Value Server01 -Force`
>  
> Hinweis: die Liste mit vertrauenswürdigen Hosts unterstützt Platzhalter, z. B. `Server*`.
>
> Geben Sie zum Anzeigen Ihrer Liste mit vertrauenswürdigen Hosts `Get-Item WSMAN:\Localhost\Client\TrustedHosts`.  
>   
> Um die Liste leer ist, geben Sie `Clear-Item WSMAN:\Localhost\Client\TrustedHost`.  

### <a name="step-13-join-the-domain-and-add-domain-accounts"></a>Schritt 1.3: Treten Sie zur Domäne bei und fügen Domänenkonten hinzu

Bisher haben Sie die einzelnen Server konfiguriert haben, mit dem lokalen Administratorkonto, `<ComputerName>\Administrator`.

Um "direkte Speicherplätze" zu verwalten, müssen Sie die Server in eine Domäne einbinden und verwenden Sie ein Domänenkonto für Active Directory Domain Services, die in der Gruppe "Administratoren" auf jedem Server ist.

Öffnen Sie aus dem Verwaltungssystem eine PowerShell-Konsole mit Administratorrechten aus. Verwendung `Enter-PSSession` eine Verbindung mit jedem Server, und führen Sie das folgende Cmdlet aus, und Ersetzen Sie dabei Ihre eigenen Computername, Domänenname und Anmeldeinformationen für die Domäne:

```PowerShell  
Add-Computer -NewName "Server01" -DomainName "contoso.com" -Credential "CONTOSO\User" -Restart -Force  
```

Wenn Ihr Storage-Administratorkonto Mitglied der Gruppe "Domänen-Admins" ist, fügen Sie Ihr Speicherkonto für den Administrator der lokalen Administratorgruppe auf jedem Knoten - oder besser noch, fügen Sie der Gruppe, die Sie für die Speicher-Administratoren verwenden. Sie können den folgenden Befehl verwenden (oder Schreiben Sie eine Windows PowerShell-Funktion so tun, finden Sie unter [Verwenden von PowerShell zum Hinzufügen von Domänen-Benutzer zu einer lokalen Gruppe](http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/19/use-powershell-to-add-domain-users-to-a-local-group.aspx) Informationen):

```
Net localgroup Administrators <Domain\Account> /add
```

### <a name="step-14-install-roles-and-features"></a>Schritt 1.4: Installieren von Rollen und features

Im nächste Schritt werden Serverrollen auf jedem Server installieren. Sie erreichen dies, indem [Windows Admin Center](../../manage/windows-admin-center/use/manage-servers.md), [Server-Manager](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)), oder PowerShell. Hier sind die Rollen zu installieren:

- Failoverclustering
- Hyper-V
- Dateiserver (falls keine Dateifreigaben, z. B. für eine konvergenten Bereitstellung gehostet werden soll)
- Daten-Center-Bridging (Wenn Sie RoCEv2 anstelle von iWARP Netzwerkadaptern verwenden)
- RSAT-Clustering-PowerShell
- Hyper-V-PowerShell

Verwenden Sie zum Installieren mithilfe von PowerShell die [Install-WindowsFeature](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature) Cmdlet. Sie können es auf einem einzelnen Server wie folgt verwenden:

```PowerShell
Install-WindowsFeature -Name "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"
```

Führen Sie den Befehl auf allen Servern im Cluster gleichzeitig mit minimalem-Skript, ändern die Liste der Variablen am Anfang des Skripts für Ihre Umgebung geeigneten.

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

Wenn Sie "direkte Speicherplätze" in virtuellen Computern bereitstellen möchten, überspringen Sie diesen Abschnitt.

"Direkte Speicherplätze" ist erforderlich, hoher Bandbreite, geringer Latenz Netzwerk zwischen Servern im Cluster. Mindestens 10-GbE-Netzwerk ist erforderlich, und remote direct Memory Access (RDMA) wird empfohlen. Sie können entweder iWARP oder RoCE verwenden, solange das Windows Server 2016-Logo hat, iWARP ist jedoch in der Regel einfacher einrichten.

> [!Important]
> Einige Konfigurationen auf dem Tor Switch kann erforderlich sein, je nach Ihrer Netzwerkkomponenten und insbesondere mit RoCE v2. Richtige Netzwerkswitch-Konfiguration ist wichtig, um Zuverlässigkeit und Leistung von "direkte Speicherplätze" zu gewährleisten.

Windows Server 2016 führt Switch embedded teaming (SET) innerhalb des virtuellen Hyper-V-Switches. Dadurch können die gleichen physischen NIC-Ports für den Netzwerkdatenverkehr verwendet werden, bei der Verwendung von RDMA, Reduzieren der Anzahl der physischen NIC-Ports, die erforderlich sind. Switch embedded teaming für "direkte Speicherplätze" empfohlen.

Anweisungen zum Einrichten von Netzwerken für "direkte Speicherplätze" finden Sie [Windows Server 2016-Converged-NIC und Gast-RDMA-Bereitstellungshandbuch](https://github.com/Microsoft/SDN/blob/master/Diagnostics/S2D%20WS2016_ConvergedNIC_Configuration.docx).

## <a name="step-3-configure-storage-spaces-direct"></a>Schritt 3: Konfigurieren von „Direkte Speicherplätze“

Die folgenden Schritte werden auf einem Verwaltungssystem durchgeführt, das über die gleiche Version wie die zu konfigurierenden Server verfügt. Die folgenden Schritte sollten nicht werden Remote mithilfe einer PowerShell-Sitzungs ausgeführt, sondern stattdessen in einer lokalen PowerShell-Sitzung auf dem Verwaltungssystem mit Administratorberechtigungen ausführen.

### <a name="step-31-clean-drives"></a>Schritt 3.1: Laufwerke reinigen

Bevor Sie "direkte Speicherplätze" aktivieren, sicherzustellen, dass die Laufwerke leer sind: keine alten Partitionen oder andere Daten. Führen Sie das folgende Skript, und Ersetzen Sie dabei Ihre Computernamen, um alle alten Partitionen oder andere Daten zu entfernen.

> [!Warning]
> Dieses Skript werden alle Daten auf alle Laufwerke außer das Startlaufwerk Betriebssystem dauerhaft entfernt.

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

Die Ausgabe sieht wie folgt, wobei **Anzahl** ist die Anzahl der Laufwerke der einzelnen Modelle auf jedem Server:

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

### <a name="step-32-validate-the-cluster"></a>Schritt 3.2: Überprüfen des Clusters

In diesem Schritt führen Sie das Tool zur clustervalidierung um sicherzustellen, dass die Serverknoten ordnungsgemäß konfiguriert sind, zum Erstellen eines Clusters mithilfe von "direkte Speicherplätze". Bei der Clusterüberprüfung (`Test-Cluster`) wird ausgeführt, bevor der Cluster erstellt wird, sie führt die Tests, die prüfen, ob die Konfiguration erfolgreich funktioniert als Failovercluster geeignet ist. Im Beispiel unten verwendet direkt den `-Include` -Parameter, und klicken Sie dann die einzelnen Testkategorien angegeben. Dadurch wird sichergestellt, dass die für „Direkte Speicherplätze“ spezifischen Tests in der Validierung enthalten sind.

Verwenden Sie den folgenden PowerShell-Befehl, um eine Gruppe von Servern zu überprüfen, die als Cluster für „Direkte Speicherplätze“ verwendet werden soll.

```PowerShell
Test-Cluster –Node <MachineName1, MachineName2, MachineName3, MachineName4> –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
```

### <a name="step-33-create-the-cluster"></a>Schritt 3.3: Erstellen des Clusters

In diesem Schritt erstellen Sie einen Cluster mit den Knoten, die Sie für die Erstellung des Clusters im vorherigen Schritt mit dem folgenden PowerShell-Cmdlet überprüft haben.

Beim Erstellen des Clusters, erhalten Sie eine Warnung angezeigt: "sind Probleme beim Erstellen der Clusterrolle, Start verhindern kann. Weitere Informationen finden Sie in der folgenden Berichtsdatei.“ Sie können diese Warnung ignorieren. Die Ursache dieser Warnung liegt darin, dass keine Datenträger für das Clusterquorum verfügbar sind. Es wird empfohlen, nach der Erstellung des Clusters einen Dateifreigabe- oder Cloudzeugen zu konfigurieren.

> [!Note]
> Wenn die Server statische IP-Adressen verwenden, ändern Sie den folgenden Befehl so, dass die statische IP-Adresse reflektiert wird. Fügen Sie dazu den folgenden Parameter hinzu, und geben Sie die IP-Adresse an: „–StaticAddress &lt;X.X.X.X&gt;“.
> Im folgenden Befehl sollte der Platzhalter „ClusterName“ durch einen eindeutigen, aus maximal 15 Zeichen bestehenden NetBIOS-Namen ersetzt werden.
> ```PowerShell
> New-Cluster –Name <ClusterName> –Node <MachineName1,MachineName2,MachineName3,MachineName4> –NoStorage
> ```

Nach der Erstellung des Clusters kann es einige Zeit dauern, bis der DNS-Eintrag für den Clusternamen repliziert wurde. Wie lange, hängt von der Umgebung und der Konfiguration der DNS-Replikation ab. Wird der Clusters nicht erfolgreich aufgelöst, können Sie den Vorgang in den meisten Fällen erfolgreich ausführen, indem Sie anstelle des Clusternamens den Computernamen eines Knotens verwenden, der ein aktives Mitglied des Clusters ist.

### <a name="step-34-configure-a-cluster-witness"></a>Schritt 3.4: Konfigurieren eines clusterzeugen

Es wird empfohlen, dass Sie einen Zeugen für den Cluster konfigurieren, damit der Cluster mit drei oder mehr Servern zwei Server ausfällt oder offline überstehen können. Eine Bereitstellung auf zwei Servern erfordert einen clusterzeugen, andernfalls entweder Server offline geschaltet, führt dazu, dass der andere ebenfalls nicht mehr verfügbar ist. Bei diesen Systemen können Sie eine Dateifreigabe als Zeugen bzw. Cloudzeugen verwenden. 

Weitere Informationen finden Sie unter den folgenden Themen:

- [Konfigurieren und Verwalten des Quorums](../../failover-clustering/manage-cluster-quorum.md)
- [Bereitstellen eines Cloudzeugen für einen Failovercluster](../../failover-clustering/deploy-cloud-witness.md)

### <a name="step-35-enable-storage-spaces-direct"></a>Schritt 3.5: Aktivieren von „Direkte Speicherplätze“

Verwenden Sie nach dem Erstellen des Clusters an, die `Enable-ClusterStorageSpacesDirect` PowerShell-Cmdlet, das das Speichersystem in den "direkte Speicherplätze"-Modus versetzt werden, und führen Sie folgende Schritte automatisch:

-   **Erstellen eines Pools:** Erstellt einen einzelnen großen Pool mit dem Namen z. B. "S2D auf Cluster1".

-   **Konfiguriert den "direkte Speicherplätze"-Caches:** Wenn es mehr als ein Medientyp (Laufwerk) Typ für "direkte Speicherplätze" verwenden, können sie die schnellsten Typen als cachegeräte (Lesen und Schreiben in den meisten Fällen)

-   **Ebenen:** Erstellt zwei Ebenen als Standardebenen. Eine mit der Bezeichnung „Kapazität“, die andere mit der Bezeichnung „Leistung“. Das Cmdlet analysiert die Geräte und konfiguriert jede Ebene mit der Kombination aus Gerätetypen und Ausfallsicherheit (Resilienz).

Starten Sie aus dem Verwaltungssystem heraus den folgenden Befehl in einem PowerShell-Befehlsfenster, das mit Administratorrechten geöffnet wurde. Der Clustername ist der Name des Clusters, den Sie in den vorherigen Schritten erstellt haben. Wenn dieser Befehl lokal auf einem der Knoten ausgeführt wird, ist der Parameter -CimSession nicht erforderlich.

```PowerShell
Enable-ClusterStorageSpacesDirect –CimSession <ClusterName>
```

Um „Direkte Speicherplätze“ mit dem oben stehenden Befehl zu aktivieren, können Sie auch den Knotennamen anstelle des Clusternamens verwenden. Die Verwendung des Knotennamens ist unter Umständen zuverlässiger, da bei einem neu erstellten Clusternamen Verzögerungen bei der DNS-Replikation auftreten können.

Wenn die Ausführung des Befehls beendet ist, was einige Minuten dauern kann, ist das System bereit für die Erstellung von Volumes.

### <a name="step-36-create-volumes"></a>Schritt 3.6: Erstellen von Volumes

Es wird empfohlen, die `New-Volume` Cmdlet als es bietet die schnellste und einfachste. Dieses einzelne Cmdlet erstellt, partitioniert und formatiert automatisch den virtuellen Datenträger, erstellt das Volume mit demselben Namen und fügt es freigegebenen Clustervolumes hinzu – alles in einem einfachen Schritt.

Weitere Informationen finden Sie unter [Erstellen von Volumes in Direkte Speicherplätze](create-volumes.md).

### <a name="step-37-optionally-enable-the-csv-cache"></a>Schritt 3.7: Aktivieren Sie optional den CSV-cache

Sie können optional den freigegebenen Clustervolume (CSV) Cache Systemspeicher (RAM) als Write-through-Blockebene Cache von Lesevorgängen verwendet werden, die von der Windows-Cache-Manager bereits zwischengespeichert sind nicht aktivieren. Dies kann die Leistung von Anwendungen wie Hyper-V verbessern. Der CSV-Cache kann die Leistung von leseanforderungen steigern und ist auch nützlich für Szenarien, Scale-Out File Server.

Aktivieren des CSV-Caches reduziert die Menge an Arbeitsspeicher für virtuelle Computer in einem hyperkonvergenten Cluster ausgeführt, daher Sie die speicherleistung auf virtuellen Festplatten verfügbare Arbeitsspeicher ausgleichen müssen verfügbar.

Um die Größe des CSV-Caches festzulegen, öffnen Sie auf dem Verwaltungssystem eine PowerShell-Sitzung mit einem Konto mit Administratorberechtigungen auf dem speichercluster und verwenden Sie dann mit diesem Skript, das Ändern der `$ClusterName` und `$CSVCacheSize` Variablen (dies angemessen Beispiel wird einen CSV-Cache von 2 GB pro Server):

```PowerShell
$ClusterName = "StorageSpacesDirect1"
$CSVCacheSize = 2048 #Size in MB

Write-Output "Setting the CSV cache..."
(Get-Cluster $ClusterName).BlockCacheSize = $CSVCacheSize

$CSVCurrentCacheSize = (Get-Cluster $ClusterName).BlockCacheSize
Write-Output "$ClusterName CSV cache size: $CSVCurrentCacheSize MB"
```

Weitere Informationen finden Sie unter [mithilfe der CSV-in-Memory-Lesecache](csv-cache.md).

### <a name="step-38-deploy-virtual-machines-for-hyper-converged-deployments"></a>Schritt 3.8: Bereitstellen von virtuellen Computern für die hyperkonvergente Bereitstellung

Wenn Sie einen hyperkonvergenten Cluster bereitstellen, ist der letzte Schritt, um virtuelle Computer im Cluster "direkte Speicherplätze" bereitzustellen.

Für den Namespace des Systems CSV-Dateien der virtuellen Maschine gespeichert werden sollen (Beispiel: c:\\ClusterStorage\\Volume1) genau wie gruppierte virtuelle Computer in Failoverclustern.

Sie können mitgelieferte Tools oder andere Tools verwenden, auf um den Speicher und virtuelle Computer, z. B. System Center Virtual Machine Manager zu verwalten.

## <a name="step-4-deploy-scale-out-file-server-for-converged-solutions"></a>Schritt 4: Bereitstellen Sie Scale-Out File Server für die zusammengeführten Lösungen

Wenn Sie eine zusammengeführte Lösung bereitstellen, werden im nächste Schritt erstellen Sie eine Instanz von Scale-Out File Server, und richten einige Dateifreigaben. Bei der Bereitstellung eines hyperkonvergenten Clusters: Sie fertig sind und nicht, benötigen Sie diesen Abschnitt.

### <a name="step-41-create-the-scale-out-file-server-role"></a>Schritt 4.1: Erstellen Sie den Scale-Out File Server-Rolle

Der nächste Schritt bei der Einrichtung der Clusterdienste für Ihren Dateiserver ist das Erstellen der gruppierten Dateiserverrolle, handelt es sich bei der Erstellung der Scale-Out File Server-Instanz in der Ihre fortlaufend verfügbare Dateifreigaben gehostet werden.

#### <a name="to-create-a-scale-out-file-server-role-by-using-server-manager"></a>So erstellen Sie eine Scale-Out File Server-Rolle mithilfe von Server-Manager

1. Im Failovercluster-Manager, wählen Sie den Cluster, wechseln Sie zur **Rollen**, und klicken Sie dann auf **Rolle konfigurieren...** .<br>Assistenten für hohe Verfügbarkeit wird angezeigt.
2. Auf der **Select Role** auf **Dateiserver**.
3. Auf der **Dateiservertyp** auf **Scale-Out File Server für Anwendungsdaten**.
4. Auf der **Clientzugriffspunkt** geben einen Namen für den Dateiserver für horizontales Skalieren.
5. Stellen Sie sicher, dass die Rolle erfolgreich eingerichtet wurde, indem Sie auf **Rollen** und bestätigt, dass die **Status** zeigt Spalte **ausführen** neben der gruppierten Dateiserverrolle, die Sie erstellt haben, wie in Abbildung 1 dargestellt.

   ![Screenshot des Failovercluster-Managers mit dem Dateiserver für horizontales Skalieren](media/Hyper-converged-solution-using-Storage-Spaces-Direct-in-Windows-Server-2016/SOFS_in_FCM.png "Failovercluster-Manager mit dem Dateiserver für horizontales Skalieren")

    **Abbildung 1** Failovercluster-Manager zeigt die Scale-Out File Server, mit dem Status wird ausgeführt

> [!NOTE]
>  Nach dem Erstellen der Clusterrolle "", gibt es möglicherweise einige Netzwerk Verzögerungen bei der Verteilung, die Erstellung von Dateifreigaben auf einige Minuten oder möglicherweise längere verhindern könnten.  
  
#### <a name="to-create-a-scale-out-file-server-role-by-using-windows-powershell"></a>So erstellen Sie eine Scale-Out File Server-Rolle mithilfe von Windows PowerShell

 Geben Sie die folgenden Befehle zum Erstellen der Scale-Out File Server-Rolle, und ändern, in einer Windows PowerShell-Sitzung, die mit dem Dateiservercluster verbunden ist, *FSCLUSTER* mit dem Namen Ihres Clusters übereinstimmen und *SOFS* mit dem Namen übereinstimmen, den Scale-Out File Server-Rolle zuweisen möchten:

```PowerShell
Add-ClusterScaleOutFileServerRole -Name SOFS -Cluster FSCLUSTER
```

> [!NOTE]
>  Nach dem Erstellen der Clusterrolle "", gibt es möglicherweise einige Netzwerk Verzögerungen bei der Verteilung, die Erstellung von Dateifreigaben auf einige Minuten oder möglicherweise längere verhindern könnten. Wenn der SOFS-Rolle schlägt sofort fehl und wird nicht gestartet werden, kann möglicherweise Computerobjekt des Clusters über die Berechtigung zum Erstellen eines Computerkontos für die SOFS-Rolle verfügt. Hilfe zur, finden Sie in diesem Blogbeitrag: [Horizontale Skalierung Datei Rolle ausfällt, beginnen Sie mit der Ereignis-IDs 1205, 1069 und 1194](http://www.aidanfinn.com/?p=14142).

### <a name="step-42-create-file-shares"></a>Schritt 4.2: Erstellen von Dateifreigaben

Nachdem Sie Ihre virtuellen Datenträger erstellt und CSV hinzugefügt haben, ist es Zeit, die Dateifreigaben auf – Erstellen einer Dateifreigabe pro CSV pro virtuellen Datenträger. System Center Virtual Machine Manager (VMM) ist wahrscheinlich die handiest Möglichkeit hierzu, da er die Berechtigungen für Sie verarbeitet, aber wenn Sie in Ihrer Umgebung nicht darüber verfügen, Sie Windows PowerShell, zum teilweise automatisieren der Bereitstellung verwenden können.

Verwenden Sie die Skripts enthalten, die der [SMB-Freigabe-Konfiguration für Hyper-V-Arbeitsauslastungen](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) Skript, das den Prozess zum Erstellen von Gruppen und Freigaben teilweise automatisiert. Es hat sich für Hyper-V-Workloads, wenn Sie andere arbeitsauslastungen bereitstellen, Sie müssen also ggf. ändern Sie die Einstellungen oder zusätzliche Schritte ausführen, nachdem Sie die Freigaben erstellt. Wenn Sie Microsoft SQL Server verwenden, muss das SQL Server-Dienstkonto beispielsweise Vollzugriff auf die Freigabe und das Dateisystem gewährt werden.

> [!NOTE]
>  Sie müssen Mitglied der Gruppe zu aktualisieren, wenn Sie die Clusterknoten hinzufügen, es sei denn, Sie System Center Virtual Machine Manager verwenden, um Ihre Dateifreigaben zu erstellen.

Um Dateifreigaben mithilfe von PowerShell-Skripts zu erstellen, führen Sie folgende Schritte aus:

1. Laden Sie die Skripts, die in enthaltenen [SMB-Freigabe-Konfiguration für Hyper-V-Arbeitsauslastungen](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) auf einen der Knoten des dateiserverclusters.
2. Öffnen Sie eine Windows PowerShell-Sitzung mit Domänenadministrator-Anmeldeinformationen auf dem Verwaltungssystem aus, und klicken Sie dann verwenden Sie das folgende Skript erstellt eine Active Directory-Gruppe für die Hyper-V-Computer-Objekte, ändern Sie die Werte für die Variablen nach Bedarf für Ihre Umgebung:

    ```PowerShell
    # Replace the values of these variables
    $HyperVClusterName = "Compute01"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of script itself
    CD $ScriptFolder
    .\ADGroupSetup.ps1 -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName -HyperVClusterName $HyperVClusterName
    ```
3. Öffnen Sie eine Windows PowerShell-Sitzung mit Administratoranmeldeinformationen auf einem der Speicherknoten, und klicken Sie dann verwenden Sie das folgende Skript zum Erstellen von Freigaben für jede CSV und gewähren von Administratorberechtigungen für die Freigaben für Domänen-Admins und der Compute-Cluster.

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

### <a name="step-43-enable-kerberos-constrained-delegation"></a>Schritt 4.3 aktivieren Kerberos eingeschränkte Delegierung

Eingeschränkte Kerberos-Delegierung einrichten für Remoteszenario Management und erhöhte Sicherheit für den Live Migration, von einem der Clusterknoten Speicher, der KCDSetup.ps1 Skript [SMB-Freigabe-Konfiguration für Hyper-V-Arbeitsauslastungen](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a). So sieht ein wenig Wrapper für das Skript aus:

```PowerShell
$HyperVClusterName = "Compute01"
$ScaleOutFSName = "SOFS"
$ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

CD $ScriptFolder
.\KCDSetup.ps1 -HyperVClusterName $HyperVClusterName -ScaleOutFSName $ScaleOutFSName -EnableLM
```

## <a name="next-steps"></a>Nächste Schritte

Es wird empfohlen, nach der Bereitstellung Ihres Clusterdateiservers, Testen der Leistung Ihrer Lösung mit künstlichen Arbeitslasten vor der Einbindung von echten Workloads. Dadurch können Sie bestätigen, dass die Projektmappe ordnungsgemäß ausgeführt wird, und lösen Sie alle veralteten Probleme vor dem Hinzufügen der Komplexität von Workloads. Weitere Informationen finden Sie unter [Storage Spaces Leistung mithilfe von synthetischen Testworkloads](https://technet.microsoft.com/library/dn894707.aspx).

## <a name="see-also"></a>Siehe auch

-   ["Direkte Speicherplätze" unter WindowsServer 2016](storage-spaces-direct-overview.md)
-   [Verstehen des Caches in "direkte Speicherplätze"](understand-the-cache.md)
-   [Planen von Volumes im "direkte Speicherplätze"](plan-volumes.md)
-   [Fehlertoleranz bei Speicherplätzen](storage-spaces-fault-tolerance.md)
-   [Hardwareanforderungen für "direkte Speicherplätze"](Storage-Spaces-Direct-Hardware-Requirements.md)
-   [To RDMA, or not to RDMA – that is the question](https://blogs.technet.microsoft.com/filecab/2017/03/27/to-rdma-or-not-to-rdma-that-is-the-question/) (RDMA oder kein RDMA – das ist hier die Frage) (TechNet-Blog)
