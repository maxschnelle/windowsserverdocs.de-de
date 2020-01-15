---
ms.assetid: 350aa5a3-5938-4921-93dc-289660f26bad
title: Neues beim Failoverclustering unter Windows Server
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: get-started-article
manager: dongill
author: JasonGerend
ms.author: jgerend
ms.date: 10/18/2018
ms.openlocfilehash: 40342f43f7afbf020ba20f27586650767218fe83
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75948030"
---
# <a name="whats-new-in-failover-clustering"></a>Neuigkeiten in Failoverclustering

> Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema werden die neuen und geänderten Funktionen in Failoverclustering für Windows Server 2019 und Windows Server 2016 erläutert.

## <a name="whats-new-in-windows-server-2019"></a>Neuerungen in Windows Server 2019

- **Clustergruppen**

    Cluster Gruppen ermöglichen es Ihnen, die Anzahl der Server in einer einzelnen SDDC-Lösung (Software-Defined Datacenter) über die aktuellen Grenzwerte eines Clusters hinaus zu erhöhen. Dies wird erreicht, indem mehrere Cluster zu einem Cluster Satz gruppiert werden: eine lose gekoppelte Gruppierung mehrerer Failovercluster: COMPUTE, Speicher und hyperkonvergiert.
    Mit Cluster Sätzen können Sie virtuelle Online Computer (Live Migration) zwischen Clustern innerhalb des Cluster Satzes verschieben.

    Weitere Informationen finden Sie unter [Cluster Sets](../storage/storage-spaces/cluster-sets.md).

- **Azure erkennende Cluster**

    Failovercluster erkennen nun automatisch, wenn Sie auf virtuellen Azure-IaaS-Computern ausgeführt werden, und optimieren die Konfiguration, um ein proaktives Failover und die Protokollierung von geplanten Azure-Wartungs Ereignissen bereitzustellen, um die höchste Verfügbarkeit zu erreichen Die Bereitstellung wird auch vereinfacht, da der Load Balancer mit dem dynamischen Netzwerknamen für den Cluster Namen nicht konfiguriert werden muss.

- **Domänenübergreifende Clustermigration**

    Failovercluster können nun dynamisch von einer Active Directory Domäne zu einer anderen migrieren, sodass die Domänen Konsolidierung vereinfacht wird und Cluster von Hardwarepartnern erstellt und später der Kunden Domäne hinzugefügt werden können.
- **USB-Zeugen**

    Sie können jetzt ein einfaches USB-Laufwerk, das mit einem Netzwerk Switch verbunden ist, als Zeuge zum Ermitteln des Quorums für einen Cluster verwenden. Dadurch wird der Datei frei gaben Zeuge erweitert, um beliebige SMB2-kompatible Geräte zu unterstützen.

- **Verbesserungen der Clusterinfrastruktur**

    Der CSV-Cache ist jetzt standardmäßig aktiviert, um die Leistung virtueller Computer zu steigern. MSDTC unterstützt nun Cluster Shared Volumes, um die Bereitstellung von MSDTC-Workloads auf Storage Spaces Direct, z. B. mit SQL Server, zu ermöglichen. Verbesserte Logik zum Erkennen von partitionierten Knoten mit Selbstkorrektur, um Knoten zur Clustermitgliedschaft zurückzugeben. Verbesserte Erkennung von Clusternetzwerkrouten und Selbstkorrektur.

- **Clusterfähiges Aktualisieren unterstützt „Direkte Speicherplätze“**

    Cluster Aware Updating (CAU) ist nun integriert und berücksichtigt Storage Spaces Direct, wodurch die Datensynchronisierung auf jedem Knoten überprüft und sichergestellt wird. Das Cluster fähige aktualisieren prüft Updates auf einen intelligenten Neustart, wenn dies erforderlich ist. Dies ermöglicht das orchestrieren von Neustarts aller Server im Cluster für eine geplante Wartung.

- **Erweiterungen des Dateifreigabe Zeugen** Wir haben die Verwendung eines Dateifreigabe Zeugen in den folgenden Szenarien aktiviert: 
  - Fehlender oder sehr schlechter Internet Zugriff aufgrund eines Remote Standorts, der die Verwendung eines cloudzeugen verhindert. 
  - Fehlende freigegebene Laufwerke für einen Datenträger Zeugen. Dabei kann es sich um eine direkte Speicherplätze hyperkonvergierte Konfiguration, eine SQL Server Always on Verfügbarkeits Gruppen (AG) oder eine * Exchange-Daten Bank Verfügbarkeits Gruppe (DAG) handeln, von denen keine freigegebene Datenträger verwendet. 
  - Fehlende Domänen Controller Verbindung, weil der Cluster hinter einer DMZ liegt. 
  - Eine Arbeitsgruppe oder ein Domänen übergreifender Cluster, für die kein Active Directory Cluster Namen Objekt (CNO) vorhanden ist. Weitere Informationen zu diesen Verbesserungen finden Sie im folgenden Beitrag in Server & Management-Blogs: Failovercluster-Dateifreigabe Zeuge und DFS.
    
    Außerdem wird die Verwendung einer DFS-Namespaces-Freigabe explizit als Speicherort blockiert. Das Hinzufügen eines Dateifreigabe Zeugen zu einer DFS-Freigabe kann zu Stabilitätsproblemen für Ihren Cluster führen, und diese Konfiguration wurde nie unterstützt. Wir haben Logik hinzugefügt, um zu erkennen, ob eine Freigabe DFS-Namespaces verwendet. Wenn DFS-Namespaces erkannt werden, blockiert Failovercluster-Manager die Erstellung des Zeugen und zeigt eine Fehlermeldung an, die nicht unterstützt wird.
- **Clusterhärtung**

    Die Intra-Cluster-Kommunikation über SMB (Server Message Block) für freigegebene Clustervolumes und Storage Spaces Direct nutzt jetzt Zertifikate, um die sicherste Plattform bereitzustellen. Dadurch können Failovercluster ohne Abhängigkeiten von NTLM arbeiten und Sicherheitsbasislinien aktivieren.
- **Failovercluster verwendet keine NTLM-Authentifizierung mehr**

    Failovercluster verwenden nicht mehr die NTLM-Authentifizierung. Stattdessen wird die Kerberos-Authentifizierung und die Zertifikat basierte Authentifizierung exklusiv verwendet. Für den Benutzer oder die Bereitstellungs Tools sind keine Änderungen erforderlich, um diese Sicherheits Erweiterung nutzen zu können. Außerdem können Failovercluster in Umgebungen bereitgestellt werden, in denen NTLM deaktiviert wurde. 


## <a name="whats-new-in-windows-server-2016"></a>Neuerungen in Windows Server 2016

### <a name="BKMK_RollingUpgrade"></a>Paralleles Upgrade des Cluster Betriebssystems

Das parallele Upgrade des Cluster Betriebssystems ermöglicht einem Administrator, das Betriebssystem der Cluster Knoten von Windows Server 2012 R2 auf eine neuere Version zu aktualisieren, ohne die Hyper-V-oder die Dateiserver mit horizontaler Skalierung Arbeits Auslastungen zu beenden. Mit diesem Feature können die Downtimesanktionen laut Vereinbarungen zum Servicelevel (Service Level Agreements, SLA) vermieden werden. 

**Welchen Nutzen bietet diese Änderung?**  

Zum Aktualisieren eines Hyper-V-oder Dateiserver mit horizontaler Skalierung Clusters von Windows Server 2012 R2 auf Windows Server 2016 sind keine Ausfallzeiten mehr erforderlich. Der Cluster funktioniert weiterhin auf Windows Server 2012 R2-Ebene, bis auf allen Knoten im Cluster Windows Server 2016 ausgeführt wird. Die Cluster Funktionsebene wird mithilfe der Windows PowerShell-Cmdlet-`Update-ClusterFunctionalLevel`auf Windows Server 2016 aktualisiert. 

> [!WARNING]  
> -   Nachdem Sie die Cluster Funktionsebene aktualisiert haben, können Sie nicht mehr zu einer Windows Server 2012 R2-Cluster Funktionsebene zurückkehren. 
> -   Bis zum Ausführen des Cmdlets "`Update-ClusterFunctionalLevel`" wird der Prozess rückgängig gemacht, und Windows Server 2012 R2-Knoten können hinzugefügt werden, und Windows Server 2016-Knoten können entfernt werden. 

**Worin bestehen die Unterschiede?**  

Ein Hyper-V-oder Dateiserver mit horizontaler Skalierung-Failovercluster kann jetzt problemlos ohne Ausfallzeiten aktualisiert werden, oder es muss ein neuer Cluster mit Knoten erstellt werden, auf denen das Betriebssystem Windows Server 2016 ausgeführt wird. Beim Migrieren von Clustern zu Windows Server 2012 R2 wurde der vorhandene Cluster offline geschaltet, und das neue Betriebssystem wird für jeden Knoten neu installiert, und der Cluster wird wieder online geschaltet. Der alte Prozess war mühsam und erforderte Ausfallzeiten. In Windows Server 2016 muss der Cluster jedoch zu keinem Zeitpunkt offline geschaltet werden. 

Die Cluster Betriebssysteme für das Upgrade in Phasen lauten wie folgt für jeden Knoten in einem Cluster:  
-   Der Knoten wird angehalten und auf allen virtuellen Computern, auf denen er ausgeführt wird, entladen. 
-   Die virtuellen Computer (oder eine andere Cluster Arbeitsauslastung) werden zu einem anderen Knoten im Cluster migriert. 
-   Das vorhandene Betriebssystem wird entfernt, und es wird eine Neuinstallation des Betriebssystems Windows Server 2016 auf dem Knoten ausgeführt. 
-   Der Knoten, auf dem das Betriebssystem Windows Server 2016 ausgeführt wird, wird wieder zum Cluster hinzugefügt. 
-   An diesem Punkt wird der Cluster als im gemischten Modus ausgeführt, da auf den Cluster Knoten entweder Windows Server 2012 R2 oder Windows Server 2016 ausgeführt wird. 
-   Die Cluster Funktionsebene bleibt bei Windows Server 2012 R2. Auf dieser Funktionsebene sind neue Features in Windows Server 2016, die sich auf die Kompatibilität mit früheren Versionen des Betriebssystems auswirken, nicht verfügbar. 
-   Schließlich werden alle Knoten auf Windows Server 2016 aktualisiert. 
-   Die Cluster Funktionsebene wird dann mithilfe des Windows PowerShell-Cmdlets `Update-ClusterFunctionalLevel`in Windows Server 2016 geändert. An diesem Punkt können Sie die Features von Windows Server 2016 nutzen. 

Weitere Informationen finden Sie unter [Cluster Operating System Rolling Upgrade](cluster-operating-system-rolling-upgrade.md). 

### <a name="BKMK_SR"></a>Speicher Replikat  
Das Speicher Replikat ist ein neues Feature, das Speicher agnostische, synchrone Replikation auf Blockebene zwischen Servern oder Clustern für die Notfall Wiederherstellung sowie das Strecken eines Failoverclusters Zwischenstand Orten ermöglicht. Die synchrone Replikation ermöglicht die Spiegelung von Daten an physischen Standorten mit ausfallsicheren Volumes, um auf Dateisystemebene sicherzustellen, dass kein Datenverlust auftritt. Asynchrone Replikation ermöglicht die Standorterweiterung über regionale Bereiche hinaus mit der Möglichkeit von Datenverlusten. 

**Welchen Nutzen bietet diese Änderung?**  

Mithilfe des Speicher Replikats können Sie folgende Aufgaben ausführen:  

-   Bereitstellen einer Notfallwiederherstellungslösung von einem einzigen Anbieter für geplante und ungeplante Ausfälle unternehmenskritischer Workloads. 

-   Verwenden des SMB3-Transportprotokolls mit bewährter Zuverlässigkeit, Skalierbarkeit und Leistung. 

-   Strecken von Windows-Failoverclustern über regionale Bereiche hinweg. 

-   Verwenden Sie Microsoft-Software End-to-End für Speicherung und Clustering, wie z. b. Hyper-V, Speicher Replikat, Speicherplätze, Cluster, Dateiserver mit horizontaler Skalierung, SMB3, Datendeduplizierung und Refs/NTFS. 

-   Aufgrund der folgenden Merkmale können Sie die Kosten und die Komplexität senken:  

    -   Hardwareagnostisches System, das keine spezifische Speicherkonfiguration wie DAS oder SAN benötigt. 

    -   Möglichkeit, allgemeine Speicher- und Netzwerktechnologien zu nutzen. 

    -   Problemlose grafische Verwaltung für einzelne Knoten und Cluster über den Failovercluster-Manager. 

    -   Umfangreiche Skriptoptionen über Windows PowerShell. 

-   Weniger Downtime sowie höhere Zuverlässigkeit und Produktivität dank Windows. 

-   Unterstützbarkeit, Leistungsmetriken und Diagnosefunktionen. 

Weitere Informationen finden Sie unter [Speicherreplikate in Windows Server 2016](../storage/storage-replica/storage-replica-overview.md). 


### <a name="BKMK_CloudWitness"></a>Cloudzeuge  
Der Cloudzeuge ist ein neuer Failovercluster-Quorumzeugen-Typ in Windows Server 2016, der Microsoft Azure als Vermittlungspunkt nutzt. Der Cloudzeuge erhält wie jeder andere Quorumzeuge ein Votum und kann an der Quorumberechnung teilnehmen. Sie können den Cloudzeugen als Quorumzeugen konfigurieren, indem Sie den Assistenten zum Konfigurieren eines Clusterquorums verwenden. 

**Welchen Nutzen bietet diese Änderung?**  

Die Verwendung des cloudzeugen als Failovercluster-Quorum Zeugen bietet die folgenden Vorteile:  

-   Nutzt Microsoft Azure und entfällt, dass ein drittes separates Daten Center benötigt wird. 

-   Verwendet den standardmäßigen öffentlich verfügbaren Microsoft Azure BLOB Storage der den zusätzlichen Wartungsaufwand von virtuellen Computern, die in einem Public Cloud gehostet werden, entfällt. 

-   Dasselbe Microsoft Azure Storage Konto kann für mehrere Cluster verwendet werden (eine BLOB-Datei pro Cluster; eindeutige Cluster-ID, die als BLOB-Dateiname verwendet wird). 

-   Bietet sehr niedrige Kosten für das Speicherkonto (sehr kleine Daten, die pro BLOB-Datei geschrieben werden, BLOB-Dateien werden nur einmal aktualisiert, wenn sich der Status der Cluster Knoten ändert). 

Weitere Informationen finden Sie unter Bereitstellen [eines cloudzeugen für einen Failovercluster](deploy-cloud-witness.md). 

**Worin bestehen die Unterschiede?**  

Dies ist eine neue Funktion in Windows Server 2016. 

### <a name="BKMK_VMs"></a>Resilienz virtueller Computer  
**Computeresilienz** Windows Server 2016 umfasst höhere computeresilienz von virtuellen Computern, um Probleme bei der Cluster Kommunikation in Ihrem Computecluster wie folgt zu reduzieren: 

-   **Resilienzoptionen, die für virtuelle Computer verfügbar sind:**  Nun können Sie die resilienzoptionen für virtuelle Computer konfigurieren, die das Verhalten der virtuellen Computer während vorübergehender Fehler definieren:  

    -   **Resilienzstufe:** Unterstützt Sie beim Definieren der Behandlung vorübergehender Fehler. 

    -   **Resilienzzeitraum:**  Hilft Ihnen bei der Definition, wie lange alle virtuellen Computer isoliert ausgeführt werden dürfen. 

-   **Quarantäne fehlerhafter Knoten:** Fehlerhafte Knoten werden unter Quarantäne gestellt und sind nicht mehr berechtigt, dem Cluster beizutreten. Dadurch wird verhindert, dass Knoten in anderen Knoten und dem gesamten Cluster negativ beeinflusst werden. 

Weitere Informationen finden Sie unter Compute resilienzworkflow und Knoten Quarantäne Einstellungen, mit denen gesteuert wird, wie der Knoten isoliert oder isoliert wird. Weitere Informationen finden Sie unter computeressourcen für [virtuelle Computer in Windows Server 2016](https://blogs.msdn.com/b/clustering/archive/2015/06/03/10619308.aspx). 

**Speicherresilienz** In Windows Server 2016 sind virtuelle Computer stabiler für vorübergehende Speicher Ausfälle. Durch die verbesserte Resilienz virtueller Computer werden die Sitzungs Zustände der Mandanten-virtuellen Computer im Falle einer Speicher Unterbrechung beibehalten. Dies wird durch eine intelligente und schnelle Reaktion von virtuellen Computern auf Probleme mit der Speicherinfrastruktur erreicht. 

Wenn ein virtueller Computer die Verbindung mit dem zugrunde liegenden Speicher trennt, hält er an und wartet auf die Wiederherstellung des Speichers. Bei angehaltenen Computern behält der virtuelle Computer den Kontext der Anwendungen bei, die darin ausgeführt werden. Wenn die Verbindung des virtuellen Computers mit dem Speicher wieder hergestellt wird, wird der virtuelle Computer wieder in den Status "wird ausgeführt" zurückversetzt. Folglich wird der Sitzungs Status des Mandanten Computers bei der Wiederherstellung beibehalten. 

In Windows Server 2016 ist die Resilienz von Speicher für virtuelle Computer für Gast Cluster auch bekannt und optimiert. 

### <a name="BKMK_Diagnostics"></a>Diagnose Verbesserungen bei Failoverclustering  
Zum Diagnostizieren von Problemen mit Failoverclustern umfasst Windows Server 2016 Folgendes:  

-   Mehrere Verbesserungen an Cluster Protokolldateien (z. b. Zeitzoneninformationen und diagnosticverbose-Protokoll), die das Beheben von Problemen mit dem Failoverclustering erleichtern. Weitere Informationen finden Sie unter [Windows Server 2016-Failovercluster-Problembehandlung bei Verbesserungen-Cluster Protokoll](https://blogs.msdn.com/b/clustering/archive/2015/05/15/10614930.aspx). 

-   Ein neuer dumptyp des **aktiven Speicher Abbilds**, das die meisten Speicherseiten filtert, die virtuellen Maschinen zugeordnet sind. Dadurch wird der Speicher. dmp wesentlich kleiner und leichter zu speichern oder zu kopieren. Weitere Informationen finden Sie unter [Verbesserungen bei der Problembehandlung für Windows Server 2016-Failovercluster-aktives Dump](https://blogs.msdn.com/b/clustering/archive/2015/05/18/10615526.aspx) 

### <a name="BKMK_SiteAware"></a>Site abhängige Failovercluster  
Windows Server 2016 umfasst standortabhängige Failovercluster, die Gruppenknoten in gestreckten Clustern basierend auf dem physischen Standort (Standort) aktivieren. Cluster Site-Awareness erweitert wichtige Vorgänge während des Cluster Lebenszyklus, z. b. Failoververhalten, Platzierungs Richtlinien, Takt zwischen den Knoten und Quorum Verhalten. Weitere Informationen finden Sie unter [Site-Aware Failover Clusters in Windows Server 2016](https://blogs.msdn.com/b/clustering/archive/2015/08/19/10636304.aspx). 

### <a name="BKMK_multidomainclusters"></a>Arbeitsgruppen und Cluster mit mehreren Domänen  
In Windows Server 2012 R2 und früheren Versionen kann ein Cluster nur zwischen Mitglieds Knoten erstellt werden, die mit derselben Domäne verknüpft sind. Windows Server 2016 beseitigt diese Hindernisse und führt die Möglichkeit zum Erstellen eines Failoverclusters ohne Active Directory-Abhängigkeiten ein. Sie können jetzt in den folgenden Konfigurationen Failovercluster erstellen:  

-   **Einzel Domänen Cluster.** Cluster mit allen Knoten, die mit derselben Domäne verknüpft sind. 

-   **Cluster mit mehreren Domänen.** Cluster mit Knoten, die Mitglieder von unterschiedlichen Domänen sind. 

-   **Arbeitsgruppen Cluster.** Cluster mit Knoten, die Mitglied Server/Arbeitsgruppe sind (nicht mit der Domäne verknüpft). 

Weitere Informationen finden Sie unter [Arbeitsgruppe und Cluster mit mehreren Domänen in Windows Server 2016](https://blogs.msdn.com/b/clustering/archive/2015/08/17/10635825.aspx) .  
### <a name="BKMK_VMLoadBalancing"></a>Lastenausgleich für virtuelle Computer  
Der Lastenausgleich für virtuelle Computer ist ein neues Feature in Failoverclustering, das den nahtlosen Lastenausgleich virtueller Maschinen über die Knoten in einem Cluster hinweg ermöglicht. Über belegte Knoten werden basierend auf dem Arbeitsspeicher der virtuellen Maschine und der CPU-Auslastung auf dem Knoten identifiziert. Virtuelle Computer werden dann (Live migriert) von einem übergeordneten Knoten zu Knoten mit verfügbarer Bandbreite (falls zutreffend) verschoben. Die Aggressivität des Ausgleichs kann optimiert werden, um eine optimale Leistung und Auslastung des Clusters sicherzustellen. Der Lastenausgleich ist in Windows Server 2016 Technical Preview standardmäßig aktiviert. Der Lastenausgleich ist jedoch deaktiviert, wenn die dynamische SCVMM-Optimierung aktiviert ist. 

### <a name="BKMK_VMStartOrder"></a>Start Reihenfolge der virtuellen Maschine  
Die Start Reihenfolge des virtuellen Computers ist ein neues Feature in Failoverclustering, das die Orchestrierung starten für virtuelle Computer (und alle Gruppen) in einem Cluster einführt. Virtuelle Computer können nun in Ebenen gruppiert werden, und es können Start Auftrags Abhängigkeiten zwischen unterschiedlichen Ebenen erstellt werden. Dadurch wird sichergestellt, dass die wichtigsten virtuellen Computer (z. b. Domänen Controller oder virtuelle Computer des-Hilfsprogramms) zuerst gestartet werden. Virtuelle Computer werden erst gestartet, wenn die virtuellen Maschinen, von denen Sie abhängig sind, ebenfalls gestartet werden. 

### <a name="BKMK_SMBMultiChannel"></a>Vereinfachte SMB Multichannel-und Multi-NIC-Cluster Netzwerke  
Failoverclusternetzwerke sind nicht mehr auf eine einzelne NIC pro Subnetz/Netzwerk beschränkt. Bei vereinfachten SMB Multichannel-und Multi-NIC-Cluster Netzwerken erfolgt die Netzwerkkonfiguration automatisch, und jede NIC im Subnetz kann für Cluster-und workloaddatenverkehr verwendet werden. Diese Erweiterung ermöglicht es Kunden, den Netzwerk Durchsatz für Hyper-V, SQL Server-Failoverclusterinstanz und andere SMB-Arbeits Auslastungen zu maximieren. 

Weitere Informationen finden Sie unter [vereinfachte SMB Multichannel-und Multi-NIC-Cluster Netzwerke](smb-multichannel.md).

## <a name="see-also"></a>Siehe auch  
* [Speicher](../storage/storage.md)  
* [Neuerungen beim Speicher in Windows Server 2016](../storage/whats-new-in-storage.md)  
