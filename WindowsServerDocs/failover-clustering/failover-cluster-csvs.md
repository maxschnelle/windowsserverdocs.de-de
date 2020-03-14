---
title: Verwenden von freigegebenen Clustervolumes in einem Failovercluster
description: Verwenden von freigegebenen Clustervolumes in einem Failovercluster
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: da0f541c34c7f8687822bec365364fdd406fa3c3
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322692"
---
# <a name="use-cluster-shared-volumes-in-a-failover-cluster"></a>Verwenden von freigegebenen Clustervolumes in einem Failovercluster

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2

Mit freigegebenen Clustervolumes (Cluster Shared Volumes, CSVs) können mehrere Knoten in einem Failovercluster gleichzeitig über den Lese-/Schreibzugriff auf dieselbe LUN (Datenträger) verfügen, die als NTFS-Volume bereitgestellt wird. (In Windows Server 2012 R2 kann der Datenträger als NTFS oder robustes Datei System (Refs) bereitgestellt werden.) Bei CSV können Cluster Rollen schnell ein Failover von einem Knoten zu einem anderen Knoten ausführen, ohne dass eine Änderung des Laufwerks Besitzes erforderlich ist oder ein Volume getrennt und bereitgestellt wird. Freigegebene Clustervolumes vereinfachen auch die Verwaltung einer möglicherweise großen Anzahl von LUNs in einem Failovercluster.

CSV stellen ein allgemeines Cluster Dateisystem bereit, das über NTFS (oder Refs in Windows Server 2012 R2) geschichtet ist. CSV-Anwendungen umfassen Folgendes:

- VHD-Clusterdateien für virtuelle Hyper-V-Clustercomputer
- Dateifreigaben mit horizontaler Skalierung zum Speichern von Anwendungsdaten für die Clusterrolle „Dateiserver mit horizontaler Skalierung“. Beispiele für die Anwendungsdaten dieser Rolle umfassen Dateien von virtuellen Hyper-V-Computern und Microsoft SQL Server-Daten. (Beachten Sie, dass Refs für eine Dateiserver mit horizontaler Skalierung nicht unterstützt wird.) Weitere Informationen zu Dateiserver mit horizontaler Skalierung finden Sie unter [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](sofs-overview.md).

> [!NOTE]
> Csvs unterstützen die Microsoft SQL Server gruppierten Arbeits Auslastungen in SQL Server 2012 und früheren Versionen von SQL Server nicht.

In Windows Server 2012 wurde die CSV-Funktionalität erheblich verbessert. Abhängigkeiten von Active Directory-Domänendiensten wurden z. B. entfernt. Für die funktionalen Verbesserungen in **chkdsk**, für die Interoperabilität mit Antiviren- und Sicherungsanwendungen sowie für die Integration mit allgemeinen Speicherfeatures wie BitLocker-verschlüsselte Volumes und Speicherplätze wurde die entsprechende Unterstützung hinzugefügt. Eine Übersicht über die CSV-Funktionalität, die in Windows Server 2012 eingeführt wurde, finden Sie unter [What es New in Failover Clustering in Windows Server 2012 \[umgeleitet\]](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)>).

Windows Server 2012 R2 bietet zusätzliche Funktionen, z. b. den verteilten CSV-Besitz, eine erhöhte Resilienz durch die Verfügbarkeit des Server Dienstanbieter, eine größere Flexibilität bei der Menge an physischem Arbeitsspeicher, die Sie dem CSV-Cache zuordnen können. Diagnose und erweiterte Interoperabilität, die die Unterstützung für Refs und die Deduplizierung umfasst. Weitere Informationen finden Sie unter [Neues beim Failoverclustering](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)>).

> [!NOTE]
> Informationen zur Verwendung der Datendeduplizierung auf freigegebenen Clustervolumes für VDI-Szenarien (Virtual Desktop Infrastructure) finden Sie in den Blogbeiträgen [Deploying Data Deduplication for VDI storage in Windows Server 2012 R2](https://blogs.technet.com/b/filecab/archive/2013/07/31/deploying-data-deduplication-for-vdi-storage-in-windows-server-2012-r2.aspx) und [Extending Data Deduplication to new workloads in Windows Server 2012 R2](https://blogs.technet.com/b/filecab/archive/2013/07/31/extending-data-deduplication-to-new-workloads-in-windows-server-2012-r2.aspx)(beide in englischer Sprache).

## <a name="review-requirements-and-considerations-for-using-csv-in-a-failover-cluster"></a>Überprüfen der Anforderungen und Überlegungen zur Verwendung von CSV in einem Failovercluster

Bevor Sie freigegebene Clustervolumes (CSV) in einem Failovercluster verwenden, lesen Sie die Anforderungen und Überlegungen zum Netzwerk, Speicher und anderen Komponenten in diesem Abschnitt.

### <a name="network-configuration-considerations"></a>Überlegungen zur Netzwerkkonfiguration

Berücksichtigen Sie Folgendes, wenn Sie die Netzwerke konfigurieren, die freigegebene Clustervolumes unterstützen.

- **Mehrere Netzwerke und Netzwerkadapter**: Es wird empfohlen, dass mehrere Clusternetzwerke den CSV-Datenverkehr übernehmen oder Sie kombinierte Netzwerkadapter konfigurieren, um im Falle eines Netzwerkfehlers die entsprechende Fehlertoleranz bereitzustellen.
    
    Wenn die Clusterknoten mit Netzwerken verbunden sind, die vom Cluster nicht verwendet werden sollten, können Sie diese Netzwerke deaktivieren. Es wird z. B. empfohlen, dass Sie iSCSI-Netzwerke für Cluster deaktivieren, um CSV-Datenverkehr in diesen Netzwerken zu verhindern. Klicken Sie zum Deaktivieren eines Netzwerks in Failovercluster-Manager auf **Netzwerke**, wählen Sie das Netzwerk aus, wählen Sie die Aktion **Eigenschaften** aus, und wählen Sie dann **Netzwerkkommunikation für Cluster in diesem Netzwerk nicht zulassen**. Alternativ können Sie die **Role** -Eigenschaft des Netzwerks mithilfe des Windows PowerShell-Cmdlets [Get-ClusterNetwork](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternetwork?view=win10-ps) konfigurieren.
- **Netzwerkadaptereigenschaften** Stellen Sie in den Eigenschaften für alle Adapter, die für die Clusterkommunikation zuständig sind, sicher, dass die folgenden Einstellungen aktiviert sind:

  - **Client für Microsoft-Netzwerke** und **Datei- und Druckerfreigabe für Microsoft-Netzwerke**: Diese Einstellungen unterstützen SMB 3.0 (Server Message Block), mit dem standardmäßig der CSV-Datenverkehr zwischen den Knoten übertragen wird. Stellen Sie zum Aktivieren von SMB außerdem sicher, dass der Server- und der Arbeitsstationsdienst aktiv sind und diese auf den einzelnen Clusterknoten für den automatischen Start konfiguriert sind.

    >[!NOTE]
    >In Windows Server 2012 R2 gibt es mehrere Server Dienst Instanzen pro Failoverclusterknoten. Es gibt eine Standardinstanz, die den eingehenden Datenverkehr von SMB-Clients bearbeitet, die auf normale Dateifreigaben zugreifen. Dann gibt es noch eine zweite CSV-Instanz, die ausschließlich den CSV-Datenverkehr zwischen den Knoten bearbeitet. Wenn der Serverdienst auf einem Knoten Fehler aufweist, wechselt das CSV-Besitzrecht automatisch zu einem anderen Knoten.

    SMB 3.0 umfasst die Features SMB Multichannel und SMB Direct, sodass CSV-Datenverkehr über mehrere Netzwerke im Cluster gestreamt und Netzwerkadapter genutzt werden können, die Remotezugriff auf den direkten Speicher (Remote Direct Memory Access, RDMA) unterstützen. SMB Multichannel wird standardmäßig für den CSV-Datenverkehr verwendet. Weitere Informationen finden Sie unter [Server Message Block – Übersicht](../storage/file-server/file-server-smb-overview.md)
  - **Microsoft Failover Cluster Virtual Adapter Performance Filter**: Diese Einstellung verbessert die Möglichkeit von Knoten, eine E/A-Umleitung auszuführen, wenn diese erforderlich ist, um freigegebene Clustervolumes zu erreichen, z. B. wenn Verbindungsfehler einen Knoten daran hindern, eine direkte Verbindung zum CSV-Datenträger herzustellen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Informationen zur e/a-Synchronisierung und e/a-Umleitung bei der CSV-Kommunikation](#about-io-synchronization-and-io-redirection-in-csv-communication) .
- **Clusternetzwerkpriorisierung**: Im Allgemeinen wird empfohlen, dass Sie die für den Cluster konfigurierten Voreinstellungen für die Netzwerke nicht ändern.
- **IP-Subnetzkonfiguration**: Für Knoten in einem Netzwerk, in dem freigegebene Clustervolumes verwendet werden, ist keine bestimmte Subnetzkonfiguration erforderlich. Freigegebene Clustervolumes (CSV) können Cluster mit mehreren Subnetzen unterstützen.
- **Richtlinienbasierter QoS (Quality of Service)** : Es wird empfohlen, dass Sie für jeden Knoten eine QoS-Prioritätenrichtlinie und eine Richtlinie für die Mindestbandbreite für den Netzwerkverkehr konfigurieren, wenn Sie CSV verwenden. Weitere Informationen finden Sie unter [Quality of Service (QoS)](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831679(v%3dws.11)>).
- **Speichernetzwerk**: Empfehlungen zum Speichernetzwerk finden Sie in den Anleitungen Ihres Speicheranbieters. Weitere Überlegungen zum Speicher für CSV finden Sie unter Anforderungen an die [Speicher-und](#storage-and-disk-configuration-requirements) Datenträger Konfiguration weiter unten in diesem Thema.

Eine Übersicht über die Hardware-, Netzwerk- und Speicheranforderungen für Failovercluster finden Sie unter [Hardwareanforderungen und Speicheroptionen für das Failoverclustering](clustering-requirements.md).

#### <a name="about-io-synchronization-and-io-redirection-in-csv-communication"></a>Informationen zur E/A-Synchronisierung und E/A-Umleitung bei der CSV-Kommunikation

- E **/a-Synchronisierung**: CSV ermöglicht mehreren Knoten den gleichzeitigen Lese-/Schreibzugriff auf denselben freigegebenen Speicher. Wenn ein Knoten Datenträgereingaben/-ausgaben (E/A) für ein CSV-Volume ausführt, kommuniziert der Knoten direkt mit dem Speicher, z. B. über ein SAN (Storage Area Network). Zu jedem Zeitpunkt ist jedoch ein einzelner Knoten (auch als Koordinatorknoten bezeichnet) „Besitzer“ der physischen Datenträgerressource, die dieser LUN zugeordnet ist. Der Koordinatorknoten für ein CSV-Volume wird im Failovercluster-Manager unter **Datenträger** als **Besitzerknoten** angezeigt. Sie wird auch in der Ausgabe des Windows PowerShell-Cmdlets [Get-clustersharedvolume](https://docs.microsoft.com/powershell/module/failoverclusters/get-clustersharedvolume?view=win10-ps) angezeigt.

  >[!NOTE]
  >In Windows Server 2012 R2 ist der CSV-Besitz gleichmäßig auf die Failoverclusterknoten verteilt, basierend auf der Anzahl der CSV-Volumes, die für die einzelnen Knoten gehören. Zudem wird das Besitzrecht automatisch ausgeglichen, wenn z. B. folgende Bedingungen auftreten: CSV-Failover, ein Knoten wird dem Cluster erneut hinzugefügt, ein Knoten wird zum Cluster hinzugefügt, ein Clusterknoten wird neu gestartet, der Failovercluster wird nach dem Herunterfahren wieder gestartet.

  Wenn im Dateisystem auf einem CSV-Volume bestimmte kleinere Änderungen auftreten, müssen diese Metadaten nicht nur auf dem Koordinatorknoten, sondern auf den einzelnen physischen Knoten synchronisiert werden, die auf die LUN zugreifen. Wenn z. B. ein virtueller Computer auf einem CSV-Volume gestartet, erstellt, gelöscht oder migriert wird, müssen diese Informationen auf den einzelnen physischen Knoten synchronisiert werden, die auf den virtuellen Computer zugreifen. Diese Metadatenaktualisierungen werden in den Clusternetzwerken mithilfe von SMB 3.0 gleichzeitig ausgeführt. Für diese Vorgänge ist es nicht erforderlich, dass alle physischen Knoten mit dem freigegebenen Speicher kommunizieren.

- E/a- **Umleitung**: Speicher Verbindungsfehler und bestimmte Speichervorgänge können verhindern, dass ein bestimmter Knoten direkt mit dem Speicher kommuniziert. Um die Funktion aufrechtzuerhalten, während der Knoten nicht mit dem Speicher kommuniziert, leitet der Knoten die Datenträger-E/A über ein Clusternetzwerk an den Koordinatorknoten weiter, von dem der Datenträger derzeit bereitgestellt wird. Wenn auf dem aktuellen Koordinatorknoten ein Verbindungsfehler aufgetreten ist, werden alle E/A-Vorgänge des Datenträgers vorübergehend in eine Warteschlange gestellt, während ein neuer Knoten als Koordinatorknoten eingerichtet wird.

Der Server verwendet in Abhängigkeit von der Situation einen der folgenden E/A-Umleitungsmodi:

- **Dateisystemumleitung** Die Umleitung erfolgt pro Volume, wenn z. B. von einer Sicherungsanwendung CSV-Snapshots erstellt werden, sobald ein CSV-Volume manuell in den Modus „E/A-Umleitung“ versetzt wird.
- **Blockumleitung** Die Umleitung erfolgt auf Dateiblockebene, wenn z. B. die Speicherverbindung zu einem Volume unterbrochen wird. Die Blockumleitung erweist sich im Vergleich zur Dateisystemumleitung als wesentlich schneller.

In Windows Server 2012 R2 können Sie den Status eines CSV-Volumes auf Knoten Basis anzeigen. Sie können z. B. erkennen, ob die E/A-Vorgänge direkt oder umgeleitet erfolgen, oder ob das CSV-Volume möglicherweise nicht verfügbar ist. Wenn sich ein CSV-Volume im E/A-Umleitungsmodus befindet, wird auch der Grund hierfür angezeigt. Verwenden Sie das Windows PowerShell-Cmdlet **Get-ClusterSharedVolumeState**, um diese Informationen anzuzeigen.

> [!NOTE]
> * In Windows Server 2012 führen CSV aufgrund von Verbesserungen beim CSV-Entwurf mehr Vorgänge im direkten e/a-Modus aus als in Windows Server 2008 R2.
> * Aufgrund der Integration von CSV mit SMB 3.0-Features wie SMB Multichannel und SMB Direct kann der umgeleitete E/A-Datenverkehr über mehrere Clusternetzwerke geleitet werden.
> * Sie sollten für Ihre Clusternetzwerke während der E/A-Umleitung eine mögliche Zunahme des Netzwerkdatenverkehrs zum Koordinatorknoten berücksichtigen.

### <a name="storage-and-disk-configuration-requirements"></a>Anforderungen an die Speicher- und Datenträgerkonfiguration

Der Speicher und die Datenträger müssen zur Verwendung von CSV die folgenden Anforderungen erfüllen:

- **Dateisystemformat**: In Windows Server 2012 R2 muss ein Datenträger oder ein Speicherplatz für ein CSV-Volume ein Basis Datenträger sein, der mit NTFS oder Refs partitioniert ist. In Windows Server 2012 muss ein Datenträger oder ein Speicherplatz für ein CSV-Volume ein Basis Datenträger sein, der mit NTFS partitioniert ist.

  Ein freigegebenes Clustervolume hat die folgenden zusätzlichen Anforderungen:
    
  - In Windows Server 2012 R2 können Sie keinen Datenträger für eine CSV-Datei verwenden, die mit FAT oder FAT32 formatiert ist.
  - In Windows Server 2012 können Sie keinen Datenträger für eine CSV-Datei verwenden, die mit FAT, FAT32 oder Refs formatiert ist.
  - Wenn Sie Speicherplatz für ein CSV verwenden möchten, können Sie einen einfachen oder einen Spiegelspeicherplatz konfigurieren. In Windows Server 2012 R2 können Sie auch einen Paritäts Speicherplatz konfigurieren. (In Windows Server 2012 werden Paritäts Speicherplätze von CSV nicht unterstützt.)
  - Ein CSV kann nicht als Quorumzeugendatenträger verwendet werden. Weitere Informationen zum Cluster Quorum finden Sie Untergrund Legendes zu [Quorum in direkte Speicherplätze](../storage/storage-spaces/understand-quorum.md).
  - Nachdem Sie einen Datenträger als CSV hinzugefügt haben, wird es im CSVFS-Format (für das CSV-Dateisystem) festgelegt. Dadurch kann der CSV-Speicher vom Cluster und anderer Software vom NTFS- oder ReFS-Speicher unterschieden werden. Im Allgemeinen unterstützt CSVFS dieselbe Funktionalität wie NTFS oder ReFS. Bestimmte Features werden jedoch nicht unterstützt. In Windows Server 2012 R2 können Sie z. b. die Komprimierung für CSV nicht aktivieren. In Windows Server 2012 können Sie die Datendeduplizierung oder Komprimierung für CSV nicht aktivieren.
- **Ressourcentyp im Cluster**: Für ein CSV-Volume müssen Sie den Ressourcentyp „Physischer Datenträger“ verwenden. Ein zum Clusterspeicher hinzugefügter Datenträger oder Speicherplatz wird standardmäßig auf diese Weise konfiguriert.
- **Auswahl von CSV- oder anderen Datenträgern im Clusterspeicher**: Berücksichtigen Sie bei der Auswahl eines oder mehrerer Datenträger für einen virtuellen Clustercomputer, wie die einzelnen Datenträger verwendet werden. Wenn ein Datenträger zum Speichern von Dateien verwendet wird, die von Hyper-V erstellt wurden, z. B. VHD-Dateien oder Konfigurationsdateien, können Sie zwischen den CSV-Datenträgern oder den anderen verfügbaren Datenträgern im Clusterspeicher wählen. Wenn ein Datenträger einem physischen Datenträger entspricht, der direkt an den virtuellen Computer angeschlossen ist (auch als Pass-Through-Datenträger bezeichnet), können Sie keinen CSV-Datenträger auswählen. Stattdessen müssen Sie aus den anderen verfügbaren Datenträgern im Clusterspeicher auswählen.
- **Pfadname zum Identifizieren von Datenträgern**: Datenträger werden in CSV über den Pfadnamen identifiziert. Jeder Pfad befindet sich auf dem Systemlaufwerk des Knotens als nummeriertes Volume unter dem **\\ClusterStorage** -Ordner. Dieser Pfad ist beim Anzeigen auf jedem anderen Knoten im Cluster gleich. Die Volumes können bei Bedarf umbenannt werden.

Speicheranforderungen für CSV finden Sie in den Anleitungen Ihres Speicheranbieters. Weitere Überlegungen zur Speicherplanung für CSV finden Sie weiter unten in diesem Thema unter [Planen der Verwendung von CSV in einem Failovercluster](#plan-to-use-csv-in-a-failover-cluster).

### <a name="node-requirements"></a>Knotenanforderungen

Die Knoten müssen zur Verwendung von CSV die folgenden Anforderungen erfüllen:

- **Laufwerkbuchstabe des Systemdatenträgers**. Der Laufwerkbuchstabe für den Systemdatenträger muss auf allen Knoten identisch sein.
- **Authentifizierungsprotokoll**. Das NTLM-Protokoll muss auf allen Knoten aktiviert werden. Dieses Verhalten ist standardmäßig aktiviert.

## <a name="plan-to-use-csv-in-a-failover-cluster"></a>Planen der Verwendung von CSV in einem Failovercluster

In diesem Abschnitt werden Planungsüberlegungen und Empfehlungen für die Verwendung von CSV in einem Failovercluster mit Windows Server 2012 R2 oder Windows Server 2012 aufgeführt.

> [!IMPORTANT]
> Fragen Sie Ihren Speicheranbieter, um Empfehlungen zur Konfiguration Ihrer Speichereinheit für CSV zu erhalten. Wenn die Empfehlungen des Speicheranbieters von den Informationen in diesem Thema abweichen, richten Sie sich nach den Empfehlungen des Speicheranbieters.

### <a name="arrangement-of-luns-volumes-and-vhd-files"></a>Anordnung von LUNs, Volumes und VHD-Dateien

Um CSV optimal zur Bereitstellung von Speicher für virtuelle Clustercomputer zu nutzen, ist es hilfreich, die Anordnung der LUNs (Datenträger) beim Konfigurieren der physischen Server zu überprüfen. Wenn Sie die entsprechenden virtuellen Computer konfigurieren, versuchen Sie, die VHD-Dateien auf ähnliche Weise anzuordnen.

Betrachten Sie einen physischen Server, für den Sie die Datenträger und Dateien organisieren möchten, wie folgt:

- Systemdateien, einschließlich einer Auslagerungsdatei, auf einem physischen Datenträger
- Dateidateien auf einem anderen physischen Datenträger

Für einen ähnlichen virtuellen Clustercomputer sollten Sie die Volumes und Dateien auf ähnliche Weise anordnen:

- Systemdateien, einschließlich einer Auslagerungsdatei, in einer VHD-Datei auf einem CSV
- Datendateien in einer VHD-Datei auf einem anderen CSV

Wenn Sie einen weiteren virtuellen Computer hinzufügen, sollten Sie dieselbe Anordnung für die VHD-Dateien auf diesem virtuellen Computer beibehalten (falls möglich).

### <a name="number-and-size-of-luns-and-volumes"></a>Anzahl und Größe von LUNs und Volumes

Wenn Sie die Speicherkonfiguration für einen Failovercluster planen, der CSV verwendet, berücksichtigen Sie die folgenden Empfehlungen:

- Wenden Sie sich an Ihren Speicheranbieter, um zu entscheiden, wie viele LUNs konfiguriert werden müssen. Ihr Speicheranbieter kann z. B. empfehlen, dass Sie jede LUN mit einer Partition konfigurieren, auf die ein CSV-Volume platziert wird.
- Es gibt keine Einschränkungen hinsichtlich der Anzahl der virtuellen Computer, die auf einem einzelnen CSV-Volume unterstützt werden können. Sie sollten jedoch die Anzahl der virtuellen Computer, die für den Cluster geplant sind, und die Arbeitsauslastung (E/A-Vorgänge pro Sekunde) für die einzelnen virtuellen Computer berücksichtigen. Beachten Sie folgende Beispiele:

  - Eine Organisation stellt virtuelle Computer bereit, die eine virtuelle Desktopinfrastruktur (VDI) unterstützen, die eine relativ gemäßigte Arbeitsauslastung aufweist. Der Cluster verwendet leistungsstarken Speicher. Der Clusteradministrator entscheidet sich nach der Rückfrage beim Speicheranbieter dazu, eine relativ große Anzahl von virtuellen Computern auf den einzelnen CSV-Volumes zu platzieren.
  - Eine andere Organisation stellt eine große Anzahl von virtuellen Computern bereit, die eine stark beanspruchte Datenbankanwendung und somit eine stärkere Arbeitsauslastung unterstützen. Der Cluster verwendet weniger leistungsstarken Speicher. Der Clusteradministrator entscheidet sich nach der Rückfrage beim Speicheranbieter dazu, eine relativ kleine Anzahl von virtuellen Computern auf den einzelnen CSV-Volumes zu platzieren.
- Wenn Sie die Speicherkonfiguration für einen bestimmten virtuellen Computer planen, berücksichtigen Sie die Datenträgeranforderungen des Diensts, der Anwendung oder der Rolle, die vom virtuellen Computer unterstützt werden. Sie können Datenträgerkonflikte besser vermeiden, die zu schlechten Leistungen führen können, wenn Sie diese Anforderungen verstehen. Die Speicherkonfiguration für den virtuellen Computer sollte stark der Speicherkonfiguration ähneln, die Sie für einen physischen Server verwenden würden, der denselben Dienst, dieselbe Anwendung oder dieselbe Rolle ausführt. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Anordnung von LUNs, Volumes und VHD-Dateien](#arrangement-of-luns-volumes-and-vhd-files) .

    Sie können Datenträgerkonflikte auch dadurch reduzieren, dass Sie Speicher mit einer großen Anzahl von unabhängigen physischen Festplatten verwenden. Wählen Sie Ihre Speicherhardware entsprechend aus, und wenden Sie sich an den Anbieter, um die Leistung des Speichers zu optimieren.
- In Abhängigkeit von Ihrer Clusterarbeitsauslastung und dem entsprechenden Bedarf an E/A-Vorgängen können Sie erwägen, dass Sie nur einen Teil der virtuellen Computer für den Zugriff auf die einzelnen LUNs konfigurieren, während andere virtuelle Computer keine Verbindungen aufweisen und stattdessen zur Berechnung von Operationen vorgesehen sind.

## <a name="add-a-disk-to-csv-on-a-failover-cluster"></a>Hinzufügen von Datenträgern zum CSV auf einem Failovercluster

Das CSV-Feature ist für das Failoverclustering standardmäßig aktiviert. Wenn Sie einen Datenträger zum freigegebenen Clustervolume (CSV) hinzufügen möchten, müssen Sie einen Datenträger zur Gruppe **Verfügbarer Speicher** des Clusters hinzufügen (sofern er nicht bereits hinzugefügt wurde) und dann den Datenträger zum CSV auf dem Cluster hinzufügen. Sie können Failovercluster-Manager oder die Windows PowerShell-Cmdlets für Failovercluster verwenden, um diese Prozeduren auszuführen.

### <a name="add-a-disk-to-available-storage"></a>Hinzufügen eines Datenträgers zum verfügbaren Speicher

1. Erweitern Sie im Failovercluster-Manager in der Konsolenstruktur den Namen des Clusters, und erweitern Sie dann die Option **Speicher**.
2. Klicken Sie mit der rechten Maustaste auf Daten **Träger und dann**auf Datenträger **Hinzufügen** Es wird eine Liste mit den Datenträgern angezeigt, die zu einem Failovercluster hinzugefügt werden können.
3. Wählen Sie die Datenträger aus, die Sie hinzufügen möchten, und klicken Sie dann auf **OK**.

    Diese Datenträger werden jetzt zur Gruppe **Verfügbarer Speicher** zugeordnet.

#### <a name="windows-powershell-equivalent-commands-add-a-disk-to-available-storage"></a>Äquivalente Windows PowerShell-Befehle (Hinzufügen eines Datenträgers zum verfügbaren Speicher)

Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.

Im folgenden Beispiel werden die Datenträger identifiziert, die zum Cluster hinzugefügt werden können, und diese dann zur Gruppe **Verfügbarer Speicher** hinzugefügt.

```PowerShell
Get-ClusterAvailableDisk | Add-ClusterDisk
```

### <a name="add-a-disk-in-available-storage-to-csv"></a>Hinzufügen eines Datenträgers im verfügbaren Speicher zum CSV

1. Erweitern **Sie in**Failovercluster-Manager in der Konsolen Struktur den Namen des Clusters, erweitern Sie **Speicher**, und wählen Sie dann Datenträger aus.
2. Wählen Sie mindestens einen Datenträger aus, der dem **verfügbaren Speicher**zugewiesen ist, klicken Sie mit der rechten Maustaste auf die Auswahl, und wählen Sie dann **zu freigegebenen Clustervolumes**

    Die Datenträger werden jetzt im Cluster zur Gruppe **Freigegebene Clustervolumes** zugewiesen. Die Datenträger werden für die einzelnen Clusterknoten als nummerierte Volumes (Bereitstellungspunkte) unter dem Ordner „%SystemDisk%ClusterStorage“ zur Verfügung gestellt. Die Volumes werden im CSVFS-Dateisystem angezeigt.

>[!NOTE]
>Sie können CSV-Volumes im Ordner „%SystemDisk%ClusterStorage“ umbenennen.

#### <a name="windows-powershell-equivalent-commands-add-a-disk-to-csv"></a>Äquivalente Windows PowerShell-Befehle (Hinzufügen eines Datenträgers zu einem CSV)

Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.

Im folgenden Beispiel wird *Cluster Disk 1* in **Verfügbarer Speicher** zum CSV auf dem lokalen Cluster hinzugefügt.

```PowerShell
Add-ClusterSharedVolume –Name "Cluster Disk 1"
```

## <a name="enable-the-csv-cache-for-read-intensive-workloads-optional"></a>Aktivieren des CSV-Cache für Auslastungen mit intensiven Lesevorgängen (optional)

Der CSV-Cache ermöglicht das Zwischenspeichern von ungepufferten E/A-Vorgängen auf Blockebene, indem Systemspeicher (RAM) als Durchschreibcache zugewiesen wird. (Nicht gepufferte e/a-Vorgänge werden nicht vom Cache-Manager zwischengespeichert.) Dies kann die Leistung für Anwendungen wie Hyper-V verbessern, die nicht gepufferte e/a-Vorgänge für den Zugriff auf eine VHD durchführt. Der CSV-Cache kann die Leistung von Leseanforderungen verstärken, ohne Schreibanforderungen zwischenzuspeichern. Das Aktivieren des CSV-Cache ist auch für Dateiserverszenarien mit horizontaler Skalierung hilfreich.

>[!NOTE]
>Es wird empfohlen, dass Sie den CSV-Cache für alle geclusterten Hyper-V- und Dateiserverbereitstellungen mit horizontaler Skalierung aktivieren.

In Windows Server 2012 ist der CSV-Cache standardmäßig deaktiviert. In Windows Server 2012 R2 und höher ist der CSV-Cache standardmäßig aktiviert. Sie müssen jedoch weiterhin die Größe des zu reservierenden Blockcache zuweisen.

In der folgenden Tabelle werden die beiden Konfigurationseinstellungen beschrieben, die den CSV-Cache steuern.

| Windows Server 2012 R2 und höher |  Windows Server 2012                 | Beschreibung |
| -------------------------------- | ------------------------------------ | ----------- |
| BlockCacheSize                   | SharedVolumeBlockCacheSizeInMB       | Dies ist eine allgemeine Clustereigenschaft, mit der Sie festlegen können, wie viel Systemspeicher (in Megabytes) für den CSV-Cache auf den einzelnen Knoten im Cluster reserviert wird. Wenn Sie z. B. den Wert „512“ festlegen, werden 512 MB des Systemspeichers auf jedem Knoten reserviert. (In vielen Clustern ist 512 MB ein empfohlener Wert.) Die Standardeinstellung ist 0 (deaktiviert). |
| EnableBlockCache                 | CsvEnableBlockCache                  | Dies ist eine private Eigenschaft der physischen Datenträgerressource des Clusters. Mit dieser Eigenschaft können Sie den CSV-Cache auf einem einzelnen Datenträger aktivieren, der zum CSV hinzugefügt wird. In Windows Server 2012 ist die Standardeinstellung 0 (deaktiviert). Legen Sie den Wert 1 fest, um den CSV-Cache auf einem Datenträger zu aktivieren. In Windows Server 2012 R2 ist diese Einstellung standardmäßig aktiviert. |

Sie können den CSV-Cache über den Systemmonitor überwachen, indem Sie die Indikatoren unter **Cache für freigegebene Clustervolumes** hinzufügen.

#### <a name="configure-the-csv-cache"></a>Konfigurieren des CSV-Caches

1. Starten Sie Windows PowerShell als Administrator.
2. Geben Sie Folgendes ein, um einen Cache von *512* MB auf den einzelnen Knoten zu reservieren:

    - Für Windows Server 2012 R2 und höher:

        ```PowerShell
        (Get-Cluster).BlockCacheSize = 512  
        ```

    - Windows Server 2012:

        ```PowerShell
        (Get-Cluster).SharedVolumeBlockCacheSizeInMB = 512  
        ```
3. Geben Sie in Windows Server 2012 folgendes ein, um den CSV-Cache auf einem CSV namens *Cluster Disk 1*zu aktivieren:

    ```PowerShell
    Get-ClusterSharedVolume "Cluster Disk 1" | Set-ClusterParameter CsvEnableBlockCache 1
    ```

>[!NOTE]
> * In Windows Server 2012 können Sie dem CSV-Cache nur 20% des gesamten physischen Arbeitsspeichers zuordnen. In Windows Server 2012 R2 und höher können Sie bis zu 80% zuordnen. Da Dateiserver mit horizontaler Skalierung in der Regel keine Speichereinschränkungen aufweisen, können Sie die Leistung erheblich steigern, indem Sie den zusätzlichen Arbeitsspeicher für den CSV-Cache verwenden.
> * Um Ressourcenkonflikte zu vermeiden, sollten Sie jeden Knoten im Cluster neu starten, nachdem Sie den dem CSV-Cache zugeordneten Arbeitsspeicher geändert haben. In Windows Server 2012 R2 und höher ist ein Neustart nicht mehr erforderlich.
> * Nachdem Sie den CSV-Cache auf einem einzelnen Datenträger aktiviert oder deaktiviert haben, müssen Sie die physische Datenträgerressource offline und anschließend wieder online schalten, damit die Einstellung wirksam wird. (In Windows Server 2012 R2 und höher ist der CSV-Cache standardmäßig aktiviert.) 
> * Weitere Informationen zum CSV-Cache, einschließlich Informationen zu Leistungsindikatoren, finden Sie im Blogbeitrag [How to Enable CSV Cache](https://blogs.msdn.microsoft.com/clustering/2013/07/19/how-to-enable-csv-cache/)(in englischer Sprache).

## <a name="backing-up-csvs"></a>Sichern von CSVs

Es gibt mehrere Methoden zum Sichern von Informationen, die in csvs in einem Failovercluster gespeichert werden. Sie können eine Microsoft-Sicherungsanwendung oder eine nicht von Microsoft stammende Anwendung verwenden. Im Allgemeinen erfordern freigegebene Clustervolumes (CSV) keine besonderen Sicherungsanforderungen. Lediglich der Clusterspeicher muss mit NTFS oder ReFS formatiert werden. Zudem unterbrechen CSV-Sicherungen keine anderen CSV-Speichervorgänge.

Bei der Auswahl einer Sicherungsanwendung und eines Sicherungszeitplans für CSV sollten Sie die folgenden Faktoren berücksichtigen:

- Die Sicherung eines CSV-Volumes auf Volumeebene kann von jedem Knoten ausgeführt werden, der über eine Verbindung zum CSV-Volume verfügt.
- Die Sicherungsanwendung kann Software- oder Hardwaremomentaufnahmen verwenden. In Abhängigkeit davon, ob sie von Ihrer Sicherungsanwendung unterstützt werden, können Sicherungen anwendungskonsistente und absturzkonsistente Momentaufnahmen des Volumeschattenkopie-Diensts (Volume Shadow Copy Service, VSS) verwenden.
- Wenn Sie ein freigegebenes Clustervolume sichern, das über mehrere aktive virtuelle Computer verfügt, sollten Sie im Allgemeinen eine auf dem Verwaltungsbetriebssystem basierende Sicherungsmethode auswählen. Es können mehrere virtuelle Computer gleichzeitig gesichert werden, wenn diese Option von Ihrer Sicherungsanwendung unterstützt wird.
- CSV unterstützt sicherungsanforderer, auf denen Windows Server 2012 R2 Backup, Windows Server 2012 Backup oder Windows Server 2008 R2 Backup ausgeführt wird. Die Windows Server-Sicherung bietet im Allgemeinen jedoch nur eine einfache Sicherungslösung, die möglicherweise nicht für Organisation mit großen Clustern geeignet ist. Die Windows Server-Sicherung unterstützt keine anwendungskonsistente Sicherung virtueller Computer auf freigegebenen Clustervolumes. Sie unterstützt ausschließlich die absturzkonsistente Sicherung auf Volumeebene. (Wenn Sie eine Absturz konsistente Sicherung wiederherstellen, befindet sich der virtuelle Computer im gleichen Zustand wie bei einem Absturz der virtuellen Maschine, die zu dem Zeitpunkt, zu dem die Sicherung erfolgte, abgestürzt ist.) Eine Sicherung eines virtuellen Computers auf einem CSV-Volume ist erfolgreich, es wird jedoch ein Fehler Ereignis protokolliert, das anzeigt, dass dies nicht unterstützt wird.
- Zum Sichern eines Failoverclusters sind möglicherweise Administratoranmeldeinformationen erforderlich.

> [!IMPORTANT]
>Überprüfen Sie sorgfältig, welche Daten von der Sicherungsanwendung gesichert und wiederhergestellt werden, welche CSV-Features unterstützt werden und welche Ressourcenanforderungen für die Anwendung auf den einzelnen Clusterknoten erforderlich sind.

> [!WARNING]
> Wenn Sie die Sicherungsdaten auf einem CSV-Volume wiederherstellen müssen, beachten Sie die Möglichkeiten und Einschränkungen der Sicherungsanwendung hinsichtlich der Verwaltung und Wiederherstellung anwendungskonsistenter Daten auf den verschiedenen Clusterknoten. Wenn das freigegebene Clustervolume z. B. bei einigen Anwendungen auf einem anderen Knoten als bei der Sicherung wiederherstellt wird, können Sie auf dem Knoten, auf dem die Wiederherstellung erfolgt, versehentlich wichtige Daten zum Anwendungsstatus überschreiben.

## <a name="more-information"></a>Weitere Informationen

- [Failoverclustering](failover-clustering.md)
- [Bereitstellen von Cluster Speicherplätzen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>)