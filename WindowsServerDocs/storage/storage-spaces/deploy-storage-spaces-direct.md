---
title: Bereitstellen von direkte Speicherplätze
ms.prod: windows-server-threshold
manager: eldenc
ms.author: stevenek
ms.technology: storage-spaces
ms.topic: get-started-article
ms.assetid: 20fee213-8ba5-4cd3-87a6-e77359e82bc0
author: stevenek
ms.date: 8/16/2018
description: Eine schrittweise Anleitung zum softwaredefinierten Speicher mit "direkte Speicherplätze" in Windows Server als hyperkonvergenten Infrastrukturen oder konvergente (auch bekannt als zerlegt) Infrastruktur bereitstellen.
ms.localizationpriority: medium
ms.openlocfilehash: 55cfa0e066506d7174f9e5b1e61cc0aa290706d7
ms.sourcegitcommit: 65e4f760be73104e67847f77e834e7b5e065211b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/23/2018
ms.locfileid: "5429042"
---
# Bereitstellen von direkte Speicherplätze

> Gilt für: WindowsServer 2019, WindowsServer 2016

Dieses Thema enthält eine schrittweise Anleitung zum Bereitstellen von ["Direkte Speicherplätze"](storage-spaces-direct-overview.md).

> [!Tip]
> Hyperkonvergente Infrastruktur erwerben möchten? Microsoft empfiehlt, diese Lösungen [Windows Server Software-Defined](https://microsoft.com/wssd) von unseren Partnern. Sie sind entwickelt, zusammengesetzt und überprüft mit dem unsere Referenzarchitektur, um sicherzustellen, dass Kompatibilität und Zuverlässigkeit, so Sie nach oben erhalten und schnell ausgeführt.

> [!Tip]
> Sie können Hyper-V virtuelle Computer, einschließlich in Microsoft Azure, um zu [bewerten, "direkte Speicherplätze" ohne Hardware](storage-spaces-direct-in-vm.md)verwenden. Sie sollten auch nützlich [Bereitstellungsskripts für Windows Server-schnelle Lab](https://aka.ms/wslab)zu überprüfen, die wir für Übungszwecken verwenden.

## Vorbereitung

Überprüfen Sie die ["direkte Speicherplätze" hardwareanforderungen](Storage-Spaces-Direct-Hardware-Requirements.md) und Überfliegen Sie dieses Dokuments, um sich mit den allgemeinen Ansatz kennen und wichtige Hinweise einige Schritte zugeordnete vertraut zu machen.

Erfassen Sie die folgende Informationen:

- **Bereitstellungsoption.** "Direkte Speicherplätze" unterstützt [zwei Bereitstellungsoptionen: zusammengeführte und zusammengeführten](storage-spaces-direct-overview.md#deployment-options), auch bekannt als zerlegt. Machen Sie sich mit den Vorteilen der einzelnen zu entscheiden, die für Sie geeignet ist. Schritte 1-3 unten gelten für beide Optionen zur Bereitstellung. Schritt 4 ist nur für konvergente Bereitstellung erforderlich.

- **Server-Namen.** Machen Sie sich mit Ihrer Organisation Benennungskonventionen für Computer, Dateien, Pfade und andere Ressourcen vertraut. Sie müssen mehrere Server mit eindeutige Namen bereitstellen.

- **Domänenname.** Rufen Sie die Richtlinien Ihres Unternehmens für benennungs- und Domänenbeitritte vertraut.  Sie sehen die Server zu Ihrer Domäne hinzufügen, und Sie müssen den Domänennamen angeben. 

- **RDMA-Netzwerke.** Es gibt zwei Arten von RDMA-Protokollen: iWarp und RoCE. Hinweis: was Ihre Netzwerkadapter verwenden, und wenn RoCE, beachten Sie auch die Version (v1 oder v2). Beachten Sie für RoCE außerdem das Modell des Top-des-Rack-Switches.

- **VLAN-ID.** Beachten Sie die VLAN-ID für Verwaltungsbetriebssystem Netzwerkadapter auf dem Server verwendet werden, sofern vorhanden. Diese sollten Sie von Ihrem Netzwerkadministrator erhalten.

## Schritt 1: Bereitstellen von Windows Server

### Schritt 1.1: Installation des Betriebssystems

Der erste Schritt ist Windows Server auf jedem Server zu installieren, die im Cluster werden sollen. "Direkte Speicherplätze" erfordert Windows Server 2016 Datacenter Edition. Sie können die Server Core-Installationsoption oder Server mit Desktopdarstellung verwenden.

Bei der Installation von Windows Server mithilfe des Setup-Assistenten können Sie wählen zwischen *Windows Server* (verweisen auf Server Core) und *Windows Server (Server mit Desktopdarstellung)*, die ist das Äquivalent der *vollständigen* Installationsoption? in Windows Server 2012 R2 verfügbar. Wenn Sie nicht möchten, erhalten Sie die Server Core-Installationsoption. Weitere Informationen finden Sie unter [Installation Optionen für Windows Server 2016](../../get-started/Windows-Server-2016.md).

### Schritt 1.2: Verbinden Sie mit dem Server

Diese Anleitung konzentriert sich die Server Core-Installationsoption und Remote von einem separaten Verwaltungssystem, die haben muss bereitstellen/verwalten:

- Windows Server 2016 mit den gleichen Updates als den verwalteten Servern verwaltet wird.
- Netzwerkkonnektivität mit den verwalteten Servern verwaltet wird.
- Die die gleiche Domäne oder einer vollständig vertrauenswürdigen Domäne beigetreten sind
- Remoteserver-Verwaltungstools (RSAT) und PowerShell-Module für Hyper-V und Failoverclustering. RSAT-Tools und PowerShell-Module sind auf Windows Server verfügbar und können ohne weitere Features installiert werden. Sie können auch die [Remoteserver-Verwaltungstools](https://www.microsoft.com/download/details.aspx?id=45520) auf einem Windows 10-Verwaltung PC installieren.

Installieren Sie auf dem Verwaltungssystem den Failovercluster sowie Hyper-V-Verwaltungstools. Dies kann über Server Manager mithilfe des Assistenten zum **Hinzufügen von Rollen und Features**. Wählen Sie auf der Seite **Features** die Option **Remoteserver-Verwaltungstools** und dann die zu installierenden Tools aus.

Geben Sie die PS-Sitzung ein, und verwenden Sie entweder den Servernamen oder die IP-Adresse des Knotens, mit dem Sie eine Verbindung herstellen möchten. Sie werden aufgefordert, ein Kennwort einzugeben nach dem Ausführen dieses Befehls, geben Sie das Administratorkennwort ein, die Sie beim Einrichten von Windows angegeben.

   ```PowerShell
   Enter-PSSession -ComputerName <myComputerName> -Credential LocalHost\Administrator
   ```

   Hier ist ein Beispiel hierfür dasselbe in eine Möglichkeit, die in Skripts, nützlicher ist für den Fall, dass Sie mehrere Male ausführen müssen:

   ```PowerShell
   $myServer1 = "myServer-1"
   $user = "$myServer1\Administrator"

   Enter-PSSession -ComputerName $myServer1 -Credential $user
   ```

> [!TIP]
> Wenn Sie Remote von einem Verwaltungssystem bereitstellen, erhalten Sie möglicherweise eine Fehlermeldung wie *WinRM kann die Anforderung nicht verarbeiten.* Um dieses Problem zu beheben, verwenden Sie Windows PowerShell die Liste der vertrauenswürdigen Hosts auf Ihr Verwaltungscomputer jedem Server hinzu:  
>   
> `Set-Item WSMAN:\Localhost\Client\TrustedHosts -Value Server01 -Force`
>  
> Hinweis: die Liste der vertrauenswürdigen Hosts unterstützt Platzhalter, z. B. `Server*`.
>
> Geben Sie zum Anzeigen Ihrer Liste der vertrauenswürdigen Hosts `Get-Item WSMAN:\Localhost\Client\TrustedHosts`.  
>   
> Um die Liste leer ist, geben Sie `Clear-Item WSMAN:\Localhost\Client\TrustedHost`.  

### Schritt 1.3: Der Domäne beitreten und Hinzufügen von Domänenkonten

Bisher haben Sie die einzelnen Server konfiguriert haben, mit dem lokalen Administratorkonto `<ComputerName>\Administrator`.

Um "direkte Speicherplätze" zu verwalten, müssen Sie den Server zu einer Domäne beitreten und verwenden Sie ein Active Directory Domain Services-Domänenkonto, das in der Gruppe "Administratoren" auf jedem Server ist.

Öffnen Sie aus dem Verwaltungssystem eine PowerShell-Konsole mit Administratorrechten. Verwendung `Enter-PSSession` jedem Server herstellen, und führen Sie das folgende Cmdlet ersetzen durch Ihre eigenen Computernamen, Domänennamen und Anmeldeinformationen für Domänen:

```PowerShell  
Add-Computer -NewName "Server01" -DomainName "contoso.com" -Credential "CONTOSO\User" -Restart -Force  
```

Wenn Ihr Administratorkonto Speicher nicht Mitglied der Gruppe "Domänen-Admins" ist, der lokalen Gruppe Administratoren auf jedem Knoten - hinzuzufügen Sie Ihr Administratorkonto Speicher, oder besser noch, fügen Sie die Gruppe, die Sie für Speicher-Administratoren verwenden. Sie können mithilfe des folgenden Befehls (oder Schreiben Sie eine Windows PowerShell-Funktion dazu-finden Sie weitere Informationen unter [Verwenden von PowerShell zum Domänenbenutzer zu einer lokalen Gruppe hinzufügen](http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/19/use-powershell-to-add-domain-users-to-a-local-group.aspx) ):

```
Net localgroup Administrators <Domain\Account> /add
```

### Schritt 1.4: Installieren von Rollen und features

Der nächste Schritt besteht darin Serverrollen auf jedem Server installieren. Sie können nicht mithilfe von [Windows Admin Center](../../manage/windows-admin-center/use/manage-servers.md), [Server-Manager](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)), oder PowerShell. Hier sind die Rollen zu installieren:

- Failoverclustering
- Hyper-V
- Dateiserver (Wenn Sie alle Dateifreigaben, z. B. für eine konvergente Bereitstellung hosten möchten)
- Daten-Center-Bridging (Wenn Sie RoCEv2 anstelle von iWARP Netzwerkadaptern verwenden)
- RSAT-Clustering-PowerShell
- Hyper-V-PowerShell

Verwenden Sie zur Installation über PowerShell das Cmdlet [Install-WindowsFeature](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature) . Sie können es auf einem einzelnen Server wie folgt aus:

```PowerShell
Install-WindowsFeature -Name "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"
```

Führen Sie den Befehl auf allen Servern im Cluster gleichzeitig mit minimalem Skript, ändern die Liste der Variablen am Anfang des Skripts für Ihre Umgebung anzupassen.

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"
$FeatureList = "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"

# This part runs the Install-WindowsFeature cmdlet on all servers in $ServerList, passing the list of features into the scriptblock with the "Using" scope modifier so you don't have to hard-code them here.
Invoke-Command ($ServerList) {
    Install-WindowsFeature -Name $Using:Featurelist
}
```

## Schritt 2: Konfigurieren des Netzwerks

Wenn Sie "direkte Speicherplätze" innerhalb von virtuellen Computern bereitstellen, überspringen Sie diesen Abschnitt.

"Direkte Speicherplätze" ist mit hoher Bandbreite, geringer Latenz zwischen den Servern im Cluster networking erforderlich. Mindestens 10 GbE-Networking ist erforderlich und remote direct Memory Access (RDMA) wird empfohlen. Sie können entweder iWARP oder RoCE verwenden, solange er verfügt über das Windows Server 2016-Logo, aber iWARP ist in der Regel einfacher einzurichten.

> [!Important]
> Je nach Ihrer Netzwerkgeräte und insbesondere bei RoCE v2 kann eine Konfiguration des Top-des-Rack-Switches erforderlich sein. Richtige Switch-Konfiguration ist wichtig, Zuverlässigkeit und Leistung von "direkte Speicherplätze" zu gewährleisten.

Windows Server 2016 führt Switch embedded teaming (SET) innerhalb der Hyper-V virtual Switch. Dadurch können die gleichen physischen NIC-Ports für den Netzwerkdatenverkehr verwendet werden, bei der Verwendung von RDMA, reduziert die Anzahl der physischen NIC-Ports erforderlich sind. Switch embedded teaming empfiehlt für "direkte Speicherplätze".

Eine Anleitung zum Einrichten von Netzwerkfunktionen für "direkte Speicherplätze" finden Sie unter [Windows Server 2016 zusammengeführten NIC und Gast RDMA-Bereitstellungshandbuch](https://github.com/Microsoft/SDN/blob/master/Diagnostics/S2D%20WS2016_ConvergedNIC_Configuration.docx).

## Schritt 3: Konfigurieren von „Direkte Speicherplätze“

Die folgenden Schritte werden auf einem Verwaltungssystem durchgeführt, das über die gleiche Version wie die zu konfigurierenden Server verfügt. Die folgenden Schritte sollten nicht remote mit einer PowerShell-Sitzung ausgeführt, sondern stattdessen in einer lokalen PowerShell-Sitzung auf dem Verwaltungssystem mit Administratorberechtigungen ausgeführt.

### Schritt 3.1: Bereinigen von Laufwerken

Bevor Sie "direkte Speicherplätze" aktivieren, müssen Sie sicherstellen Ihrer Laufwerke sind leer: keine alten Partitionen oder andere Daten entfernt. Führen Sie das folgende Skript, ersetzen die Computernamen, um alle alten Partitionen oder andere Daten zu entfernen.

> [!Warning]
> Dieses Skript entfernt alle Daten auf Laufwerken, die als das Betriebssystemlaufwerk Start dauerhaft!

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

Die Ausgabe sieht wie folgt, aus, in denen **Anzahl** der Anzahl der Laufwerke jedes Modell in jedem Server ist:

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

### Schritt 3.2: Überprüfen Sie den cluster

In diesem Schritt führen Sie das clustervalidierungstool aus, um sicherzustellen, dass die Serverknoten ordnungsgemäß konfiguriert sind, um einen Cluster mit "direkte Speicherplätze" erstellen. Wenn cluster-Überprüfung (`Test-Cluster`) wird vor der Erstellung des Clusters ausgeführt, es führt die Tests, die Stellen Sie sicher, dass die Konfiguration für eine erfolgreiche als Failovercluster geeignet ist. Im Beispiel unten wird direkt der `-Include` Parameter, und klicken Sie dann die einzelnen Testkategorien angegeben. Dadurch wird sichergestellt, dass die für „Direkte Speicherplätze“ spezifischen Tests in der Validierung enthalten sind.

Verwenden Sie den folgenden PowerShell-Befehl, um eine Gruppe von Servern zu überprüfen, die als Cluster für „Direkte Speicherplätze“ verwendet werden soll.

```PowerShell
Test-Cluster –Node <MachineName1, MachineName2, MachineName3, MachineName4> –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
```

### Schritt 3.3: Erstellen des Clusters

In diesem Schritt erstellen Sie einen Cluster mit Knoten, die Sie für die Erstellung des Clusters im vorherigen Schritt mit dem folgenden PowerShell-Cmdlet überprüft haben.

Beim Erstellen des Clusters erhalten Sie eine Warnung, die besagt: "Es wurden Probleme beim Erstellen der Clusterrolle, die es verhindern kann. Weitere Informationen finden Sie in der folgenden Berichtsdatei.“ Sie können diese Warnung ignorieren. Die Ursache dieser Warnung liegt darin, dass keine Datenträger für das Clusterquorum verfügbar sind. Es wird empfohlen, nach der Erstellung des Clusters einen Dateifreigabe- oder Cloudzeugen zu konfigurieren.

> [!Note]
> Wenn die Server statische IP-Adressen verwenden, ändern Sie den folgenden Befehl so, dass die statische IP-Adresse reflektiert wird. Fügen Sie dazu den folgenden Parameter hinzu, und geben Sie die IP-Adresse an: „–StaticAddress &lt;X.X.X.X&gt;“.
> Im folgenden Befehl sollte der Platzhalter „ClusterName“ durch einen eindeutigen, aus maximal 15 Zeichen bestehenden NetBIOS-Namen ersetzt werden.
> ```PowerShell
> New-Cluster –Name <ClusterName> –Node <MachineName1,MachineName2,MachineName3,MachineName4> –NoStorage
> ```

Nach der Erstellung des Clusters kann es einige Zeit dauern, bis der DNS-Eintrag für den Clusternamen repliziert wurde. Wie lange, hängt von der Umgebung und der Konfiguration der DNS-Replikation ab. Wird der Cluster nicht erfolgreich aufgelöst, können Sie den Vorgang in den meisten Fällen erfolgreich ausführen, indem Sie anstelle des Clusternamens den Computernamen eines Knotens verwenden, der ein aktives Mitglied des Clusters ist.

### Schritt 3.4: Konfigurieren eines clusterzeugen

Es wird empfohlen, dass Sie so konfigurieren, einen Zeugen für den Cluster, Cluster mit drei oder mehr Servern zwei Servern oder das widerstehen können. Eine Bereitstellung von zwei Servern erfordert einen clusterzeugen, andernfalls entweder Server offline zu gehen bewirkt, dass der andere ebenfalls nicht mehr verfügbar sind. Bei diesen Systemen können Sie eine Dateifreigabe als Zeugen bzw. Cloudzeugen verwenden. 

Weitere Informationen finden Sie unter den folgenden Themen:

- [Konfigurieren und Verwalten des Quorums](../../failover-clustering/manage-cluster-quorum.md)
- [Bereitstellen eines Cloudzeugen für einen Failovercluster](../../failover-clustering/deploy-cloud-witness.md)

### Schritt 3.5: Aktivieren von „Direkte Speicherplätze“

Verwenden Sie nach der Erstellung des Clusters, den `Enable-ClusterStorageSpacesDirect` PowerShell-Cmdlet, der das Speichersystem in den "direkte Speicherplätze"-Modus versetzt, und führen Sie die folgenden automatisch:

-   **Erstellen eines Pools:** Erstellt einen einzelnen großen Pool mit einem Namen wie z.B. „S2D auf Cluster1“.

-   **Konfigurieren der Caches von „Direkte Speicherplätze“** Falls mehr als ein Medientyp bzw. Laufwerkstyp für die Verwendung von „Direkte Speicherplätze“ verfügbar ist, werden die schnellsten Typen als Cachegeräte aktiviert (in den meisten Fällen wird von diesen gelesen und auf diese geschrieben)

-   **Ebenen:** Erstellt zwei Ebenen als Standardebenen. Eine mit der Bezeichnung „Kapazität“, die andere mit der Bezeichnung „Leistung“. Das Cmdlet analysiert die Geräte und konfiguriert jede Ebene mit der Kombination aus Gerätetypen und Ausfallsicherheit (Resilienz).

Starten Sie aus dem Verwaltungssystem heraus den folgenden Befehl in einem PowerShell-Befehlsfenster, das mit Administratorrechten geöffnet wurde. Der Clustername ist der Name des Clusters, den Sie in den vorherigen Schritten erstellt haben. Wenn dieser Befehl lokal auf einem der Knoten ausgeführt wird, ist der Parameter -CimSession nicht erforderlich.

```PowerShell
Enable-ClusterStorageSpacesDirect –CimSession <ClusterName>
```

Um „Direkte Speicherplätze“ mit dem oben stehenden Befehl zu aktivieren, können Sie auch den Knotennamen anstelle des Clusternamens verwenden. Die Verwendung des Knotennamens ist unter Umständen zuverlässiger, da bei einem neu erstellten Clusternamen Verzögerungen bei der DNS-Replikation auftreten können.

Wenn die Ausführung des Befehls beendet ist, was einige Minuten dauern kann, ist das System bereit für die Erstellung von Volumes.

### Schritt 3.6: Erstellen von Volumes

Wir empfehlen die Verwendung der `New-Volume` Cmdlet wie sie bietet die schnellste und einfachste Methode dafür. Dieses einzelne Cmdlet erstellt, partitioniert und formatiert automatisch den virtuellen Datenträger, erstellt das Volume mit demselben Namen und fügt es freigegebenen Clustervolumes hinzu – alles in einem einfachen Schritt.

Weitere Informationen finden Sie unter [Erstellen von Volumes in Direkte Speicherplätze](create-volumes.md).

### Schritt 3.7: Optional den CSV-Cache aktivieren

Sie können optional den freigegebenen Clustervolume (CSV) Cache Systemarbeitsspeicher (RAM) als Schreib-through auf Blockebene Cache der Lesevorgänge verwenden, die von der Windows-Cache-Manager bereits zwischengespeichert werden nicht aktivieren. Dies kann die Leistung für Anwendungen wie Hyper-V verbessern. Die CSV-Cache kann die Leistung von Lesevorgängen steigern und ist auch hilfreich für Dateiserver mit horizontaler Skalierung Szenarien.

Aktivieren des CSV-Caches reduziert die Größe des Arbeitsspeichers für VMs in einem hyperkonvergenten Cluster ausführen, daher Sie speicherleistung mit verfügbare Arbeitsspeicher für virtuelle Festplatten Saldo müssen verfügbar.

Zum Festlegen der Größe des Caches CSV-öffnen Sie eine PowerShell-Sitzung auf dem Verwaltungssystem mit einem Konto, das über Administratorrechte auf dem speichercluster verfügt, und verwenden Sie dieses Skript, Ändern der `$ClusterName` und `$CSVCacheSize` Variablen nach Bedarf (in diesem Beispiel wird ein 2 GB CSV-Cache pro Server):

```PowerShell
$ClusterName = "StorageSpacesDirect1"
$CSVCacheSize = 2048 #Size in MB

Write-Output "Setting the CSV cache..."
(Get-Cluster $ClusterName).BlockCacheSize = $CSVCacheSize

$CSVCurrentCacheSize = (Get-Cluster $ClusterName).BlockCacheSize
Write-Output "$ClusterName CSV cache size: $CSVCurrentCacheSize MB"
```

Weitere Informationen finden Sie unter [Verwendung der CSV-speicherinterne Lesecache](csv-cache.md).

### Schritt 3.8: Bereitstellung virtueller Computer für zusammengeführte Bereitstellungen

Wenn Sie einen hyperkonvergenten Cluster bereitstellen, ist der letzte Schritt virtuellen Computern auf den "direkte Speicherplätze" Cluster bereitstellen.

Die Dateien des virtuellen Computers sollten im CSV-Namespace des Systems gespeichert werden (Beispiel: „c:\\ClusterStorage\\Volume1“), genau wie gruppierte virtuelle Computer in Failoverclustern.

Sie können mitgelieferte Tools oder andere Tools zum Verwalten der Speicher und virtuellen Computern, z. B. System Center Virtual Machine Manager verwenden.

## Schritt 4: Bereitstellen von Dateiserver mit horizontaler Skalierung für konvergente solutions

Wenn Sie eine konvergente Lösung bereitstellen, werden im nächste Schritt erstellen Sie eine Instanz des Dateiservers mit horizontaler Skalierung und einige Dateifreigaben einzurichten. Wenn Sie einen hyperkonvergenten Cluster - bereitstellen, sind Sie fertig sind und nicht benötigt Abschnitt.

### Schritt 4.1: Erstellen der Rolle "Dateiserver mit horizontaler Skalierung"

Im nächsten Schritt beim Einrichten der Clusterdienste für Ihre Dateiserver ist die gruppierten Datei-Serverrolle, erstellt die ist beim Erstellen der Scale-Out File Server-Instanz auf dem Ihre ständig verfügbare Dateifreigaben gehostet werden.

#### So erstellen Sie eine Rolle "Dateiserver mit horizontaler Skalierung" mit Server-Manager

1.  Wählen Sie im Failovercluster-Manager den Cluster, wechseln Sie zu **Rollen**und klicken Sie dann auf **Rolle konfigurieren**.<br>Der Assistent für hohe Verfügbarkeit angezeigt wird.
2.  Klicken Sie auf der Seite " **Select Role** " auf **Dateiserver**.
3.  Klicken Sie auf der Seite " **Server Dateityp** " **Dateiserver mit horizontaler Skalierung für Anwendungsdaten**aus.
4.  Geben Sie auf der Seite " **Clientzugriffspunkt** " einen Namen für den Dateiserver mit horizontaler Skalierung.
5.  Stellen Sie sicher, dass die Rolle "erfolgreich durch das Aufrufen **von Rollen** eingerichtet und bestätigt haben wurde, dass der Spalte" **Status** " **ausgeführt** neben der gruppierten Datei-Serverrolle zeigt Sie erstellt haben, wie in Abbildung 1 dargestellt.

    ![Screenshot des Failovercluster-Manager mit dem Dateiserver mit horizontaler Skalierung](media\Hyper-converged-solution-using-Storage-Spaces-Direct-in-Windows-Server-2016\SOFS_in_FCM.png "Failover Cluster Manager showing the Scale-Out File Server")

     **Abbildung 1** Failovercluster-Manager mit dem Dateiserver mit horizontaler Skalierung mit der Ausführung status

> [!NOTE]
>  Nach dem Erstellen der Clusterrolle, gibt es möglicherweise einige Netzwerk Verbreitung Verzögerungen, die Sie vor der Erstellung von Dateifreigaben von es ein paar Minuten oder potenziell länger verhindern könnten.  
  
#### So erstellen Sie eine Rolle "Dateiserver mit horizontaler Skalierung" mithilfe von Windows PowerShell

 In einer Windows PowerShell-Sitzung, die mit dem Dateiservercluster verbunden ist, geben Sie die folgenden Befehle zum Erstellen der Rolle "Dateiserver mit horizontaler Skalierung", ändern *FSCLUSTER* entsprechend den Namen des Clusters und *sofs kontaktieren* mit dem Namen übereinstimmen, erhalten soll die Rolle "Dateiserver mit horizontaler Skalierung":

```PowerShell
Add-ClusterScaleOutFileServerRole -Name SOFS -Cluster FSCLUSTER
```

> [!NOTE]
>  Nach dem Erstellen der Clusterrolle, gibt es möglicherweise einige Netzwerk Verbreitung Verzögerungen, die Sie vor der Erstellung von Dateifreigaben von es ein paar Minuten oder potenziell länger verhindern könnten. Wenn die Rolle "sofs kontaktieren" sofort fehlschlägt und startet nicht, kann es sein, da die Cluster-Computerobjekt über die Berechtigung zum Erstellen eines Computerkontos für die Rolle "sofs kontaktieren" besitzt. Hilfe, finden Sie unter diesem Blogbeitrag: [Scale-Out-Datei Server Rolle fehlschlägt To Start With Ereignis IDs 1205 1069, und 1194](http://www.aidanfinn.com/?p=14142).

### Schritt 4.2: Erstellen von Dateifreigaben

Nachdem Sie Ihren virtuellen Datenträgern erstellt und zu freigegebenen Clustervolumes hinzugefügt haben, ist es Zeit zur Erstellung von Dateifreigaben auf – eine Dateifreigabe pro CSV pro virtuellen Datenträger. System Center Virtual Machine Manager (VMM) ist wahrscheinlich die handiest Möglichkeit, dies tun, da es die Berechtigungen für Sie behandelt, aber wenn Sie in Ihrer Umgebung nicht darüber verfügen, können Sie mithilfe von Windows PowerShell um die Bereitstellung teilweise zu automatisieren.

Verwenden Sie die Skripts in die [SMB-Freigabe für Hyper-V-Workloads](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) Konfigurationsskript, das teilweise den Prozess zum Erstellen von Gruppen und Freigaben automatisiert enthalten. Bezieht sich für Hyper-V-Workloads, wenn Sie andere Workloads bereitstellen, müssen Sie möglicherweise die Einstellungen zu ändern oder zusätzliche Schritte ausführen, nachdem Sie die Freigaben erstellt. Wenn Sie Microsoft SQL Server verwenden, muss der SQL Server-Dienstkontos z. B. Vollzugriff auf die Freigabe und das Dateisystem erteilt werden.

> [!NOTE]
>  Sie müssen allerdings noch die Gruppenmitgliedschaft zu aktualisieren, wenn Sie Knoten im Cluster hinzufügen, es sei denn, Sie System Center Virtual Machine Manager verwenden, um Ihre Freigaben erstellen.

Um Dateifreigaben mithilfe von PowerShell-Skripts erstellen, gehen Sie wie folgt:

1. Herunterladen der in einem der Knoten des Datei-Server-Clusters [SMB-Freigabe Konfiguration für Hyper-V-Workloads](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) enthaltene Skripts.
2. Öffnen Sie eine Windows PowerShell-Sitzung mit Domänenadministrator-Anmeldeinformationen auf dem Verwaltungssystem, und verwenden Sie das folgende Skript zum Erstellen einer Active Directory-Gruppe für die Hyper-V-Computer-Objekte, die Werte für die Variablen entsprechend ändern Ihrer Umgebung:

    ```PowerShell
    # Replace the values of these variables
    $HyperVClusterName = "Compute01"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of script itself
    CD $ScriptFolder
    .\ADGroupSetup.ps1 -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName -HyperVClusterName $HyperVClusterName
    ```
3. Öffnen Sie eine Windows PowerShell-Sitzung mit Administratorrechten auf einen der Speicherknoten, und verwenden Sie das folgende Skript zum Erstellen von Freigaben für jeden CSV und gewähren von Administratorberechtigungen für die Freigaben für Domänen-Admins und Compute-Cluster.

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

### Eingeschränkte Schritt 4.3 aktivieren Kerberos-Delegierung

Verwenden Sie zum Einrichten von eingeschränkte Kerberos-Delegierung für remote-Szenario Verwaltungs- und erhöhte Livemigration Sicherheit von einem Clusterknoten Speicher das KCDSetup.ps1 Skript in [SMB-Freigabe Konfiguration für Hyper-V-Workloads](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)enthalten. Hier ist ein wenig Wrapper für das Skript aus:

```PowerShell
$HyperVClusterName = "Compute01"
$ScaleOutFSName = "SOFS"
$ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

CD $ScriptFolder
.\KCDSetup.ps1 -HyperVClusterName $HyperVClusterName -ScaleOutFSName $ScaleOutFSName -EnableLM
```

## Nächste Schritte

Es wird empfohlen, nach der Bereitstellung des gruppierten Dateiservers, testen die Leistung Ihrer Lösung mit synthetische Workloads vor allen reale Workloads aufrufen. Auf diese Weise können Sie bestätigen, dass die Lösung ordnungsgemäß ausgeführt wird und nach außen veralteten Probleme vor dem Hinzufügen der Komplexität von Workloads. Weitere Informationen finden Sie unter [Test Leerzeichen Leistung mithilfe von synthetischen Speicherworkloads](https://technet.microsoft.com/library/dn894707.aspx).

## Weitere Informationen:

-   [Direkte Speicherplätze in Windows Server 2016](storage-spaces-direct-overview.md)
-   [Grundlegendes zum Cache in Direkte Speicherplätze](understand-the-cache.md)
-   [Planen von Volumes in Direkte Speicherplätze](plan-volumes.md)
-   [Fehlertoleranz bei Speicherplätzen](storage-spaces-fault-tolerance.md)
-   [Hardwareanforderungen für „Direkte Speicherplätze“](Storage-Spaces-Direct-Hardware-Requirements.md)
-   [To RDMA, or not to RDMA – that is the question](https://blogs.technet.microsoft.com/filecab/2017/03/27/to-rdma-or-not-to-rdma-that-is-the-question/) (RDMA oder kein RDMA – das ist hier die Frage) (TechNet-Blog)
