---
ms.assetid: 350aa5a3-5938-4921-93dc-289660f26bad
title: Neues beim Failoverclustering unter Windows Server
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: get-started-article
manager: dongill
author: JasonGerend
ms.author: jgerend
ms.date: 10/18/2018
ms.openlocfilehash: 330f65721fca1908ac54ddfd194f96ffe540f1b5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442361"
---
# <a name="whats-new-in-failover-clustering"></a>What's new in Failover Clustering (Neues beim Failoverclustering)

> Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema wird erläutert, die neue und geänderte Funktionen im Failover-Clusterunterstützung für Windows Server 2019 und Windows Server 2016.

## <a name="whats-new-in-windows-server-2019"></a>Neuigkeiten in Windows Server 2019

- **Clustergruppen**

    Cluster-Sätze können Sie die Anzahl von Servern in einer einzelnen softwaredefinierten Rechenzentrums (SDDC)-Lösung über die aktuellen Grenzwerte eines Clusters hinaus erhöhen. Dies erfolgt durch die Gruppierung mehrerer Cluster in einem Clustersatz – eine lose verbundene Gruppierung mehrere Failovercluster: compute, Speicher, und hyper-konvergiert.
    Mit Cluster, können Sie online virtuellen Computer verschieben (Livemigration) zwischen Clustern innerhalb des Clusters festgelegt.

    Weitere Informationen finden Sie unter [Clustersätze](../storage/storage-spaces/cluster-sets.md).

- **Azure-fähigen Clustern**

    Failovercluster erkennen jetzt automatisch, wenn sie in Azure IaaS-Computer ausführen und optimieren die Konfiguration, um proaktives Failover und die Protokollierung von Ereignissen, die ein Höchstmaß an Verfügbarkeit zu erreichen, geplanten Wartung in Azure bereitstellen. Die Bereitstellung ist auch die Notwendigkeit zum Konfigurieren des Lastenausgleichs mit dynamischen Netzwerknamen für den Clusternamen vereinfacht.

- **Domänenübergreifende-clustermigration**

    Failovercluster können nun dynamisch Verschieben von einer Active Directory-Domäne in eine andere domänenkonsolidierung vereinfachen, und die Cluster von Hardwarepartnern erstellt wurden und die Domäne des Kunden wird später hinzugefügt werden können.
- **USB-Zeugen**

    Sie können nun ein einfaches USB-Laufwerk mit einem Netzwerkswitch verbunden sind, als Zeuge beim Bestimmen des Quorums für einen Cluster verwenden. Dies erweitert den Dateifreigabezeugen an, um alle SMB2-konformes Gerät zu unterstützen.

- **Verbesserungen der Cluster-Infrastruktur**

    Der CSV-Cache ist jetzt standardmäßig aktiviert, zur Verbesserung der Leistung des virtuellen Computers. MSDTC unterstützt nun Cluster Shared Volumes, um die Bereitstellung von MSDTC-Workloads auf Storage Spaces Direct, z. B. mit SQL Server, zu ermöglichen. Verbesserte Logik zum Erkennen von partitionierten Knoten mit Selbstkorrektur, um Knoten zur Clustermitgliedschaft zurückzugeben. Verbesserte Erkennung von Clusternetzwerkrouten und Selbstkorrektur.

- **Clusterfähiges aktualisieren unterstützt "direkte Speicherplätze".**

    Cluster Aware Updating (CAU) ist nun integriert und berücksichtigt Storage Spaces Direct, wodurch die Datensynchronisierung auf jedem Knoten überprüft und sichergestellt wird. Clusterfähiges aktualisieren untersucht Updates nur bei Bedarf auf intelligente Weise neu starten. Dies ermöglicht die Orchestrierung Neustarts für alle Server im Cluster für eine geplante Wartung.

- **File Share Witness Verbesserungen** wir aktiviert die Verwendung von File Share Witness in den folgenden Szenarien: 
  - Fehlt oder ist sehr schlechte Zugriff auf das Internet aufgrund von einem Remotestandort befindet, verhindert, dass einen cloudzeugen. 
  - Fehlende der freigegebenen Laufwerke für einen datenträgerzeugen. Dies ist möglicherweise ein "direkte Speicherplätze" hyperkonvergenten Konfiguration einer SQL Server Always On Availability Gruppen (-Verfügbarkeitsgruppen), oder * Exchange Database Availability Group (DAG), verwenden Sie keines der freigegebene Datenträger. 
  - Mangel an einer domänencontrollerverbindung aufgrund der Cluster wird hinter einer DMZ. 
  - Ein Arbeitsgruppe oder Cross-Domain-Cluster für die es ist keine Active Directory-Clusternamenobjekt (CNO). Erfahren Sie mehr über diese Erweiterungen in den folgenden Beitrag im Server und Management-Blogs: Failover-Cluster-Dateifreigabenzeugen und DFS.
    
    Wir jetzt auch explizit blockiert die Verwendung einer DFS-Namespaces-Dateifreigabe als Speicherort. Hinzufügen ein dateifreigabezeugen Freigabe kann eine DFS-Verknüpfung Stabilitätsprobleme für Ihren Cluster, und diese Konfiguration nicht unterstützt. Wir haben die Logik zum erkennen, wenn eine Freigabe verwendet die DFS-Namespaces und DFS-Namespaces erkannt wird, Failovercluster-Manager blockiert die Erstellung des Zeugen, und zeigt eine Fehlermeldung zur fehlenden Unterstützung hinzugefügt.
- **Cluster-Härtung**

    Die Intra-Cluster-Kommunikation über SMB (Server Message Block) für freigegebene Clustervolumes und Storage Spaces Direct nutzt jetzt Zertifikate, um die sicherste Plattform bereitzustellen. Dadurch können Failovercluster ohne Abhängigkeiten von NTLM arbeiten und Sicherheitsbasislinien aktivieren.
- **Failovercluster verwendet nicht mehr die NTLM-Authentifizierung.**

    Failovercluster werden nicht mehr NTLM-Authentifizierung verwenden. Stattdessen wird Kerberos und zertifikatbasierte Authentifizierung ausschließlich verwendet. Es gibt keine Änderungen durch den Benutzer oder die Bereitstellungstools, nutzen diese Verbesserung der Sicherheit erforderlich. Darüber hinaus können Failovercluster in Umgebungen bereitgestellt werden, in denen NTLM deaktiviert wurde. 


## <a name="whats-new-in-windows-server-2016"></a>Was ist neu in Windows Server 2016

### <a name="BKMK_RollingUpgrade"></a>Operating System Rolling Upgrade von Clustern

Cluster Operating System Rolling Upgrade kann ein Administrator des Betriebssystems des Clusterknotens von Windows Server 2012 R2 auf eine neuere Version zu aktualisieren, ohne Unterbrechung von Hyper-V oder Workloads des Dateiservers für horizontales Skalieren. Mit diesem Feature können die Downtimesanktionen laut Vereinbarungen zum Servicelevel (Service Level Agreements, SLA) vermieden werden. 

**Welchen Nutzen bietet diese Änderung?**  

Aktualisieren eines Hyper-V oder Scale-Out File Server Clusters von Windows Server 2012 R2 auf Windows Server 2016 nicht mehr eine Unterbrechung erforderlich ist. Der Cluster funktionieren weiterhin auf einem Windows Server 2012 R2-Ebene, bis alle Knoten im Cluster Windows Server 2016 ausgeführt werden. Funktionsebene des Clusters wird ein Upgrade auf Windows Server 2016 mithilfe der Windows PowerShell-Cmdlet `Update-ClusterFunctionalLevel`. 

> [!WARNING]  
> -   Nach der Aktualisierung der Funktionsebene des Clusters können Sie nicht zurück auf einer Funktionsebene der Windows Server 2012 R2-Cluster wechseln. 
> -   Bis die `Update-ClusterFunctionalLevel` Cmdlet ausgeführt wird, der Prozess kann rückgängig gemacht werden, und können Windows Server 2012 R2-Knoten hinzugefügt werden und Windows Server 2016-Knoten entfernt werden können. 

**Worin bestehen die Unterschiede?**  

Ein Hyper-V oder Scale-Out File Server-Failovercluster kann jetzt problemlos ohne Ausfallzeiten aktualisiert werden oder benötigen, um einen neuen Cluster mit Knoten erstellen, die das Betriebssystem Windows Server 2016 ausgeführt werden. Migrieren von Clustern auf Windows Server 2012 R2 verwendet den vorhandenen Cluster offline geschaltet und Neuinstallation des neuen Betriebssystems für jeden Knoten den Cluster wieder online schalten. Der alte Prozess war mühsam und erforderliche Ausfallzeit. Allerdings in Windows Server 2016 muss der Cluster nicht zu einem beliebigen Zeitpunkt offline geschaltet. 

Die Cluster-Betriebssysteme für das Upgrade in Phasen lauten wie folgt für jeden Knoten in einem Cluster:  
-   Der Knoten angehalten und ausgeglichen, die von allen virtuellen Computern, die darauf ausgeführt werden. 
-   Die virtuellen Computer (oder andere clusterarbeitsauslastung) werden auf einen anderen Knoten im Cluster migriert werden. 
-   Das vorhandene Betriebssystem entfernt, und eine Neuinstallation des Betriebssystems Windows Server 2016 auf dem Knoten ausgeführt wird. 
-   Der Knoten, auf denen das Betriebssystem Windows Server 2016 wird erneut zum Cluster hinzugefügt. 
-   An diesem Punkt wird der Cluster als im gemischten Modus ausgeführt werden, da die Knoten des Clusters entweder Windows Server 2012 R2 oder Windows Server 2016 ausgeführt werden. 
-   Funktionsebene des Clusters bleibt bei Windows Server 2012 R2. Auf dieser Funktionsebene werden neue Features in Windows Server 2016, die Kompatibilität mit früheren Versionen des Betriebssystems betreffen nicht verfügbar. 
-   Schließlich werden alle Knoten auf Windows Server 2016 aktualisiert. 
-   Clusterfunktionsebene wird dann in Windows Server 2016 mithilfe des Windows PowerShell-Cmdlets geändert `Update-ClusterFunctionalLevel`. An diesem Punkt können Sie die Windows Server 2016-Funktionen nutzen. 

Weitere Informationen finden Sie unter [Cluster Operating System Rolling Upgrade](cluster-operating-system-rolling-upgrade.md). 

### <a name="BKMK_SR"></a>Funktion "Speicherreplikat"  
Funktion "Speicherreplikat" ist eine neue Funktion, die es eine speicheragnostische ermöglicht auf Blockebene, synchrone Replikation zwischen Servern oder Clustern für die notfallwiederherstellung sowie Strecken eines Failoverclusters zwischen Standorten. Die synchrone Replikation ermöglicht die Spiegelung von Daten an physischen Standorten mit ausfallsicheren Volumes, um auf Dateisystemebene sicherzustellen, dass kein Datenverlust auftritt. Die asynchrone Replikation ermöglicht die Standorterweiterung über regionale Bereiche hinaus mit der Möglichkeit von Datenverlusten. 

**Welchen Nutzen bietet diese Änderung?**  

Funktion "Speicherreplikat" können Sie die folgenden Schritte ausführen:  

-   Bereitstellen einer Notfallwiederherstellungslösung von einem einzigen Anbieter für geplante und ungeplante Ausfälle unternehmenskritischer Workloads. 

-   Verwenden des SMB3-Transportprotokolls mit bewährter Zuverlässigkeit, Skalierbarkeit und Leistung. 

-   Strecken von Windows-Failoverclustern über regionale Bereiche hinweg. 

-   Verwenden Sie Microsoft-Software-End-to-End für die Speicherung und clustering, z. B. Hyper-V-Funktion "Speicherreplikat", Speicherplätze, Cluster, Scale-Out File Server, SMB3, die Datendeduplizierung und ReFS/NTFS. 

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

Mithilfe von Cloudzeugen als Failovercluster-quorumzeugen bietet die folgenden Vorteile:  

-   Nutzt die Microsoft Azure ein, und beseitigt die Notwendigkeit von einem dritten separaten Datencenter. 

-   Verwendet den standard öffentlich verfügbaren Microsoft Azure Blob Storage, den zusätzlichen Wartungsaufwand für in einer öffentlichen Cloud gehostete virtuelle Computer mehr herstellen müssen. 

-   Dieselbe Microsoft Azure Storage-Konto kann für mehrere Cluster (einen Blob-Datei pro Cluster, Cluster eindeutige Id als Blob-Dateiname) verwendet werden. 

-   Stellt einen sehr geringen laufenden Kosten für das Storage-Konto (aus der sehr klein geschriebenen pro Blob-Datei, BLOB-Datei aktualisiert wird, nur einmal bei Clusterknoten Zustandsänderungen Daten) bereit. 

Weitere Informationen finden Sie unter [einen Cloud Zeugen für ein Failovercluster bereitstellen](deploy-cloud-witness.md). 

**Worin bestehen die Unterschiede?**  

Dies ist eine neue Funktion in Windows Server 2016. 

### <a name="BKMK_VMs"></a>VM-Resilienz  
**Berechnen der Resilienz** Windows Server 2016 enthält mehr virtuellen Computern Compute resilienz um clusterinternen Kommunikationsprobleme in Ihrem Computecluster wie folgt zu verringern: 

-   **Resilienzoptionen für virtuelle Computer verfügbar:**  Sie können jetzt die resilienz virtueller Computer – Optionen konfigurieren, die Verhalten der virtuellen Computer während des vorübergehenden Fehlern zu definieren:  

    -   **Resilienzgrad:** Sie definieren, wie die vorübergehende Fehler behandelt werden können. 

    -   **Resilienz Zeitraum:**  Können Sie definieren, wie lange von allen virtuellen Computern isoliert ausgeführt werden dürfen. 

-   **Isolieren fehlerhafter Knoten:** Fehlerhafter Knoten sind isoliert und dürfen nicht mehr auf dem Cluster beitreten. Dadurch wird verhindert, dass Flügelschlagen Knoten negativ beeinflusst werden, andere Knoten und den gesamten Cluster. 

Weitere Informationen VM Compute Workflow und Knoten Quarantäne resilienzeinstellungen, die steuern, wie Ihre Knoten in Isolation oder in Quarantäne befindet, finden Sie unter [Compute-Resilienz virtueller Computer in Windows Server 2016](http://blogs.msdn.com/b/clustering/archive/2015/06/03/10619308.aspx). 

**Storage Resilienz** In WindowsServer 2016, virtuelle Computer sind stabiler, vorübergehende Fehler. Die verbesserte VM-resilienz hilft dabei, Mandanten-VM-Sitzungsstatus im Fall einer Unterbrechung Speicher beizubehalten. Dies erfolgt durch intelligente und schnelle VM-Antwort an Problemen mit Storage-Infrastruktur. 

Wenn des zugrunde liegenden Speichers ein virtuellen Computers trennt, angehalten und wartet darauf, dass Speicher wiederherstellen. Bei angehaltener behält der virtuelle Computer im Rahmen der darin ausgeführten Anwendungen. Wenn die Verbindung des virtuellen Computers, für den Speicher wiederhergestellt wird, gibt den virtuellen Computer in den ausgeführten Zustand zurück. Daher wird der Mandanten-VM-Sitzungsstatus zur Wiederherstellung beibehalten. 

In Windows Server 2016 ist die Storage resilienz virtueller Computer aktiviert, und optimiert für gastcluster zu. 

### <a name="BKMK_Diagnostics"></a>Verbesserungen bei der Diagnose im Rahmen des Failoverclustering  
Zum Diagnostizieren von Problemen mit Failoverclustern, umfasst Windows Server 2016 Folgendes:  

-   Mehrere Erweiterungen für Cluster Log-Dateien (z. B. Informationen zur Zeitzone und DiagnosticVerbose-Protokoll), mit der, ist einfacher, die Failover-clustering-Probleme zu beheben. Weitere Informationen finden Sie unter [Server 2016 Failover Cluster Problembehandlung bei Erweiterungen für Windows - Clusterprotokoll](http://blogs.msdn.com/b/clustering/archive/2015/05/15/10614930.aspx). 

-   Ein neues Geben Sie ein Speicherabbild des **Active Speicherabbild**, die filtert die meisten Speicher – Seiten, die virtuellen Maschinen zugeordnet und macht daher die memory.dmp viel kleiner und leichter zu speichern oder kopieren. Weitere Informationen finden Sie unter [Server 2016 Failover Cluster Problembehandlung bei Erweiterungen für Windows - Active Dump](http://blogs.msdn.com/b/clustering/archive/2015/05/18/10615526.aspx). 

### <a name="BKMK_SiteAware"></a>Standortabhängige Failovercluster  
Windows Server 2016 enthält Website - bewusst Failoverclustern, die von Gruppenknoten in gestreckten Clustern, die basierend auf ihrem physischen Standort (Standort) zu aktivieren. Cluster-Standortinformationen, verbessert wesentliche Vorgänge während des clusterlebenszyklus, z.B. Failoververhalten, Platzierungsrichtlinien, Takt zwischen den Knoten und quorumverhalten. Weitere Informationen finden Sie unter [standortabhängige Failovercluster in Windows Server 2016](http://blogs.msdn.com/b/clustering/archive/2015/08/19/10636304.aspx). 

### <a name="BKMK_multidomainclusters"></a>Clustern von Arbeitsgruppen und Domänen  
In Windows Server 2012 R2 und früheren Versionen kann ein Cluster nur zwischen Memberknoten Mitglied derselben Domäne erstellt werden. Windows Server 2016 beseitigt diese Hindernisse und führt die Möglichkeit zum Erstellen eines Failoverclusters ohne Active Directory-Abhängigkeiten ein. Sie können jetzt die Failovercluster in den folgenden Konfigurationen erstellen:  

-   **Cluster mit nur einer Domäne.** Cluster mit allen Knoten, die mit der gleichen Domäne verknüpft. 

-   **-Cluster mit mehreren Domänen.** Cluster mit Knoten, die verschiedenen Domänen angehören. 

-   **Arbeitsgruppe-Cluster.** Cluster mit Knoten, die ein Mitgliedsserver ist / Arbeitsgruppe (nicht der Domäne angehört). 

Weitere Informationen finden Sie unter [Arbeitsgruppen und Domänen-Cluster in Windows Server 2016](http://blogs.msdn.com/b/clustering/archive/2015/08/17/10635825.aspx)  
### <a name="BKMK_VMLoadBalancing"></a>VM-Lastenausgleich  
Lastenausgleich der VM ist ein neues Feature im Rahmen des Failoverclustering, die erleichtert den nahtlosen Lastenausgleich von virtuellen Computern auf die Knoten in einem Cluster. Überbelegt Knoten werden basierend auf dem virtuellen Computer, Arbeitsspeicher und CPU-Auslastung auf dem Knoten identifiziert. Virtuelle Computer verschoben werden (live migriert) aus einem überbelegten Knoten zu Knoten mit verfügbarer Bandbreite (falls zutreffend). Die Aggressivität der Lastenausgleich kann optimiert werden, um eine optimale Leistung und Auslastung zu gewährleisten. Lastenausgleich ist in Windows Server 2016 Technical Preview standardmäßig aktiviert. Lastenausgleich ist jedoch deaktiviert, wenn SCVMM dynamische Optimierung aktiviert ist. 

### <a name="BKMK_VMStartOrder"></a>VM-Startreihenfolge  
VM starten-Reihenfolge ist ein neues Feature in der Failover-Clusterunterstützung, die Reihenfolge der startorchestrierung für virtuelle Computer (und alle Gruppen) eingeführt werden, in einem Cluster. Virtuelle Computer können jetzt in Ebenen gruppiert werden, und starten Reihenfolge Abhängigkeiten zwischen unterschiedlichen Tarifen erstellt werden. Dadurch wird sichergestellt, dass die wichtigsten virtuellen Computer (z. B. virtuelle Computer sich Domänencontroller oder -Hilfsprogramm) zuerst gestartet werden. Virtuelle Computer werden nicht gestartet werden, bis die virtuellen Computer, die sie verfügen über eine Abhängigkeit für auch gestartet werden. 

### <a name="BKMK_SMBMultiChannel"></a> Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke  
Failover-Clusternetzwerke sind nicht mehr auf einer einzelnen NIC pro Subnetz beschränkt / Netzwerk. Vereinfachte SMB Multichannel und Multi-NIC-Clusternetzwerke Netzwerkkonfiguration erfolgt automatisch, und jede Netzwerkkarte das Subnetz für Cluster- und Workload-Datenverkehr verwendet werden kann. Dank dieser Erweiterung kann Kunden den Netzwerkdurchsatz für Hyper-V, SQL Server-Failoverclusterinstanz und andere SMB-Workloads zu maximieren. 

Weitere Informationen finden Sie unter [vereinfacht SMB Multichannel und Multi-NIC-Clusternetzwerke](smb-multichannel.md).

## <a name="see-also"></a>Siehe auch  
* [Speicher](../storage/storage.md)  
* [Neuerungen beim Speicher in WindowsServer 2016](../storage/whats-new-in-storage.md)  
