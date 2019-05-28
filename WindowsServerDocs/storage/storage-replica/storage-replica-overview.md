---
title: Übersicht über Speicherreplikate
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 4/26/2019
ms.assetid: e9b18e14-e692-458a-a39f-d5b569ae76c5
ms.openlocfilehash: e8b437a1a4ba3e5c10d6709e23efb306a077a21b
ms.sourcegitcommit: 4ff3d00df3148e4bea08056cea9f1c3b52086e5d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2019
ms.locfileid: "64773536"
---
# <a name="storage-replica-overview"></a>Übersicht über Speicherreplikate

>Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)

Das Speicherreplikat ist eine Windows Server-Technologie, durch die die Replikation von Volumes zwischen Servern oder Clustern für die Notfallwiederherstellung möglich ist. Darüber hinaus ermöglicht sie Ihnen, Stretched Failovercluster zu erstellen, die sich über zwei Standorte erstrecken und bei denen alle Knoten synchron bleiben.

Das Speicherreplikat unterstützt sowohl die synchrone als auch die asynchrone Replikation.

* Die **synchrone Replikation** spiegelt Daten an physischen Standorten mit ausfallsicheren Volumes wider, um auf Dateisystemebene sicherzustellen, dass während eines Ausfalls kein Datenverlust auftritt.
* Die **asynchrone Replikation** spiegelt Daten zwischen Standorten über regionale Bereiche über Netzwerklinks mit höherer Latenzen wider, jedoch ohne die Garantie, dass beide Standorte über identische Kopien der Daten zur Zeit eines Ausfalls verfügen.

## <a name="why-use-storage-replica"></a>Gründe für die Verwendung von Speicherreplikaten

Das Speicherreplikatfeature bietet für notfallwiederherstellung und-Bereitschaft Funktionen in Windows Server. Windows Server bietet die Sicherheit der keine Daten verloren gehen, mit der Möglichkeit, Daten in unterschiedlichen Racks, Etagen, Gebäuden, campussen zeitlich festzulegen, Countys und Städte synchron zu schützen. Nachdem ein Notfall eintritt, alle Daten ist an anderer Stelle ohne Risiko von Datenverlusten. Dasselbe gilt, *bevor* eine Notfallsituation eintritt. Bei Verwendung von Speicherreplikaten können Sie Workloads vor einem Katastrophenfall ohne Datenverlust an sichere Standorte verlagern, wenn Sie rechtzeitig über das Ereignis informiert sind.  

Speicherreplikate ermöglichen eine effizientere Verwendung von mehreren Rechenzentren. Indem Cluster gestreckt oder repliziert werden, können Workloads in mehreren Rechenzentren ausgeführt werden, um einen schnelleren Datenzugriff für Benutzer und Anwendungen mit der jeweils geringsten Entfernung zu ermöglichen. Gleichzeitig kann die Last besser verteilt, und Computeressourcen können besser genutzt werden. Wenn ein Rechenzentrum in einer Notfallsituation ausfällt, können sie die typischen Workloads dieses Rechenzentrums vorübergehend an einen anderen Standort verlagern.  

Mit Speicherreplikaten können Sie vorhandene Dateireplikationssysteme wie die DFS-Replikation gegebenenfalls außer Betrieb nehmen, die als Low-End-Notfallwiederherstellungslösungen eingesetzt wurden. Wenngleich die DFS-Replikation eine geeignete Lösung für Netzwerke mit äußerst geringer Bandbreite ist, ist die Latenz bei diesem System sehr hoch (häufig liegt diese bei mehreren Stunden oder Tagen). Der Grund dafür ist, dass Dateien geschlossen werden müssen und künstliche Drosselungen implementiert sind, um eine Netzwerküberlastung zu verhindern. Aufgrund dieses Aufbaus werden die neuesten Dateien in einem Replikat der DFS-Replikation mit der geringsten Wahrscheinlichkeit repliziert. Das Speicherreplikatfeature wird unterhalb der Dateiebene ausgeführt, sodass keine dieser Einschränkungen gelten.  

Für größere Bereiche und Netzwerke mit höherer Latenz unterstützt das Speicherreplikatfeature zudem die asynchrone Replikation. Da es ist nicht von Checkpoint-basierte und stattdessen kontinuierlich repliziert werden, ist das Delta Änderungen deutlich geringer als bei Momentaufnahme-basierten Produkten werden. Darüber hinaus wird das Speicherreplikatfeature auf Partitionsebene ausgeführt, sodass alle von Windows Server oder Sicherungssoftware erstellten VSS-Momentaufnahmen repliziert werden. Dadurch können anwendungskonsistente Momentaufnahmen von Daten für eine Zeitpunktwiederherstellung verwendet werden. Dies gilt insbesondere für unstrukturierte Benutzerdaten, die asynchron repliziert wurden.  

## <a name="BKMK_SRSupportedScenarios"></a>Unterstützte Konfigurationen

Sie können die Funktion "Speicherreplikat" in einem Stretched Cluster sowie zwischen Cluster-zu-Cluster, und klicken Sie im Server-zu-Server-Konfigurationen (Siehe Abbildungen 1-3) bereitstellen.

Ein **Stretched Cluster** ermöglicht die Konfiguration von Computern und Speicher innerhalb eines einzigen Clusters, wobei einige Knoten asymmetrischen Speicher und andere Knoten sich gegenseitig gemeinsam verwenden. Die Replikation wird anschließend mit Standortinformationen synchron oder asynchron durchgeführt. In diesem Szenario können Speicherplätze mit freigegebenem SAS-Speicher, SAN und an iSCSI-LUNs verwendet werden. Die Verwaltung erfolgt über PowerShell und das grafische Tool Failovercluster-Manager. Außerdem ist ein automatisiertes Workloadfailover möglich.  

![Diagramm, das zwei Clusterknoten in New York zeigt, die das Speicherreplikat verwenden, um den Speicher von New York mit zwei Knoten in New Jersey zu replizieren](./media/Storage-Replica-Overview/Storage_SR_StretchCluster.png)  

**ABBILDUNG 1: Speicherreplikation in einem Stretched Cluster unter Verwendung von Speicherreplikaten**  

Eine **Cluster-zu-Cluster-Konfiguration** ermöglicht die Replikation zwischen zwei separaten Clustern, wobei ein Cluster synchron oder asynchron in den anderen Cluster repliziert wird. In diesem Szenario können Sie „Direkte Speicherplätze“ und Speicherplätze mit freigegebenem SAS-Speicher, SAN und an iSCSI-LUNs verwendet werden. Es wird mit Windows Admin Center und PowerShell verwaltet und sind manuelle Eingriffe erforderlich für das Failover. 

![Diagramm, das einen Cluster in Los Angeles zeigt, der ein Speicherreplikat verwendet, um den Speicher mit einem anderen Speicher in Las Vegas zu replizieren](./media/Storage-Replica-Overview/Storage_SR_ClustertoCluster.png)  

**ABBILDUNG 2: Cluster-zu-Cluster-Speicherreplikation unter Verwendung von Speicherreplikaten**  

Eine **Server-zu-Server-Konfiguration** ermöglicht eine synchrone und asynchrone Replikation zwischen zwei eigenständigen Servern unter Verwendung von Speicherplätzen mit freigegebenem SAS-Speicher, SAN- und iSCSI-LUNs sowie lokalen Laufwerken. Es wird mit Windows Admin Center und PowerShell verwaltet und sind manuelle Eingriffe erforderlich für das Failover.  

![Diagramm, das einen Server in Gebäude 5 zeigt, der mit einem Server in Gebäude 9 repliziert wird](./media/Storage-Replica-Overview/Storage_SR_ServertoServer.png)  

**ABBILDUNG 3: Server-zu-Server-Speicherreplikation unter Verwendung von Speicherreplikaten**  

> [!NOTE]
> Sie können auch eine Server-to-Self-Replikation konfigurieren, bei der vier separate Volumes auf einem einzigen Computer verwendet werden. Dieses Szenario wird in diesem Leitfaden jedoch nicht abgedeckt.  

## <a name="BKMK_SR2"> </a> Speicherreplikatfeatures  

* **Replikation auf Blockebene ohne Datenverlust**. Bei der synchronen Replikation besteht kein Risiko von Datenverlust. Bei der Replikation auf Blockebene besteht kein Risiko von Dateisperrungen.  

* **Einfache Bereitstellung und Verwaltung**. Das Speicherreplikatfeature wurde von Grund auf für eine hohe Benutzerfreundlichkeit entwickelt. Die Windows Admin Center kann Erstellung eine Replikationspartnerschaft zwischen zwei Servern verwendet werden. Zur Bereitstellung von Stretched Clustern wird der intuitive Assistent des vertrauten Failovercluster-Managers verwendet.   

* **Gast und Host**. Alle Funktionen des Speicherreplikatfeatures werden sowohl in virtualisierten Gast- als auch in hostbasierten Bereitstellungen offengelegt. Dies bedeutet, dass Gäste Datenmengen replizieren können, selbst wenn auf nicht-Windows-Virtualisierungsplattformen oder in öffentlichen Clouds, ausgeführt als Windows Server auf dem Gast zu verwenden.  

* **SMB3-basiert**. Das Speicherreplikatfeature verwendet die bewährte und ausgereifte SMB3-Technologie, die in Windows Server 2012 eingeführt wurde. Das bedeutet, dass alle ausgereiften Merkmale von SMB (z. B. SMB Multichannel- und SMB Direct-Unterstützung für RoCE-, iWARP- und InfiniBand RDMA-Netzwerkkarten) für Speicherreplikate verfügbar sind.   

* **Sicherheit**. Im Gegensatz zu den Produkten vieler anderer Anbieter ist branchenführende Sicherheitstechnologie bereits in das Speicherreplikatfeature integriert. Dies umfasst Paketsignatur, vollständige AES-128-GCM-Datenverschlüsselung, Unterstützung für Intel AES-NI-Verschlüsselungsbeschleunigung sowie Vorauthentifizierung zur Verhinderung von Man-in-the-Middle-Angriffen. Das Speicherreplikatfeature nutzt Kerberos AES256 für die gesamte Authentifizierung zwischen Knoten.  

* **Erste Synchronisierung mit hoher Leistung**. Das Speicherreplikatfeature unterstützt ein Seeding vor der ersten Synchronisierung, wobei auf einem Ziel bereits eine Untermenge von Daten aus älteren Kopien, Sicherungen oder bereitgestellten Laufwerken vorhanden ist. Die erste Replikation kopiert nur die abweichenden Blöcke, potenziell ersten Synchronisierung verkürzt und verhindert, dass Daten Belegung eingeschränkter Bandbreite. Da Speicherreplikate eine Prüfsummenberechnung und Aggregation verhindern, ist die Leistung bei der ersten Synchronisierung lediglich durch die Geschwindigkeit von Speicher und Netzwerk beschränkt.  

* **Konsistenzgruppen**. Schreibreihenfolge gewährleistet, die dass die Anwendungen wie Microsoft SQL Server mit mehreren schreiben können replizierte Volumes und die Daten ist sequenziell geschrieben, auf dem Zielserver.  

* **Benutzerdelegierung**. Benutzern können Berechtigungen zum Verwalten der Replikation zugewiesen werden, ohne dass diese Mitglied der integrierten Administratorengruppe auf den replizierten Knoten sind. Dadurch wird der Zugriff dieser Benutzer auf nicht verknüpfte Bereiche eingeschränkt.  

* **Netzwerkeinschränkung**. Das Speicherreplikatfeature kann durch die Angabe von Servern und replizierten Volumes auf einzelne Netzwerke beschränkt werden, um Bandbreite für Anwendungen, Sicherungen und Verwaltungssoftware bereitzustellen.  

* **Schlanke Speicherzuweisung**. Um in vielen Situationen eine praktisch unmittelbare erste Replikation zu ermöglichen, wird die schlanke Speicherzuweisung für Speicherplätze und SAN-Geräte unterstützt.  

Funktion "Speicherreplikat" enthält die folgenden Features:  

|Feature|Details|  
|-----------|-----------|  
|Typ|Hostbasiert|  
|Synchron|Ja|  
|Asynchron|Ja|  
|Speicherhardwareagnostisch|Ja|  
|Replikationseinheit|Volume (Partition)|  
|Windows Server stretch-Clustererstellung|Ja|  
|Server-zu-Server-Replikation|Ja|  
|Cluster-zu Cluster-Replikation|Ja|  
|Transport|SMB3|  
|Network|TCP/IP oder RDMA|
|Unterstützung für die Netzwerkeinschränkung|Ja|  
|RDMA*|iWARP, InfiniBand, RoCE v2|  
|Netzwerkport-Firewallanforderungen für die Replikation|Einzelner IANA-Port (TCP 445 oder 5445)|  
|Multipath/Multichannel|Ja (SMB3)|  
|Kerberos-Unterstützung|Ja (SMB3)|  
|Verschlüsselung und Signatur über das Netzwerk|Ja (SMB3)|  
|Volumebasiertes Failover zulässig|Ja|
|Unterstützung für die schlanke Speicherzuweisung|Ja|
|Integrierte Verwaltungsbenutzeroberfläche|PowerShell, Failovercluster-Manager|  

*Möglicherweise sind Geräte und Kabel für große Entfernungen erforderlich.  

## <a name="BKMK_SR3"></a> Voraussetzungen für Speicherreplikate  

* Active Directory Domain Services-Gesamtstruktur.
* Speicherplätze mit SAS JBODs, „Direkte Speicherplätze“, Fibre Channel-SAN, freigegebene VHDX, iSCSI-Ziel oder lokalem SAS/SCSI/SATA-Speicher. Für Replikationsprotokolllaufwerke werden mindestens SSDs empfohlen. Microsoft empfiehlt, dass die Protokollspeicherung schneller als die Datenspeicherung durchgeführt wird. Protokollvolumes dürfen niemals für andere Workloads verwendet werden.
* Mindestens eine Ethernet/TCP-Verbindung auf jedem Server für die synchrone Replikation (vorzugsweise RDMA).
* Mindestens 2GB RAM und zwei Kerne pro Server.
* Ein Netzwerk zwischen den Servern mit ausreichender Bandbreite für Ihre E/A-Schreibworkload sowie durchschnittlich 5 ms Roundtriplatenz oder niedriger für die synchrone Replikation. Für die asynchrone Replikation gilt keine Empfehlung bezüglich der Latenz.
* WindowsServer, Datacenter Edition oder WindowsServer Standard Edition. Funktion "Speicherreplikat" auf Windows Server Standard Edition gelten die folgenden Einschränkungen:

  * Sie müssen WindowsServer 2019 oder höher verwenden.
  * Das Speicherreplikat repliziert ein einzelnes Volume, anstatt eine unbegrenzte Anzahl von Volumes.
  * Volumes können eine Größe von bis zu 2 TB, anstatt eine unbegrenzte Größe aufweisen.

##  <a name="BKMK_SR4"> </a> Hintergrund  
Dieser Abschnitt enthält Informationen zu allgemeinen Begriffen aus der Branche, synchroner und asynchroner Replikation und zu Schlüsselverhalten.

### <a name="high-level-industry-terms"></a>Allgemeine branchenübliche Begriffe  
Der Begriff Notfallwiederherstellung bezieht sich auf einen Notfallplan für die Wiederherstellung nach einem Katastrophenfall an einem Standort, damit die Geschäftsvorgänge weiter ausgeführt werden können. Zur Notfallwiederherstellung von Daten werden mehrere Kopien von Produktionsdaten an einem separaten physischen Standort erstellt. Ein Beispiel ist ein Stretched Cluster, bei dem sich die Hälfte der Knoten an einem Standort und die andere Hälfte der Knoten an einem anderen Standort befindet. Der Begriff Notfallbereitschaft bezieht sich auf einen Notfallplan, um Workloads präventiv an einen anderen Standort zu verschieben, bevor eine bevorstehende Notallsituation eintritt (z. B. ein Orkan).  

Vereinbarungen zum Servicelevel (Service Level Agreement, SLA) definieren die Verfügbarkeit der Anwendungen eines Unternehmens sowie die jeweilige Toleranz von Downtime und Datenverlust während geplanten und ungeplanten Ausfällen. Der RTO-Wert (Recovery Time Objective) definiert den maximalen Zeitraum ohne Datenzugriff, der für ein Unternehmen tolerierbar ist. Der RPO-Wert (Recovery Point Objective) definiert die maximale Menge an Daten, die ein Unternehmen verlieren kann.  

### <a name="synchronous-replication"></a>Synchrone Replikation  
Bei der synchronen Replikation wird sichergestellt, dass die Anwendung Daten gleichzeitig an zwei Standorten schreibt, bevor der E/A-Vorgang abgeschlossen wird. Diese Art der Replikation ist für geschäftskritische Daten geeignet, da sowohl Netzwerk- als auch Speicherinvestitionen erforderlich sind. Außerdem geht die synchrone Replikation mit dem Risiko einer eingeschränkten Anwendungsleistung einher.  

Wenn Anwendungsschreibvorgänge für die Quelldatenkopie ausgeführt werden, bestätigt der Ursprungsspeicher die E/A nicht umgehend. Stattdessen werden diese Datenänderungen in die Remotezielkopie repliziert, und es wird eine Bestätigung zurückgegeben. Erst dann empfängt die Anwendung die E/A-Bestätigung. Dadurch wird eine konstante Synchronisierung des Remote- und des Quellstandorts sichergestellt, und Speicher-E/A-Vorgänge werden auf das Netzwerk ausgeweitet. Bei einem Ausfall des Quellstandorts kann ein Anwendungsfailover auf den Remotestandort durchgeführt werden, sodass die Anwendungen ohne Datenverlust weiter ausgeführt werden können.  

|Modus|Diagramm|Schritte|  
|--------|-----------|---------|  
|**Synchrone**<br /><br />Kein Datenverlust<br /><br />RPO|![Diagramm das zeigt, wie das Speicherreplikat Daten in die synchrone Replikation schreibt](./media/Storage-Replica-Overview/Storage_SR_SynchronousV2.png)|1.  Anwendung schreibt Daten<br />2.  Protokolldaten werden geschrieben, und die Daten werden am Remotestandort repliziert<br />3.  Protokolldaten werden am Remotestandort geschrieben<br />4.  Bestätigung durch den Remotestandort<br />5.  Anwendungsschreibvorgang wird bestätigt<br /><br />t & t1: Daten, die auf das Volume geleert Protokolle werden immer geschrieben|  

### <a name="asynchronous-replication"></a>Asynchrone Replikation  
Im Gegensatz zur synchronen Replikation werden die von einer Anwendung geschriebenen Daten bei der asynchronen Replikation ohne umgehende Bestätigung an den Remotestandort repliziert. Dieser Modus ermöglicht kürzere Antwortzeiten für die Anwendung und bietet eine geografisch einsetzbare Notfallwiederherstellungslösung.  

Wenn die Anwendung Daten schreibt, erfasst das Replikationsmodul den Schreibvorgang und bestätigt diesen umgehend gegenüber der Anwendung. Die erfassten Daten werden dann am Remotestandort repliziert. Der Remoteknoten verarbeitet die Kopie der Daten und bestätigt den Vorgang mit einer gewissen Verzögerung gegenüber der Quellkopie. Da der Anwendungs-E/A-Pfad nicht länger für die Replikationsleistung ausschlaggebend ist, sind die Reaktionsfähigkeit und Entfernung des Remotestandorts weniger wichtige Faktoren. Es gibt jedoch ein Risiko von Datenverlust, wenn die Quelldaten nicht mehr verfügbar sind und sich die Zielkopie der Daten noch im Puffer befindet.  

Da der RPO-Wert bei der asynchronen Replikation größer Null ist, ist dieser Replikationstyp für Hochverfügbarkeitslösungen wie Failovercluster weniger gut geeignet. Bei diesen Lösungen sind ein unterbrechungsfreier Betrieb, Redundanz und keinerlei Datenverlust entscheidend.  

|Modus|Diagramm|Schritte|  
|--------|-----------|---------|  
|**Asynchrone**<br /><br />Praktisch keinerlei Datenverlust<br /><br />(von verschiedenen Faktoren abhängig)<br /><br />RPO|![Diagramm das zeigt, wie das Speicherreplikat Daten in die asynchrone Replikation schreibt](./media/Storage-Replica-Overview/Storage_SR_AsynchronousV2.png)|1.  Anwendung schreibt Daten<br />2.  Protokolldaten werden geschrieben<br />3.  Anwendungsschreibvorgang wird bestätigt<br />4.  Daten werden am Remotestandort repliziert<br />5.  Protokolldaten werden am Remotestandort geschrieben<br />6.  Bestätigung durch den Remotestandort<br /><br />t & t1: Daten, die auf das Volume geleert Protokolle werden immer geschrieben|  

### <a name="key-evaluation-points-and-behaviors"></a>Wichtige evaluierungsaspekte und Verhaltensweisen  

-   Netzwerkbandbreite und Latenz bei Speicher mit maximaler Geschwindigkeit. Bei der synchronen Replikation müssen physische Einschränkungen berücksichtigt werden. Da das Speicherreplikat einen E/A-Filtermechanismus unter Verwendung von Protokollen implementiert und Netzwerkroundtrips erforderlich sind, werden Anwendungsschreibvorgänge durch die synchrone Replikation wahrscheinlich langsamer ausgeführt. Verwenden Sie für die Protokolle mit geringer Latenz, Netzwerke mit großer Bandbreite sowie Datenträgersubsystemen mit hohem Durchsatz, minimieren Sie die Performance-Overhead.  

-   Auf das Zielvolume kann während der Replikation in Windows Server 2016 nicht zugegriffen werden. Bei der Konfiguration der Replikation wird die Bereitstellung des Zielvolumes aufgehoben, sodass Benutzer keine Daten auf diese Volumes schreiben oder lesen können. Die Laufwerkbuchstaben werden möglicherweise auf typischen Schnittstellen wie dem Datei-Explorer angezeigt, aber eine Anwendung kann nicht auf das Volume selbst zugreifen. Replikationstechnologien auf Blockebene lassen keinen Zugriff auf das bereitgestellte Dateisystem eines Volumes auf dem Ziel zu. NTFS und ReFS bieten keine Unterstützung für Benutzerschreibvorgänge auf dem Volume, während die zugrunde liegenden Blöcke geändert werden. 

In Windows Server-2019 (und Windows Server, Version 1709) die **Test-Failover** Cmdlet wurde hinzugefügt. Nun unterstützt vorübergehend einen Lese-/ Schreibzugriff-Snapshot des Zielvolumes für Sicherungen zu laden, testen, usw. an. Finden Sie unter https://aka.ms/srfaq für Weitere Informationen.

-   Die Microsoft-Implementierung der asynchronen Replikation unterscheidet sich von den meisten anderen Implementierungen. Bei den meisten Implementierungen der asynchronen Repliktion, die innerhalb der Branche verfügbar sind, basiert die Replikation auf Momentaufnahmen. Dabei werden regelmäßig Differenzen an den anderen Knoten übertragen, auf denen die Daten zusammengeführt werden. Bei der asynchronen Replikation mithilfe des Speicherreplikatfeatures wird der Vorgang wie bei der synchronen Replikation ausgeführt. Die beiden Vorgänge unterscheiden sich einzig dadurch, dass die Notwendigkeit einer serialisierten synchronen Bestätigung durch das Ziel entfällt. Das bedeutet, dass für das Speicherreplikat theoretisch ein niedrigerer RPO-Wert gilt, da die Daten kontinuierlich repliziert werden. Es bedeutet jedoch auch, dass der Vorgang von einer internen Absicherung der Anwendungskonsistenz abhängt, da die Konsistenz der Anwendungsdateien nicht mithilfe von Momentaufnahmen sichergestellt wird. Das Speicherreplikat stellt bei einem Absturz in sämtlichen Replikationsmodi Konsistenz sicher  

-   Viele Kunden verwenden die DFS-Replikation als Notfallwiederherstellungslösung, obwohl dies häufig nicht die ideale Lösung für dieses Szenario ist. Die DFS-Replikation kann keine geöffneten Dateien replizieren und wurde für eine minimierte Bandbreitennutzung entworfen. Dies hat jedoch eine beeinträchtigte Leistung und große Wiederherstellungspunktdeltas zur Folge. Das Speicherreplikat bietet Ihnen die Möglichkeit, die DFS-Replikation gegebenenfalls nicht länger für einige dieser Notfallwiederherstellungsvorgänge einzusetzen.  

-   Funktion "Speicherreplikat" ist keiner backup-Lösung. Da Replikationssysteme einen Datenverlust vollständig verhindern, werden sie in einigen IT-Umgebungen als Sicherungslösungen bereitgestellt und anstelle von täglichen Sicherungen genutzt. Das Speicherreplikat repliziert sämtliche Änderungen an allen Datenblöcken auf dem Volume (unabhängig von der Art der Änderung). Wenn ein Benutzer alle Daten von einem Volume löscht, repliziert Funktion "Speicherreplikat" den Löschvorgang umgehend auf das andere Volume, entfernen die Daten unwiderruflich von beiden Servern. Verwenden Sie das Speicherreplikat nicht als Ersatz für eine Zeitpunktsicherungslösung.  

-   Das Speicherreplikatfeature darf nicht mit Hyper-V-Replikaten oder Microsoft SQL AlwaysOn-Verfügbarkeitsgruppen verwechselt werden. Das Speicherreplikatfeature ist ein allgemeines speicheragnostisches Modul. Sein Verhalten kann nicht so optimal angepasst werden wie bei der Replikation auf Anwendungsebene. Dies kann bestimmte Featurelücken mit sich bringen, aufgrund derer Sie sich weiterhin für bestimmte Anwendungsreplikationstechnologien entscheiden.  

> [!NOTE]
> In diesem Dokument finden Sie eine Liste mit [bekannten Problemen](storage-replica-known-issues.md) und erwarteten Verhaltensweisen sowie einen Abschnitt mit [häufig gestellten Fragen](storage-replica-frequently-asked-questions.md).
 
### <a name="storage-replica-terminology"></a>Terminologie im Zusammenhang mit Speicherreplikaten  
In diesem Leitfaden werden folgende Begriffe häufig verwendet:  

-   Die Quelle ist das Volume eines Computers, das lokale Schreibvorgänge ermöglicht und eine ausgehende Replikation durchführt. Es wird auch als „primäres Volume“ bezeichnet.  

-   Das Ziel ist das Volume eines Computers, das keine lokalen Schreibvorgänge ermöglicht und eine eingehende Replikation durchführt. Es wird auch als „sekundäres“ Volume bezeichnet.   

-   Eine Replikationspartnerschaft ist die Synchronisierungsbeziehung zwischen einem Quell- und einem Zielcomputer für mindestens ein Volume, für die ein einziges Protokoll verwendet wird.  

-   Eine Replikationsgruppe ist die Organisation der Volumes sowie der zugehörigen Replikationskonfiguration innerhalb einer Partnerschaft und gilt pro Server. Eine Gruppe kann ein oder mehrere Volumes umfassen.  

### <a name="whats-new-for-storage-replica"></a>Was ist neu in Funktion "Speicherreplikat"

Eine Liste der neuen Funktionen in der Funktion "Speicherreplikat" in Windows Server-2019, finden Sie unter [Neuigkeiten im Speicher](../whats-new-in-storage.md#storage-replica2019)

## <a name="see-also"></a>Siehe auch
- [Replikation eines Stretched Clusters mithilfe von freigegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)  
- [Server-zu-Server-Replikation](server-to-server-storage-replication.md)  
- [Cluster-zu-Cluster-Speicherreplikation](cluster-to-cluster-storage-replication.md)  
- [Speicherreplikat: Bekannte Probleme](storage-replica-known-issues.md)  
- [Speicherreplikat: Häufig gestellte Fragen](storage-replica-frequently-asked-questions.md)  
- ["Direkte Speicherplätze" unter WindowsServer 2016](../storage-spaces/storage-spaces-direct-overview.md)
- [Windows IT Pro-Support](https://www.microsoft.com/itpro/windows/support)
