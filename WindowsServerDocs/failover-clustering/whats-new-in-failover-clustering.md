---
ms.assetid: 350aa5a3-5938-4921-93dc-289660f26bad
title: Neues beim Failoverclustering in Windows Server
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: get-started-article
manager: dongill
author: JasonGerend
ms.author: jgerend
ms.date: 10/11/2016
ms.openlocfilehash: a4330f62095e13f2f4736f15924ed31fb4893e7a
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="whats-new-in-failover-clustering-in-windows-server-2016"></a>Neues beim Failoverclustering in Windows Server2016
> Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema werden die neue und geänderte Funktionen im Failoverclustering in Windows Server2016.  

## <a name="BKMK_RollingUpgrade"></a>Cluster Operating System Rolling Upgrade  
Ein neues Feature in der Failover-Clusterunterstützung Cluster Operating System Rolling Upgrade, kann ein Administrator des Betriebssystems des Clusterknotens von Windows Server2012 R2 auf Windows Server2016 aktualisieren, ohne eine Unterbrechung von Hyper-V- oder Workloads des Dateiservers mit horizontaler Skalierung durchzuführen. Mit diesem Feature können die downtimesanktionen gegen Service LevelAgreements (SLA) vermieden werden.  

**Hinzufügen der Wert diese Änderung?**  

Aktualisieren eines Clusters Hyper-V- oder Dateiserver mit horizontaler Skalierung in Windows Server2012 R2 zu Windows Server2016 nicht mehr ist Ausfallzeit erforderlich. Cluster werden weiterhin Ebene der Windows Server2012 R2 ausgeführt wird, bis alle Knoten im Cluster die Windows Server2016 ausgeführt werden. Die Funktionsebene der Cluster wird mithilfe der Windows PowerShell-Cmdlet zu Windows Server2016 aktualisiert `Update-ClusterFunctionalLevel`.  

> [!WARNING]  
> -   Nachdem Sie die Funktionsebene der Cluster aktualisiert haben, können keine wechseln Sie zurück auf einer Funktionsebene der Windows Server2012 R2-Cluster.  
> -   Bis die `Update-ClusterFunctionalLevel`Cmdlet ausgeführt wird, der Prozess umkehrbar ist, und Windows Server2012 R2-Knoten hinzugefügt werden können und Windows Server2016-Knoten entfernt werden können.  

**Worin bestehen die Unterschiede?**  

Ein Failovercluster für Hyper-V- oder Dateiserver mit horizontaler Skalierung kann nun problemlos aktualisiert werden, ohne Downtime oder ein neues Clusters mit Knoten zu erstellen, die das Betriebssystem Windows Server2016 ausgeführt werden müssen. Migrieren von Clustern zu Windows Server2012 R2 beteiligt den vorhandenen Cluster offline geschaltet und installieren das neue Betriebssystem für jeden Knoten den Cluster wieder online schalten. Das alte war mühsam und erforderliche Downtime. Jedoch in Windows Server2016 muss der Cluster nicht zu jedem beliebigen Zeitpunkt offline geschaltet.  

Die Cluster-Betriebssysteme für das Upgrade in mehreren Phasen sind wie folgt für jeden Knoten in einem Cluster:  
-   Der Knoten angehalten und leer aller virtuellen Computer, die darauf ausgeführt werden.  
-   Die virtuellen Computer (oder andere clusterarbeitsauslastung) werden auf einen anderen Knoten im Cluster Cluster.The virtuellen Maschinen werden auf einen anderen Knoten im Cluster migriert.  
-   Das vorhandene Betriebssystem wird entfernt, und eine Neuinstallation des Betriebssystems Windows Server2016 auf dem Knoten erfolgt.  
-   Der Knoten, auf denen das Betriebssystem Windows Server2016 wird wieder zum Cluster hinzugefügt.  
-   An diesem Punkt wird der Cluster bezeichnet im gemischten Modus ausgeführt werden, da die Cluster-Knoten Windows Server2012 R2 oder Windows Server2016 ausgeführt werden.  
-   Die Funktionsebene der Cluster bleibt bei Windows Server2012 R2. Diese Funktionsebene werden neue Features in Windows Server2016, die Einfluss auf Kompatibilität mit früheren Versionen des Betriebssystems nicht verfügbar.  
-   Zu einem späteren Zeitpunkt werden alle Knoten auf Windows Server2016 aktualisiert.  
-   Cluster-Funktionsebene ist dann in Windows Server2016 mithilfe von Windows PowerShell-Cmdlets geändert `Update-ClusterFunctionalLevel`. An diesem Punkt können Sie die Windows Server2016-Features nutzen.  

Weitere Informationen finden Sie unter [Cluster Operating System Rolling Upgrade ](cluster-operating-system-rolling-upgrade.md).  

## <a name="BKMK_SR"></a>Das Speicherreplikatfeature  
Speicherreplikate sind ein neues Feature, das speicheragnostische ermöglicht, die auf Blockebene, synchrone Replikation zwischen Servern oder Clustern für die notfallwiederherstellung sowie das Strecken eines Failoverclusters zwischen Standorten. Synchrone Replikation ermöglicht die Spiegelung von Daten an physischen Standorten mit ausfallsicheren Volumes, um sicherzustellen, dass kein Datenverlust auf der Ebene des Dateisystems. Die asynchrone Replikation ermöglicht die standorterweiterung über regionale Bereiche mit der Möglichkeit von Datenverlusten hinaus.  

**Hinzufügen der Wert diese Änderung?**  

Von Speicherreplikaten können Sie die folgenden Schritteausführen:  

-   Bereitstellen eine einzelnen Hersteller Disaster Recovery-Lösung für geplante und ungeplante Ausfälle unternehmenskritischer Workloads.  

-   Verwenden Sie SMB3-Transportprotokolls mit bewährter Zuverlässigkeit, Skalierbarkeit und Leistung.  

-   Vergrößern Sie die Windows-Failoverclustern über regionale Bereiche hinweg.  

-   Verwenden Sie Microsoft-Software für die gesamte Speicher- und Clusterumgebung, z.B. Hyper-V, Speicherreplikate, Speicherplätze, Cluster, Dateiserver mit horizontaler Skalierung, SMB3, der Datendeduplizierung und ReFS/NTFS.  

-   Verringern Sie Kosten und Komplexität wie folgt:  

    -   Unabhängigkeit von der Hardware, keine Anforderung für eine spezifische Speicherkonfiguration wie DAS oder SAN-Inseln  

    -   Möglichkeit, allgemeine Speicher- und Netzwerkhardware Technologien.  

    -   Problemlose grafische Verwaltung für einzelne Knoten und Cluster mit Failovercluster-Manager.  

    -   Enthält umfangreiche Skriptoptionen über Windows PowerShell.  

-   Weniger Downtime sowie höhere Zuverlässigkeit und Produktivität dank Windows-Hilfe.  

-   Stellen Sie Wartungsfreundlichkeit, Leistungsmetriken und Diagnosefunktionen.  

Weitere Informationen finden Sie in der [Storage Replica in Windows Server2016](../storage/storage-replica/storage-replica-overview.md).  


## <a name="BKMK_CloudWitness"></a>Cloudzeuge  
Cloudzeuge ist ein neuer Typ von Failoverclusterquorum-Zeuge in Windows Server2016, die Microsoft Azure als Vermittlungspunkt nutzt. Der Cloudzeuge wie jeder andere quorumzeuge eine Stimme abgerufen und an der quorumberechnung teilnehmen kann. Sie können den cloudzeugen als quorumzeugen-Konfiguration einer Cluster-Quorum-Assistent konfigurieren.  

**Hinzufügen der Wert diese Änderung?**  

Mithilfe von Cloudzeugen als Failovercluster-quorumzeugen bietet die folgenden Vorteile:  

-   Nutzt Microsoft Azure und entfällt die Notwendigkeit für eine dritte separaten Datencenter.  

-   Mithilfe der standardmäßigen öffentlich verfügbaren Microsoft Azure BLOB-Speicher die nicht den zusätzlichen Verwaltungsaufwand der virtuellen Maschinen in einer öffentlichen Cloud gehostet werden.  

-   Microsoft Azure Storage-Konto kann für mehrere Cluster (ein Blobdatei pro Cluster; Cluster eindeutige ID, die als BLOB--Dateiname) verwendet werden.  

-   Enthält nur noch sehr wenig laufende Kosten für das Storage-Konto (sehr kleinen Daten geschrieben pro BLOB-Datei, BLOB-Datei aktualisiert wird, nur einmal Wenn Clusterknoten-Zustand ändert).  

Weitere Informationen finden Sie unter [eine Cloud Witness für einen Failovercluster bereitstellen ](deploy-cloud-witness.md).  

**Worin bestehen die Unterschiede?**  

Diese Funktion ist neu in Windows Server2016.  

## <a name="BKMK_VMs"></a>VM-Resilienz  
**Berechnen der Resilienz** Windows Server2016 enthält mehr virtuelle Maschinen Compute Resilienz zur Verringerung von Kommunikationsproblemen in Ihrem Computecluster innerhalb des Clusters wie folgt: 

-   **Resilienz Optionen für virtuelle Maschinen verfügbar:** können Sie jetzt virtuelle Maschine Resilienz Optionen, die Verhalten der virtuellen Computer während der vorübergehende Fehler definieren konfigurieren:  

    -   **Resilienzgrad:** können Sie festlegen, wie die vorübergehende Fehler behandelt werden.  

    -   **Resilienz Zeitraum:** können Sie festlegen, wie lange von den virtuellen Computern isoliert ausgeführt werden dürfen.  

-   **Isolieren von fehlerhaften Knoten:** fehlerhafte Knoten werden unter Quarantäne gestellt und dürfen nicht mehr auf dem Cluster nicht beitreten. Dadurch wird verhindert, dass Flügelschlagen Knoten negativ beeinflusst, andere Knoten und den gesamten Cluster.  

Weitere Informationen Compute Resilienz Workflow und Knoten Quarantäne Einstellungen des virtuellen Computers, die steuern, wie Ihre Knoten Isolation oder unter Quarantäne gestellten platziert wird, finden Sie unter [Compute-Resilienz virtueller Computer in Windows Server2016](http://blogs.msdn.com/b/clustering/archive/2015/06/03/10619308.aspx).  

**Speicher-Resilienz** In Windows Server 2016, virtuelle Maschinen sind stabiler, bei vorübergehenden Speicher. Die verbesserte VM-Resilienz kann Mandanten virtuelle Maschine Sitzungsstatus im Fall einer Unterbrechung der Speicher erhalten. Dies erfolgt durch intelligente und schnelle virtuelle Maschine als Reaktion auf Speicherprobleme-Infrastruktur.  

Wenn eine virtuelle Maschine trennt zugrunde liegenden Speicher, es angehalten und wartet darauf, dass Speicher wiederherstellen. Angehaltener, behält der virtuellen Maschine Kontext der Anwendungen, die Sie ausgeführt werden. Wenn für den Speicher des virtuellen Computers-Verbindung wiederhergestellt wird, wird der virtuelle Computer auf den ausgeführten Zustand zurückgegeben. Daher wird dem mandantencomputer Sitzungszustand auf Wiederherstellungspunkte beibehalten.  

In Windows Server2016 ist die Speicher Resilienz virtueller Computer kennen und für Gastcluster zu.  

## <a name="BKMK_Diagnostics"></a>Diagnose Verbesserungen bei der Failover-Clusterunterstützung  
Um Probleme mit Failoverclustern zu diagnostizieren, Windows Server2016 umfassen Folgendes:  

-   Mehrere Erweiterungen für Cluster Log-Dateien (z.B. Zeitzoneninformationen und DiagnosticVerbose-Protokoll), die macht ist einfacher, Failover Clustering Probleme zu beheben. Weitere Informationen finden Sie unter [Windows Server2016 Failover Cluster Troubleshooting Enhancements - Clusterprotokoll](http://blogs.msdn.com/b/clustering/archive/2015/05/15/10614930.aspx).  

-   Ein neues Geben Sie ein Abbild des **Active Speicherabbild**, die filtert die meisten Speicherseiten, die virtuellen Maschinen zugeordnet und macht daher die memory.dmp sehr viel kleiner und leichter zu speichern oder kopieren.  Weitere Informationen finden Sie unter [Windows Server2016 Failover Cluster Troubleshooting Enhancements Verbesserungen - aktiven Dump](http://blogs.msdn.com/b/clustering/archive/2015/05/18/10615526.aspx).  

## <a name="BKMK_SiteAware"></a>Standortabhängige Failovercluster  
Windows Server2016 enthält Site - aware Failoverclustern, die von Gruppenknoten in gestreckten Clustern, die basierend auf ihrer physischen Position (Standort) aktivieren. Cluster-Standortinformationen verbessert wesentliche Vorgänge während des clusterlebenszyklus wie das Failoververhalten, Platzierungsrichtlinien, Takt zwischen den Knoten und quorumverhalten. Weitere Informationen finden Sie unter [Site-aware Failover Clusters in Windows Server2016](http://blogs.msdn.com/b/clustering/archive/2015/08/19/10636304.aspx).  

## <a name="BKMK_multidomainclusters"></a>Arbeitsgruppen und Domänen-Clustern  
In Windows Server2012 R2 und früheren Versionen kann ein Cluster nur zwischen Memberknoten der gleichen Domäne erstellt werden.   Windows Server2016 beseitigt diese Hindernisse und führt die Möglichkeit zum Erstellen eines Failoverclusters ohne Active Directory-Abhängigkeiten. Sie können jetzt in den folgenden Konfigurationen Failovercluster erstellen:  

-   **Cluster mit nur einer Domäne.** Cluster mit allen Knoten der gleichen Domäne angehören.  

-   **Cluster mit mehreren Domänen.** Cluster mit Knoten, die verschiedenen Domänen angehören.  

-   **Arbeitsgruppe Cluster.** Cluster mit Knoten, die ein Mitgliedsserver ist / Arbeitsgruppe (keiner Domäne beigetreten).  

Weitere Informationen finden Sie unter [Arbeitsgruppen und Domänen-Cluster in Windows Server2016](http://blogs.msdn.com/b/clustering/archive/2015/08/17/10635825.aspx)  
## <a name="BKMK_VMLoadBalancing"></a>VM-Lastenausgleich  
Virtuelle Maschine Netzwerklastenausgleich ist ein neues Feature in der Failover-Clusterunterstützung, die der nahtlosen Lastenausgleich von virtuellen Maschinen über die Knoten in einem Cluster hinweg vereinfacht. Überbelegt Knoten werden basierend auf der virtuellen Maschine Arbeitsspeicher und CPU-Auslastung auf dem Knoten identifiziert. Virtuelle Maschinen werden dann verschoben (live migriert) aus einem überbelegten Knoten zu Knoten mit verfügbare Bandbreite (sofern zutreffend). Der Aggressivität für den Netzwerklastenausgleich kann optimiert werden, um eine optimale Leistung und -Auslastung zu gewährleisten.  Lastenausgleich ist in Windows Server2016 Technical Preview standardmäßig aktiviert. Lastenausgleich ist jedoch deaktiviert, wenn die dynamische Optimierung SCVMM aktiviert ist.  

## <a name="BKMK_VMStartOrder"></a>VM-Startreihenfolge  
VM-Startreihenfolge ist ein neues Feature in der Failover-Clusterunterstützung, in der Start Reihenfolge Orchestrierung für virtuelle Computer (und alle Gruppen) eingeführt, in einem Cluster. Virtuelle Maschinen können jetzt in Ebenen gruppiert werden, und starten Reihenfolge Abhängigkeiten zwischen verschiedenen erstellt werden können. Dadurch wird sichergestellt, dass die wichtigsten virtuellen Computer (z.B. Domänencontroller oder Dienstprogramm virtuelle Maschinen) erste gestartet werden. Virtuelle Computer werden nicht gestartet, bis die virtuellen Computer, die sie über eine Abhängigkeit auch gestartet werden.  

## <a name="BKMK_SMBMultiChannel"></a>Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke  
Failovercluster-Netzwerke sind nicht mehr auf eine einzelne NIC pro Subnetz beschränkt / Netzwerk. Klicken Sie mit vereinfachten SMB Multichannel- und Multi-NIC-Clusternetzwerke Netzwerkkonfiguration erfolgt automatisch, und jede Netzwerkkarte im Subnetz für den Cluster und die Arbeitslast Datenverkehr verwendet werden kann. Diese Verbesserung ermöglicht Kunden, um den Netzwerkdurchsatz für Hyper-V, SQL Server-Failoverclusterinstanz und anderen SMB-Arbeitslasten zu maximieren.  

Weitere Informationen finden Sie unter [vereinfachten SMB Multichannel- und Multi-NIC-Clusternetzwerke](smb-multichannel.md).

## <a name="see-also"></a>Siehe auch  
* [Speicher](../storage/storage.md)  
* [Neues im Speicher in Windows Server 2016](../storage/whats-new-in-storage.md)  
