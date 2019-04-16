---
title: Verwenden von freigegebenen Cluster-Volumes in einem Failovercluster
description: Informationen zum Cluster Shared Volumes in einem Failovercluster verwenden.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f5bd0ad05bdc2573a5ea0abbe165de2d3e7f5c8f
ms.sourcegitcommit: 375e94dc70c76e7aa5679c32f0f4dbc26cf7dd83
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2018
ms.locfileid: "2233516"
---
# <a name="use-cluster-shared-volumes-in-a-failover-cluster"></a>Verwenden von freigegebenen Cluster-Volumes in einem Failovercluster

>Betrifft: Windows Server 2012 R2, WindowsServer 2012 und WindowsServer 2016

Cluster Shared Volumes (CSV) können mehrere Knoten in einem Failovercluster gleichzeitig Lese-/ Schreibzugriff auf die gleiche LUN (Festplatte) zugreifen, die als NTFS-Volumes bereitgestellt wird. (In Windows Server 2012 R2, kann der Datenträger als NTFS oder ausfallsichere File System (ReFS) bereitgestellt werden.) Mit CSV können gruppierte Rollen schnell von einem Knoten auf einen anderen Knoten Failover ohne eine Änderung des Besitzes mit Laufwerk, oder Aufheben der Bereitstellung und erneutes Bereitstellen ein Volume. CSV auch vereinfachen die Verwaltung von eine möglicherweise große Anzahl von LUNs in einem Failovercluster.

CSV bieten eine allgemeine, gruppierte Dateisystem, das über NTFS (oder in Windows Server 2012 R2 ReFS) installiert ist. CSV-Anwendungen umfassen:

- Clustered-Dateien für virtuelle Computer für gruppierte Hyper-V virtual Hard Disk (VHD)
- Horizontale Skalierung Dateifreigaben zum Speichern von Anwendungsdaten für die horizontale Skalierung Datei gruppierte Serverrolle. Beispiele für die Anwendungsdaten für diese Rolle sind Hyper-V virtueller Computerdateien und Microsoft SQL Server-Daten. (Beachten Sie, dass ReFS wird für einen Dateiserver Dezentrales Skalieren nicht unterstützt.) Weitere Informationen zu horizontal skalierten Dateiserver finden Sie unter [Dateiserver für Anwendungsdaten Dezentrales Skalieren](sofs-overview.md).

>[!NOTE]
>CSV unterstützt nicht die Microsoft SQL Server gruppierte Arbeitslast in SQL Server 2012 und früheren Versionen von SQL Server.

CSV-Funktionalität wurde in Windows Server 2012 erheblich verbessert. Beispielsweise wurden Abhängigkeiten von Active Directory-Domänendienste entfernt. Unterstützung wurde für die funktionalen Verbesserungen in **Chkdsk**, für die Interoperabilität mit antivirus und Sicherung und für die Integration mit Features wie Volumes BitLocker verschlüsselt und Speicherplätze Allgemeiner Speicher hinzugefügt. Eine Übersicht über CSV-Funktionen, die in Windows Server 2012 eingeführt wurde, finden Sie unter [Was ist neu in der Failover-Clusterunterstützung in Windows Server 2012 \[redirected\]](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)>).

Einführung in Windows Server 2012 R2 zusätzliche Funktionen, beispielsweise verteilte CSV Besitz, höhere Flexibilität durch die Verfügbarkeit des Server-Dienstes, größere Flexibilität in Höhe von physischen Arbeitsspeichers, die CSV-Cache, besser zugeordnet werden können Diagnosibility und verbesserte Interoperabilität, die Unterstützung für ReFS und Deduplizierung enthält. Weitere Informationen finden Sie unter [What's New in der Failover-Clusterunterstützung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)>).

>[!NOTE]
>Informationen zur Verwendung von Datendeduplizierung auf CSV für Virtual Desktop Infrastructure (VDI) Szenarien sehen Sie sich die Blogbeiträge [Bereitstellen von Daten für VDI-Speicher in Windows Server 2012 R2 Deduplizierung](https://blogs.technet.com/b/filecab/archive/2013/07/31/deploying-data-deduplication-for-vdi-storage-in-windows-server-2012-r2.aspx) und [Extending Datendeduplizierung auf neue Arbeitslasten in Windows Server 2012 R2](https://blogs.technet.com/b/filecab/archive/2013/07/31/extending-data-deduplication-to-new-workloads-in-windows-server-2012-r2.aspx).

## <a name="review-requirements-and-considerations-for-using-csv-in-a-failover-cluster"></a>Überprüfen und-Überlegungen für die Verwendung von CSV in einem Failovercluster

Überprüfen Sie vor der Nutzung CSV in einem Failovercluster, im Netzwerk, Speicherung und anderen Anforderungen und Aspekte in diesem Abschnitt.

### <a name="network-configuration-considerations"></a>Überlegungen zum Netzwerk-Konfiguration

Berücksichtigen Sie Folgendes, wenn Sie die Netzwerke konfigurieren, die CSV unterstützen.

- **Mehrere Netzwerke und mehrere Netzwerkadapter**. Um die Fehlertoleranz Ausfall des Netzwerks aktivieren, wird empfohlen, mehrere Cluster-Netzwerken CSV-Traffic führen oder, Konfigurieren von Netzwerkadaptern gearbeitet.
    
    Wenn die Knoten im Cluster mit Netzwerken verbunden sind, die nicht vom Cluster verwendet werden soll, sollten Sie sie deaktivieren. Beispielsweise wird empfohlen, dass Sie iSCSI-Netzwerke für die Verwendung im Cluster CSV-Datenverkehr in diesen Netzwerken verhindert deaktivieren. Zum Deaktivieren von einem Netzwerk, im Failovercluster-Manager, wählen Sie **Netzwerke**, wählen Sie das Netzwerk, wählen Sie die **Eigenschaften** -Aktion und wählen Sie dann auf **Cluster-Netzwerkkommunikation auf diesem Netzwerk nicht zulassen**. Alternativ können Sie mithilfe des Windows PowerShell-Cmdlets [Get-Clusternetzwerk](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternetwork?view=win10-ps) die **Role** -Eigenschaft des Netzwerks konfigurieren.
- **Eigenschaften von Netzwerkadapter**. Stellen Sie in den Eigenschaften für alle Netzwerkadapter, die Clusterkommunikation ausführen sicher, dass die folgenden Einstellungen aktiviert sind:

  - **Client für Microsoft-Netzwerke** und **Datei- und Druckerfreigabe für Microsoft-Netzwerke**. Diese Einstellungen unterstützen SMB Server Message Block () 3.0, das standardmäßig verwendet wird, CSV-Verkehr zwischen Knoten auszuführen. Um SMB zu aktivieren, stellen Sie außerdem sicher, dass der Server-Dienst und der Workstation-Dienst ausgeführt werden und dass sie auf jedem Clusterknoten automatischen Start konfiguriert sind.

    >[!NOTE]
    >In Windows Server 2012 R2 sind mehrere Server Service-Instanzen pro Knoten des Failoverclusters. Es gibt die Standardinstanz, die die eingehenden Datenverkehr von SMB-Clients behandelt, die reguläre Dateifreigaben zugreifen und eine zweite CSV-Instanz, die nur die Kommunikation zwischen Knoten CSV-Datenverkehr behandelt. Auch wenn der Server-Dienst auf einem Knoten fehlerhaft ist, wechselt CSV Gesamtbetriebskosten automatisch auf einen anderen Knoten.

    SMB 3.0 enthält die SMB Multichannel und direkte SMB-Features, die CSV-Traffic in Stream-Objekt über mehrere Netzwerke im Cluster und Netzwerkadapter nutzen, die unterstützen (RDMA, Remote Direct Memory Access) zu aktivieren. Standardmäßig wird SMB Multichannel für CSV-Datenverkehr verwendet. Weitere Informationen finden Sie unter [Übersicht über die Server Message Block](../storage/file-server/file-server-smb-overview.md).
  - **Microsoft-Failovercluster virtuellen Adapter Leistung Filter**. Diese Einstellung wird die Fähigkeit von Knoten e/a-Umleitung ausführen, wenn es erforderlich ist, CSV, beispielsweise erreichen, wenn ein Fehler Connectivity verhindert, dass einen Knoten eine Verbindung herstellen, direkt auf den Datenträger CSV verbessert. Weitere Informationen finden Sie weiter unten in diesem Thema [zu e/a-Synchronisierung und e/a-Umleitung in CSV-Kommunikation](#about-i/o-synchronization-and-i/o-redirection-in-csv-communication) .
- **Cluster-Netzwerk Priorisierung**. Im Allgemeinen wird empfohlen, dass die Cluster konfiguriert Einstellungen für die Netzwerke nicht zu ändern.
- **Konfiguration der IP-Subnetz**. Es ist keine bestimmte Subnetzkonfiguration erforderlich für Knoten in einem Netzwerk, die CSV verwenden. CSV kann multisubnet Cluster unterstützen.
- **Richtlinienbasierte Dienstqualität (QoS)**. Es wird empfohlen, dass Sie eine QoS-Richtlinie Priorität und eine Mindestbandbreite Richtlinie für den Netzwerkverkehr zu jedem Knoten konfigurieren, bei der Verwendung von CSV. Weitere Informationen finden Sie unter [Quality of Service (QoS)](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831679(v%3dws.11)>).
- **Speichernetzwerk**. Speicher Netzwerk Empfehlungen überprüfen Sie die Richtlinien, die von Ihrem Speicheranbieter bereitgestellt werden. Zusätzliche Überlegungen zur Speicherung für CSV finden Sie unter [Storage and Datenträger konfigurationsanforderungen](#storage-and-disk-configuration-requirements) weiter unten in diesem Thema.

Eine Übersicht über die Hardware Netzwerk und speicheranforderungen für Failoverclustern finden Sie unter [Failover Clustering Hardwareanforderungen und Speicheroptionen](clustering-requirements.md).

#### <a name="about-io-synchronization-and-io-redirection-in-csv-communication"></a>Informationen zu e/a-Synchronisierung und e/a-Umleitung in CSV-Kommunikation

- **E/a-Synchronisierung**: CSV mehrere Knoten gleichzeitige Lese-/ Schreibzugriff auf demselben freigegebenen Speicher zugreifen kann. Wenn ein Knoten Datenträger Eingabe/Ausgabe (e/a) auf einem Datenträger CSV ausführt, der Knoten kommuniziert direkt mit der Speicherung, beispielsweise über eine Storage Area Network (SAN). Jedoch "zu einem beliebigen Zeitpunkt ein einzelner Knoten (den Knoten Coordinator genannt)" die physischen Datenträgerressource gehört, die die LUN zugeordnet ist. Der Knoten Koordinator für ein Volume CSV wird als **Besitzerknoten** unter **Datenträger**im Failovercluster-Manager angezeigt. Es wird auch in der Ausgabe des [Get-ClusterSharedVolume](https://docs.microsoft.com/powershell/module/failoverclusters/get-clustersharedvolume?view=win10-ps) Windows PowerShell-Cmdlets angezeigt.

  >[!NOTE]
  >In Windows Server 2012 R2 wird die CSV-Besitz über die Failover-Clusterknoten basierend auf der Anzahl der CSV-Volumes, die Eigentümer von jedem Knoten gleichmäßig verteilt. Darüber hinaus wird den Besitz automatisch ausgeführt, bei der es gibt Situationen wie CSV-Failover, ein Knoten wird den Cluster wieder aufgenommen, Sie einen neuen Knoten mit dem Cluster hinzufügen, Sie neu starten, einen Clusterknoten oder Failovercluster zu starten, nachdem er heruntergefahren.

  Beim Auftreten bestimmter geringfügige Änderungen im Dateisystem auf einem Datenträger CSV, muss diese Metadaten auf den einzelnen physischen Knoten synchronisiert werden, die die LUN, nicht nur auf den einzelnen Coordinator Knoten zugreifen. Beispielsweise wenn ein virtuellen Computer auf einem Datenträger CSV gestartet, erstellt oder gelöscht wird, oder ein virtuellen Computer migriert werden, diese Informationen auf den einzelnen physischen Knoten synchronisiert werden soll, die auf dem virtuellen Computer zugreifen. Diese Metadaten Aktualisierungsvorgänge auftreten parallel in der Clusternetzwerken mithilfe von SMB 3.0. Diese Vorgänge erfordern keinen die physikalischen Knoten mit dem freigegebenen Speicher kommunizieren.

- **E/a-Umleitung**: Verbindungsfehler Speicher und bestimmte Speichervorgänge können verhindern, einen angegebenen Knoten kommunizieren direkt mit den Speicher. Um Funktion beizubehalten, während der Knoten nicht mit den Speicher kommuniziert, leitet der Knoten den Datenträger-e/a über ein Cluster-Netzwerk an den Koordinator-Knoten, auf dem Datenträger derzeit bereitgestellt ist. Wenn der aktuelle Coordinator Knoten ein Speicher Connectivity-Fehler auftritt, werden alle Datenträger-e/a-Vorgänge in der Warteschlange vorübergehend, während Sie ein neuer Knoten als Knoten Coordinator hergestellt wird.

Der Server hat einen der folgenden e/a-Umleitung Modi, je nach der Situation:

- **Datei System-Umleitung** Umleitung pro Volume ist – beispielsweise wenn CSV Momentaufnahmen werden übernommen, durch eine backup-Anwendung Wenn ein Volume CSV manuell in umgeleitete e/a-Modus befindet.
- **Umleitung blockieren** Umleitung wird auf der Ebene der Datei-Block – beispielsweise wenn Speicher Verbindung ist auf einen Datenträger verloren. Block Umleitung ist wesentlich schneller als Datei System Umleitung.

In Windows Server 2012 R2 können Sie den Status eines Volumes CSV auf pro Knoten anzeigen. Beispielsweise können Sie sehen, ob e/a direkte oder umgeleitete ist, oder gibt an, ob der CSV-Datenträger nicht verfügbar ist. Wenn ein Volume CSV in umgeleitete e/a-Modus befindet, können Sie auch den Grund anzeigen. Verwenden Sie das Windows PowerShell-Cmdlet **Get-ClusterSharedVolumeState** , um diese Informationen anzuzeigen.

>[!NOTE]
> * In Windows Server 2012 aufgrund von Verbesserungen bei der CSV-Design CSV weitere Vorgänge ausführen im Modus für direkte e/a als Fehler in Windows Server 2008 R2.
> * Aufgrund der Integration von CSV mit SMB 3.0 Features wie beispielsweise SMB Multichannel und direkte SMB kann umgeleitete e/a-Datenverkehr über mehrere Clusternetzwerke stream.
> * Planen Sie Ihre Cluster-Netzwerken für den potenziellen Anstieg Netzwerkdatenverkehr auf den Knoten Coordinator während des e/a-Umleitung zu ermöglichen.

### <a name="storage-and-disk-configuration-requirements"></a>Speicher- und Datenträger konfigurationsanforderungen

Um CSV verwenden, müssen Ihre Speicher- und Datenträger die folgenden Anforderungen erfüllen:

- **System-Dateiformat**. In Windows Server 2012 R2 muss ein Leerzeichen Datenträger oder Speicherung für eine CSV-Volume eines Basisdatenträgers, das mit NTFS und ReFS partitioniert werden. In Windows Server 2012 muss ein Leerzeichen Datenträger oder Speicherung für eine CSV-Volume eines Basisdatenträgers, das mit NTFS partitioniert werden.

  Eine CSV-Datei hat die folgenden zusätzlichen Anforderungen:
    
  - In Windows Server 2012 R2 keinen Datenträger für eine CSV-Datei verwendet werden, die mit FAT oder FAT32 formatiert ist.
  - In Windows Server 2012 keinen Datenträger für eine CSV-Datei verwendet werden, die mit FAT, FAT32 oder ReFS formatiert ist.
  - Wenn Sie ein Speicherplatz für eine CSV-Datei verwenden möchten, können Sie ein einfaches Leerzeichen oder ein Leerzeichen Spiegelung konfigurieren. In Windows Server 2012 R2 können Sie auch ein Leerzeichen Parität konfigurieren. (In Windows Server 2012 CSV keine Parität Leerzeichen unterstützt.)
  - Eine CSV-Datei kann nicht als eine Quorumdatenträger Zeuge verwendet werden. Weitere Informationen zu den Clusterquorum finden Sie unter [Grundlegendes zu Quorum im Speicher Leerzeichen Direct](../storage/storage-spaces/understand-quorum.md).
  - Einen Datenträger als eine CSV-Datei hinzugefügt haben, wird es im Format CSVFS (für CSV-Datei (System) festgelegt. Dadurch wird der Cluster und andere Software, um die CSV-Speicher aus anderen NTFS oder ReFS Speicherung zu unterscheiden. Im Allgemeinen unterstützt CSVFS dieselbe Funktionalität wie NTFS und ReFS. Für bestimmte Features werden jedoch nicht unterstützt. Beispielsweise kann nicht in Windows Server 2012 R2 Komprimierung von CSV aktiviert werden. In Windows Server 2012 können Sie nicht die Datendeduplizierung oder Komprimierung von CSV aktivieren.
- **Ressourcentyp im Cluster**. Für ein Volume CSV müssen Sie den Ressourcentyp physischen Datenträger verwenden. Standardmäßig wird ein Datenträger oder Speicherung Leerzeichen, die Cluster-Speicher hinzugefügt wird, automatisch auf diese Weise konfiguriert.
- **Auswahl der CSV-Datenträger oder andere Datenträger im Cluster-Speicher**. Wenn Sie einen oder mehrere Datenträger für einen gruppierten virtuellen Computer auswählen, sollten Sie wie auf jedem Datenträger verwendet wird. Wenn ein Datenträger verwendet werden soll, zum Speichern von Dateien, die von Hyper-V,, wie VHD-Dateien oder Konfigurationsdateien erstellt werden, können Sie die CSV-Datenträger oder anderen verfügbaren Datenträger im Cluster-Speicher auswählen. Wenn ein Datenträger einen physischen Datenträger eingefügt wird, der direkt ist, dem virtuellen Computer (auch als einen Pass-Through-Datenträger bezeichnet) zugeordnet ist, Sie können keinen CSV-Datenträger auswählen und Sie müssen über die verfügbaren Laufwerke im Clusterspeicher auswählen.
- **Pfadname zur Identifizierung von Datenträgern**. Datenträger in CSV werden mit einem Pfadnamen identifiziert. Jeder Pfad scheint auf dem Systemlaufwerk des Knotens als nummerierte Volume unterhalb des Ordners **\\ClusterStorage** sein. Dieser Pfad ist derselbe, wenn er von einem Knoten im Cluster angezeigt. Sie können die Volumes umbenennen, falls erforderlich.

Speicheranforderungen für CSV überprüfen Sie die Richtlinien, die von Ihrem Speicheranbieter bereitgestellt werden. Zusätzlicher Speicher Planungsaspekte für CSV finden Sie weiter unten in diesem Thema [CSV in einem Failovercluster verwenden möchten](#plan-to-use-csv-in-a-failover-cluster) .

### <a name="node-requirements"></a>Knoten-Anforderungen

Um CSV verwenden, müssen die Knoten die folgenden Anforderungen erfüllen:

- **Laufwerkbuchstabe des Systemdatenträger**. Auf allen Knoten muss der Buchstabe des Laufwerks für den Systemdatenträger identisch sein.
- **Authentifizierungsprotokoll**. Das NTLM-Protokoll muss auf allen Knoten aktiviert sein. Dies ist standardmäßig aktiviert.

## <a name="plan-to-use-csv-in-a-failover-cluster"></a>CSV in einem Failovercluster verwenden möchten

In diesem Abschnitt werden Planungsaspekte und Empfehlungen für die Verwendung von CSV in einem Failovercluster unter Windows Server 2012 R2 oder Windows Server 2012.

>[!IMPORTANT]
>Fragen Sie den Speicheranbieter Empfehlungen zum Konfigurieren Ihres Geräts bestimmten Speicher für CSV. Wenn die Empfehlungen aus der Speicheranbieter von Informationen in diesem Thema unterscheiden, verwenden Sie die Empfehlungen aus der Speicheranbieter.

### <a name="arrangement-of-luns-volumes-and-vhd-files"></a>Anordnung von LUNs, Volumes und VHD-Dateien

So machen Sie die Nutzung des CSV Speicher für gruppierte virtuelle Computer bereitstellen, ist es hilfreich, überprüfen, wie Sie die LUNs (Datenträger) beim Konfigurieren von physischer Servers anordnen würde. Wenn Sie die entsprechenden virtuellen Computer konfigurieren, versuchen Sie, VHD-Dateien auf ähnliche Weise anordnen.

Berücksichtigen Sie eines physischen Servers für das Sie die Datenträger und Dateien wie folgt organisieren würde:

- Systemdateien, einschließlich einer Auslagerungsdatei auf einem physischen Datenträger
- Datendateien auf einem anderen physischen Datenträger

Für eine entsprechende gruppierten virtuellen Computer sollten Sie die Volumes und Dateien auf ähnliche Weise organisieren:

- Systemdateien, einschließlich einer Seitendatei in eine VHD-Datei in eine CSV-
- Datendateien in einer VHD-Datei auf einem anderen CSV

Wenn Sie einen weiteren virtuellen Computer, sofern möglich hinzufügen, sollten Sie die gleiche Anordnung für die VHDs auf dem virtuellen Computer beibehalten.

### <a name="number-and-size-of-luns-and-volumes"></a>Anzahl und Größe von LUNs und volumes

Berücksichtigen Sie beim Planen der Speicherkonfiguration für einen Failovercluster, die CSV verwendet, die folgenden Empfehlungen:

- Um festzulegen, wie viele LUNs konfigurieren, wenden Sie sich an Ihrem Speicheranbieter. Beispielsweise kann Ihre Speicheranbieter empfehlen, jede LUN mit einer Partition zu konfigurieren und eine CSV-Volume darauf platzieren.
- Es gibt keine Begrenzung für die Anzahl der virtuellen Computer, die auf einem einzelnen CSV Volume unterstützt werden können. Allerdings sollten Sie die Anzahl der virtuellen Computer an, denen Sie in der Cluster und die Arbeitslast (e/a-Vorgänge pro Sekunde) für jeden virtuellen Computer haben möchten. Beachten Sie folgende Beispiele:

  - Eine Organisation ist virtuellen Computern bereitstellen, die eine virtuelle Desktopinfrastruktur (VDI), unterstützen die eine Arbeitslast relativ gering ist. Der Cluster verwendet Hochleistungsspeicher. Der Clusterverwaltung beschließt nach Rücksprache mit der Speicheranbieter, eine relativ große Anzahl von virtuellen Computern pro Volume CSV platzieren.
  - Einer anderen Organisation ist eine große Anzahl von virtuellen Computern bereitstellen, die eine datenbankanwendung verwendeten unterstützen, die eine größere Arbeitslast ist. Cluster verwendet den Speicher Zeiteinheiten durchführen. Der Clusterverwaltung beschließt nach Rücksprache mit der Speicheranbieter eine relativ geringe Anzahl von virtuellen Computern pro Volume CSV platziert.
- Wenn Sie die Speicherkonfiguration für einen bestimmten virtuellen Computer planen, sollten Sie die benötigter des Dienstes, Anwendung oder Rolle, die dem virtuellen Computer unterstützen. Diese Anforderungen kennen, können Sie die Datenträger Konflikte zu vermeiden, die Leistung beeinträchtigt werden kann. Die Speicherkonfiguration für den virtuellen Computer sollte die Speicherkonfiguration ähneln, die Sie für einen physischen Server verwenden, die die gleichen Service, Anwendung oder Rolle ausgeführt wird. Weitere Informationen finden Sie weiter oben in diesem Thema [Anordnung von LUNs, Volumes, und VHD-Dateien](#arrangement-of-luns,-volumes,-and-vhd-files) .

    Sie können auch Datenträger Konflikte gebundener Speicher mit einer großen Anzahl von unabhängigen physischen Festplatten minimieren. Wählen Sie entsprechend der Speicherhardware, und wenden Sie sich an den Anbieter zum Optimieren der Leistung des Speichers.
- Je nach Ihrer Cluster-Arbeitslasten und deren Notwendigkeit e/a-Vorgänge können Sie berücksichtigen, konfigurieren nur einen Prozentsatz der virtuellen Computer auf jede LUN zugreifen, während andere virtuelle Computer keinen Konnektivität und stattdessen dedizierten Vorgänge berechnet werden.

## <a name="add-a-disk-to-csv-on-a-failover-cluster"></a>Hinzufügen von einem Datenträger CSV auf einem Failovercluster

Das CSV-Feature ist standardmäßig in der Failover-Clusterunterstützung aktiviert. Um einem Datenträger CSV hinzuzufügen, müssen Sie **Verfügbaren** Speichergruppe des Clusters (sofern nicht bereits vorhanden ist) einen Datenträger hinzugefügt werden und dann den Datenträger im Cluster CSV hinzufügen. Failovercluster-Manager oder den Failover Cluster Windows PowerShell-Cmdlets können Sie diese Verfahren ausführen.

### <a name="add-a-disk-to-available-storage"></a>Hinzufügen von einem Datenträger verfügbaren Speicher

1. Im Failovercluster-Manager, in der Konsolenstruktur, erweitern Sie den Namen des Clusters, und erweitern Sie dann den **Speicher**.
2. Mit der rechten Maustaste **Datenträger**, und wählen Sie dann auf **Datenträger hinzufügen**. Wird eine Liste mit den Festplatten, die für die Verwendung in einem Failovercluster hinzugefügt werden können.
3. Wählen Sie Datenträger, den Sie hinzufügen möchten, und wählen Sie dann auf **OK**.

    Festplatten werden nun die **Verfügbaren** Speichergruppe zugewiesen.

#### <a name="windows-powershell-equivalent-commands-add-a-disk-to-available-storage"></a>Entsprechende Windows PowerShell-Befehle (Hinzufügen von einem Datenträger verfügbaren Speicher)

Führen Sie die folgenden Windows PowerShell-Cmdlets oder Cmdlets die gleiche Funktion wie das vorangegangene Verfahren. Geben Sie jede Cmdlet auf einer einzelnen Zeile, obwohl sie über mehrere Zeilen hier Wortumbruch erscheint aufgrund von Einschränkungen Formatierung.

Im folgende Beispiel identifiziert die Datenträger, auf die bereit sind, den Cluster hinzugefügt werden soll, und anschließend **Verfügbaren** Speichergruppe hinzugefügt.

```PowerShell
Get-ClusterAvailableDisk | Add-ClusterDisk
```

### <a name="add-a-disk-in-available-storage-to-csv"></a>Fügen Sie einen Datenträger in verfügbaren Speicher CSV

1. Im Failovercluster-Manager, in der Konsolenstruktur, erweitern Sie den Namen des Clusters, erweitern Sie **Speicher**und wählen Sie dann auf **Datenträger**.
2. Wählen Sie eine oder mehr Festplatten, die an den **Verfügbaren Speicher**zugewiesen sind mit der rechten Maustaste in der Auswahl, und wählen Sie **zur Cluster Shared Volumes hinzufügen**.

    Festplatten werden nun die **Cluster Shared Volume** -Gruppe im Cluster zugewiesen. Festplatten werden auf jedem Clusterknoten als nummerierte Volumes (Bereitstellungspunkte) unter dem Ordner % SystemDisk ClusterStorage verfügbar gemacht. Die Volumes im Dateisystem CSVFS angezeigt werden.

>[!NOTE]
>Sie können die CSV-Volumes in den Ordner % SystemDisk ClusterStorage umbenennen.

#### <a name="windows-powershell-equivalent-commands-add-a-disk-to-csv"></a>Entsprechende Windows PowerShell-Befehle (Hinzufügen von einem Datenträger CSV)

Führen Sie die folgenden Windows PowerShell-Cmdlets oder Cmdlets die gleiche Funktion wie das vorangegangene Verfahren. Geben Sie jede Cmdlet auf einer einzelnen Zeile, obwohl sie über mehrere Zeilen hier Wortumbruch erscheint aufgrund von Einschränkungen Formatierung.

Das folgende Beispiel fügt *Cluster Datenträger 1* in **Verfügbaren Speicher** CSV auf dem lokalen Cluster.

```PowerShell
Add-ClusterSharedVolume –Name "Cluster Disk 1"
```

## <a name="enable-the-csv-cache-for-read-intensive-workloads-optional"></a>Aktivieren des CSV-Caches-Lesevorgänge Arbeitslasten (optional)

Der CSV-Cache bereitstellt, Zuweisung von Arbeitsspeicher (RAM) als Cache Write über Zwischenspeichern auf Blockebene der schreibgeschützte ungepufferte e/a-Vorgänge. (Vom CacheManager werden ungepufferte e/a-Vorgänge nicht zwischengespeichert.) Dies kann die Leistung für Anwendungen wie Hyper-V, verbessern die ungepufferte e/a-Vorgänge durchgeführt werden, wenn Sie eine virtuelle Festplatte zugreifen. Der CSV-Cache kann die Leistung von Lesevorgängen gesteigert werden ohne Zwischenspeichern Write Anforderungen. Aktivieren des Caches CSV eignet sich auch für dezentrales Skalieren Dateiserver-Szenarien.

>[!NOTE]
>Es wird empfohlen, den CSV-Cache für alle gruppierten Hyper-V und Skalierung Dateiserver-Bereitstellungen zu aktivieren.

Der CSV-Cache ist standardmäßig in Windows Server 2012 deaktiviert. In Windows Server 2012 R2 wird der Cache CSV standardmäßig aktiviert. Die Größe des Caches Block reservieren müssen Sie jedoch weiterhin zuweisen.

Die folgende Tabelle beschreibt die zwei Konfigurationseinstellungen, die den CSV-Cache zu steuern.

<table>
<thead>
<tr class="header">
<th>Name der Eigenschaft in Windows Server 2012 R2</th>
<th>Name der Eigenschaft in WindowsServer 2012</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>BlockCacheSize</strong></td>
<td><strong>SharedVolumeBlockCacheSizeInMB</strong></td>
<td>Dies ist eine allgemeine Cluster-Eigenschaft, die Ihnen ermöglicht, wie viel Arbeitsspeicher (in MB) zu definieren, um die CSV-Cache auf jedem Knoten im Cluster zu reservieren. Beispielsweise wenn ein Wert von 512 definiert ist, ist dann 512 MB des Systemspeichers auf jedem Knoten reserviert. (In viele Cluster ist 512 MB empfohlen wird der Wert). Die Standardeinstellung wird 0 (deaktiviert).</td>
</tr>
<tr class="even">
<td><strong>EnableBlockCache</strong></td>
<td><strong>CsvEnableBlockCache</strong></td>
<td>Dies ist eine private Eigenschaft des Clusters physische Datenträgerressource. Sie können die CSV-Clientcache auf eine einzelne Festplatte zu aktivieren, die CSV hinzugefügt wird. In Windows Server 2012 wird die Standardeinstellung 0 (deaktiviert). Konfigurieren Sie CSV-Cache auf einem Datenträger, um den Wert 1. In Windows Server 2012 R2 standardmäßig ist diese Einstellung aktiviert.</td>
</tr>
</tbody>
</table>

Die Leistungsindikatoren unter **Cluster CSV Volume Cache**hinzufügen können Sie den CSV-Cache in Systemmonitor überwachen.

#### <a name="configure-the-csv-cache"></a>Konfigurieren Sie den CSV-cache

1. Starten Sie Windows PowerShell als Administrator an.
2. Um einen Cache von *512* MB zu reservierende auf jedem Knoten zu definieren, geben Sie Folgendes ein:

    - Für Windows Server 2012 R2:

        ```PowerShell
        (Get-Cluster).BlockCacheSize = 512  
        ```

    - Für WindowsServer 2012:

        ```PowerShell
        (Get-Cluster).SharedVolumeBlockCacheSizeInMB = 512  
        ```
3. In Windows Server 2012 um die CSV-Clientcache auf eine CSV-Datei mit dem Namen *Cluster Datenträger 1*zu aktivieren, geben Sie Folgendes ein:

    ```PowerShell
    Get-ClusterSharedVolume "Cluster Disk 1" | Set-ClusterParameter CsvEnableBlockCache 1
    ```

>[!NOTE]
> * In Windows Server 2012 können Sie nur 20 % des physischen Arbeitsspeichers im Clientcache CSV-zuordnen. In Windows Server 2012 R2 können Sie bis zu 80 % zuordnen. Da Dateiserver Dezentrales Skalieren nicht in der Regel Speicher eingeschränkt sind, können Sie große zunichte mithilfe des zusätzlichen Arbeitsspeichers für den Cache CSV ausführen.
> * Um Ressourcenkonflikte zu vermeiden, sollten Sie jedem Knoten im Cluster neu starten, nachdem Sie den Speicher ändern, der dem Cache CSV zugewiesen ist. In Windows Server 2012 R2 ist ein Neustart nicht mehr erforderlich.
> * Nach dem Aktivieren oder Deaktivieren der CSV-Cache auf einem einzelnen Datenträger, damit die Einstellung wirksam wird, müssen Sie die physischen Datenträger-Ressource offline und wieder online zu bringen. (Standardmäßig in Windows Server 2012 R2 wird der CSV-Cache aktiviert.) 
> * Weitere Informationen zu CSV-Cache, der enthält Informationen über Leistungsindikatoren, finden Sie im Blogbeitrag [wie CSV-Cache aktivieren](https://blogs.msdn.microsoft.com/clustering/2013/07/19/how-to-enable-csv-cache/).

## <a name="back-up-csv"></a>Sichern von CSV

Es gibt mehrere Methoden zum Sichern von Informationen, die in einem Failovercluster auf CSV gespeichert ist. Sie können eine Microsoft-backup-Anwendung oder einer Anwendung nicht von Microsoft. Im Allgemeinen CSV nicht bedingen spezielle sicherungsanforderungen als lediglich diejenigen für Speicher im Cluster mit NTFS und ReFS formatiert. CSV-Sicherungen führen Sie auch andere CSV Speichervorgänge nicht unterbrochen.

Wenn Sie ein backup-Anwendung und Sicherungszeitplan für CSV auswählen, sollten Sie die folgenden Faktoren berücksichtigen:

- Lautstärkepegel Sicherung eines Datenträgers CSV kann aus jeder Knoten ausgeführt werden, die auf den Datenträger CSV verbindet.
- Ihre backup-Anwendung kann Momentaufnahmen Software oder Hardware Momentaufnahmen verwenden. Je nach die Möglichkeit der Sicherung Anwendung zu ihrer Unterstützung können Sicherungen Anwendung konsistent und konsistente (Volume Shadow Copy Service, VSS) Snapshots.
- Wenn Sie von CSV, die mehrere ausgeführten virtuellen Computern haben sichern, sollten Sie im Allgemeinen Management-basierten Betriebssystem Sicherungsmethode auswählen. Wenn Ihre backup-Anwendung unterstützt wird, können mehrere virtuelle Computer gleichzeitig gesichert werden.
- CSV unterstützen backup Requestors, auf denen Windows Server 2012 R2-Sicherung, Windows Server 2012-Sicherung oder Windows Server 2008 R2-Sicherung ausgeführt werden. Stellt jedoch Windows Server-Sicherung in der Regel nur eine grundlegende backup-Lösung, die nicht für Organisationen mit größere Cluster geeignet sein kann. Windows Server-Sicherung unterstützt nicht Backups Anwendung konsistent virtueller Maschinen auf CSV. Konsistente nur Lautstärkepegel Sicherung unterstützt. (Wenn Sie eine konsistente Sicherung wiederherstellen, wird der virtuelle Computer in dem Zustand, wenn Sie den virtuellen Computer genau gegenwärtig abgestürzt hatte, die die Sicherung durchgeführt wurde sein.) Sicherung eines virtuellen Computers auf einem Datenträger CSV wird erfolgreich ausgeführt, aber ein Error-Ereignis gibt an, dass dies nicht unterstützt wird protokolliert werden.
- Sichern von einem Failovercluster, benötigen Sie möglicherweise administrative Anmeldeinformationen.

>[!IMPORTANT]
>Stellen Sie sicher, welche Daten sorgfältig überprüfen Ihrer backup-Anwendung gesichert und wiederhergestellt wird, welche Features von CSV unterstützt wird, und den Ressourcenbedarf für die Anwendung auf jedem Clusterknoten.

>[!WARNING]
>Wenn Sie die Sicherungsdaten auf einem CSV Volume wiederherstellen müssen, achten Sie den Funktionen und Beschränkungen der backup-Anwendung verwalten und Wiederherstellen von Anwendung konsistente Daten über den Knoten im Cluster. Beispielsweise mit einigen Anwendungen, wenn im CSV-Format auf einem Knoten wiederhergestellt wird, die von den Knoten unterscheidet, in dem die CSV-Lautstärke gesichert wurde, Sie möglicherweise versehentlich wichtige Daten über den Zustand der Anwendung für den Knoten überschrieben, auf dem die Wiederherstellung stattfindet.

## <a name="more-information"></a>Weitere Informationen

- [Failoverclusterunterstützung](failover-clustering.md)
- [Gruppierte Speicherplätze bereitstellen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>)