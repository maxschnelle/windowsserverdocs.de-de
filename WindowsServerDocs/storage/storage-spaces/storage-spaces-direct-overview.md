---
title: Direkte Speicherplätze – Übersicht
ms.prod: windows-server
ms.author: cosdar
manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 06/26/2019
ms.assetid: 8bd0d09a-0421-40a4-b752-40ecb5350ffd
description: Eine Übersicht über direkte Speicherplätze, ein Feature von Windows Server, mit dem Sie Server mit internem Speicher in einer Software definierten Speicherlösung Clustern können.
ms.localizationpriority: medium
ms.openlocfilehash: d2568f068495ec56936c7f14bd286daf77b57bd4
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966502"
---
# <a name="storage-spaces-direct-overview"></a>Direkte Speicherplätze – Übersicht

>Gilt für: Windows Server 2019, Windows Server 2016

„Direkte Speicherplätze“ verwendet branchenübliche Server mit lokal angeschlossenen Laufwerken, um hoch verfügbare, hoch skalierbare softwaredefinierte Speicher zu einem Bruchteil der Kosten von herkömmlichen SAN- oder NAS-Arrays zu erstellen. Die konvergierte oder hyperkonvergierte Architektur vereinfacht die Beschaffung und Bereitstellung, während Features wie Caching, Speicherebenen und Lösch Programmierung zusammen mit den neuesten Hardware Innovationen wie RDMA-Netzwerk-und nvme-Laufwerke eine nicht über rivalisierte Effizienz und Leistung bieten.

Direkte Speicherplätze ist in den Builds Windows Server 2019 Datacenter, Windows Server 2016 Datacenter und [Windows Server Insider Preview](https://insider.windows.com/for-business-getting-started-server/)enthalten.

Informationen zu anderen Anwendungen von Speicherplätzen, wie freigegebene SAS-Cluster und eigenständige Server, finden Sie unter [Übersicht über Speicherplätze](overview.md). Informationen zur Verwendung von Speicherplätzen auf einem Windows 10-PC finden Sie unter [Speicherplätze in Windows 10](https://support.microsoft.com/help/12438/windows-10-storage-spaces).

|       |       |
|   -   |   -   |
| **Grundlegende Informationen**<br><ul><li>Übersicht (Sie sind hier)</li><li>[Grundlegendes zum Cache](understand-the-cache.md)</li><li>[Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md)<li>[Aspekte symmetrischer Laufwerke](drive-symmetry-considerations.md)</li><li>[Grundlagen und Überwachung der Neusynchronisierung des Speichers](understand-storage-resync.md)</li><li>[Grundlegendes zum Cluster- und Poolquorum](understand-quorum.md)</li><li>[Clustergruppen](cluster-sets.md)</li> | **Planen**<br><ul><li>[Hardwareanforderungen](storage-spaces-direct-hardware-requirements.md)</li><li>[Verwenden direkter Speicherplätze mit dem CSV-In-Memory-Lesecache](csv-cache.md)</li><li>[Auswählen von Laufwerken](choosing-drives.md)</li><li>[Planen von Volumes](plan-volumes.md)</li><li>[Verwendung von Gast-VM-Clustern](storage-spaces-direct-in-vm.md)</li><li>[Notfallwiederherstellung](storage-spaces-direct-disaster-recovery.md)</li> |
| **Bereitstellen**<br><ul><li>[Bereitstellen von direkten Speicherplätzen](deploy-storage-spaces-direct.md)</li><li>[Erstellen von Volumes](create-volumes.md)</li><li>[Geschachtelte Resilienz](nested-resiliency.md)</li><li>[Konfigurieren des Quorums](../../failover-clustering/manage-cluster-quorum.md)</li><li>[Upgrade eines „Direkte Speicherplätze“-Clusters auf Windows Server 2019](upgrade-storage-spaces-direct-to-windows-server-2019.md)</li><li>[Grundlagen und Bereitstellung des persistenten Speichers](deploy-pmem.md)</li> | **Verwalten**<br><ul><li>[Verwalten mit Windows Admin Center](../../manage/windows-admin-center/use/manage-hyper-converged.md)</li><li>[Hinzufügen von Servern oder Laufwerken](add-nodes.md)</li><li>[Offlineschalten eines „Direkte Speicherplätze“-Servers zu Wartungszwecken](maintain-servers.md)</li><li>[Entfernen von Servern in „Direkte Speicherplätze“](remove-servers.md)</li><li>[Erweitern von Volumes](resize-volumes.md)</li><li>[Löschen von Volumes](delete-volumes.md)</li><li>[Aktualisieren der Laufwerkfirmware](../update-firmware.md)</li><li>[Leistungsverlauf](performance-history.md)</li><li>[Einschränken der Zuweisung von Volumes](delimit-volume-allocation.md)</li><li>[Verwenden von Azure Monitor in einem hyperkonvergierten Cluster](configure-azure-monitor.md)</li> |
| **Problembehandlung**<br><ul><li>[Problembehandlungsszenarien](troubleshooting-storage-spaces.md)</li><li>[Beheben von Integritäts-und Betriebszuständen](storage-spaces-states.md)</li><li>[Sammeln von Diagnosedaten mit direkte Speicherplätze](data-collection.md)</li><li>[Integritätsverwaltung für Speicherklassenspeicher](Storage-class-memory-health.md)</li> | **Aktuelle Blogbeiträge**<br><ul><li>[13,7 Millionen IOPS with direkte Speicherplätze: der neue Branchendaten Satz für die hyperkonvergierte Infrastruktur](https://techcommunity.microsoft.com/t5/storage-at-microsoft/the-new-hci-industry-record-13-7-million-iops-with-windows/ba-p/428314)</li><li>[Hyperkonvergierte Infrastruktur in Windows Server 2019: Die Countdownzeit wird jetzt gestartet!](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)</li><li>[Fünf große Ankündigungen von Windows Server Summit](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)</li><li>[10.000 direkte Speicherplätze Cluster und Zählung...](https://techcommunity.microsoft.com/t5/storage-at-microsoft/storage-spaces-direct-10-000-clusters-and-counting/ba-p/428185)</li> |

## <a name="videos"></a>Videos

**Übersicht über Quick Videos (5 Minuten)**

> [!Video https://www.youtube-nocookie.com/embed/raeUiNtMk0E]

**Direkte Speicherplätze bei der Microsoft Ignite 2018 (1 Stunde)**

> [!Video https://www.youtube-nocookie.com/embed/5kaUiW3qo30]

**Direkte Speicherplätze bei der Microsoft Ignite 2017 (1 Stunde)**

> [!Video https://www.youtube-nocookie.com/embed/YDr2sqNB-3c]

**Start Ereignis bei Microsoft Ignite 2016 (1 Stunde)**

> [!Video https://www.youtube-nocookie.com/embed/LK2ViRGbWs]

## <a name="key-benefits"></a>Hauptvorteile

|       |       |
|   -   |   -   |
| ![Einfachheit](media/storage-spaces-direct-in-windows-server-2016/simplicity-icon.png)   | **Theit.** Wechseln Sie in weniger als 15 Minuten von branchenüblichen Servern unter Windows Server 2016 zu Ihrem ersten „Direkte Speicherplätze“-Cluster. Für System Center-Benutzer erfolgt die Bereitstellung über ein einziges Kontrollkästchen.       |
| ![Nicht über rivalisierte Leistung](media/storage-spaces-direct-in-windows-server-2016/performance-icon.png)   | **Unübertroffene Leistung.** Ganz gleich, ob All-Flash- oder Hybridspeicher, mit „Direkte Speicherplätze“ erreichen Sie mühelos über [150.000 gemischte zufällige 4K-Random-IOPS (E/A-Vorgänge pro Sekunde) pro Server](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) mit konsistenter, geringer Latenz dank der in den Hypervisor eingebetteten Architektur, dem integrierten Lese-/Schreibcache und der Unterstützung für innovative, direkt auf dem PCIe-Bus montierte NVMe-Laufwerke.      |
| ![Fehlertoleranz](media/storage-spaces-direct-in-windows-server-2016/fault-tolerance-icon.png)   | **Fehlertoleranz.** Integrierte Resilienz verarbeitet Laufwerk-, Server- oder Komponentenausfälle bei fortlaufender Verfügbarkeit. Größere Bereitstellungen können auch für [Gehäuse- und Rack-Fehlertoleranz](../../failover-clustering/fault-domains.md) konfiguriert werden. Bei Ausfall von Hardware brauchen Sie diese nur auszutauschen. Die Software setzt sich selbst und ohne komplizierte Verwaltungsschritte wieder instand.       |
| ![Ressourceneffizienz](media/storage-spaces-direct-in-windows-server-2016/efficiency-icon.png)   | **Ressourceneffizienz.** Die Löschung von Lösch Vorgängen bietet eine bis zu 2,4-fache höhere Speichereffizienz mit einzigartigen Innovationen wie z. b. lokalen Erstellungs Codes und Refs-echt Zeitebenen, um diese Vorteile auf Festplattenlaufwerke und gemischte heiße/kalte Workloads auszuweiten       |
| ![Verwaltbarkeit](media/storage-spaces-direct-in-windows-server-2016/manageability-icon.png)   | **Verwaltbarkeit**: Verwenden Sie [Storage QoS-Steuerelemente](../storage-qos/storage-qos-overview.md), um zu gewährleisten, dass übermäßig ausgelastete VMs die Mindest- und Höchstgrenzen für IOPS pro-VM nicht unter- bzw. überschreiten. Der [Integritätsdienst](../../failover-clustering/health-service-overview.md) bietet fortlaufende integrierte Überwachung und Warnung, und neue APIs erleichtern das Sammeln umfassender, clusterweiter Leistungs- und Kapazitätsmetriken.      |
| ![Skalierbarkeit](media/storage-spaces-direct-in-windows-server-2016/scalability-icon.png)   | **Skalierbarkeit**. Gehen Sie bis zu 16 Server und mehr als 400 Laufwerke, um bis zu 1 Peer-(1.000 Terabytes) Speicher pro Cluster zu erhalten. Zum horizontalen Skalieren fügen Sie einfach Laufwerke oder weitere Server hinzu. „Direkte Speicherplätze“ integriert und nutzt neue Laufwerke automatisch. Speichereffizienz und Leistung lassen sich berechenbar in großem Maßstab verbessern.       |

## <a name="deployment-options"></a>Bereitstellungsoptionen

„Direkte Speicherplätze“ wurde für zwei unterschiedliche Bereitstellungsoptionen entworfen:

### <a name="converged"></a>Konvergente Bereitstellung

**Speicher und Compute in separaten Clustern.** Die Option der konvergenten Bereitstellung ordnet einen Dateiserver mit horizontaler Skalierung (Scale-out File Server, SoFS) in Ebenen über „Direkte Speicherplätze“ an, um NAS über SMB3-Dateifreigaben bereitzustellen. Dies ermöglicht die Skalierung von Compute/Workload unabhängig vom Speichercluster, was für größere Bereitstellungen, z. B. Hyper-V-IaaS (Infrastruktur als Dienst) für Dienstanbieter und Unternehmen unerlässlich ist.

![Direkte Speicherplätze bietet Speicher mithilfe des Dateiserver mit horizontaler Skalierung Features für Hyper-V-VMS auf einem anderen Server oder Cluster.](media/storage-spaces-direct-in-windows-server-2016/converged-minimal.png)

### <a name="hyper-converged"></a>Hyperkonvergente Bereitstellung

**Ein einzelner Cluster für Compute und Speicher.** Die Option der hyperkonvergenten Bereitstellung führt virtuelle Hyper-V-Computer oder SQL Server-Datenbanken direkt auf den Servern aus, stellt den Speicher bereit und speichert die Dateien der VMs auf den lokalen Volumes. Dadurch entfällt die Notwendigkeit, den Zugriff auf Dateiserver und die entsprechenden Berechtigungen zu konfigurieren, und die Hardwarekosten für kleine und mittelständische Unternehmen oder Installationen in Remotebüros/Filialen werden gesenkt. Siehe Bereitstellen von [direkte Speicherplätze](deploy-storage-spaces-direct.md).

![Direkte Speicherplätze bietet Speicher für Hyper-V-VMS im gleichen Cluster.](media/storage-spaces-direct-in-windows-server-2016/hyper-converged-minimal.png)

## <a name="how-it-works"></a>Funktionsweise

„Direkte Speicherplätze“ ist die Weiterentwicklung von „Speicherplätze“, das mit Windows Server 2012 eingeführt wurde. „Direkte Speicherplätze“ nutzt viele Features von Windows Server, die Sie bereits kennen, z. B. Failoverclustering, das CSV-Dateisystem (Cluster Shared Volume, freigegebenes Clustervolume), SMB3 (Server Message Block) und natürlich „Speicherplätze“. Außerdem werden neuen Technologie eingeführt, insbesondere der Softwarespeicherbus.

Hier finden Sie eine Übersicht über den „Direkte Speicherplätze“-Stapel:

![Stapel bei Verwendung von „Direkte Speicherplätze“](media/storage-spaces-direct-in-windows-server-2016/converged-full-stack.png)

**Netzwerkhardware.** „Direkte Speicherplätze“ verwendet für die Kommunikation zwischen Servern SMB3, einschließlich SMB Direct und SMB Multichannel über Ethernet. Es wird dringend empfohlen, mehr als 10 GbE mit RDMA (Remote Direct Memory Access, Remotezugriff auf den direkten Speicher) zu verwenden, entweder iWARP oder RoCE.

**Speicherhardware.** Zwischen 2 und 16 Server mit lokal angeschlossenen SATA- SAS-, oder NVMe-Laufwerken. Jeder Server muss über mindestens 2 SSDs und mindestens 4 zusätzliche Laufwerke verfügen. Die SATA- und SAS-Geräte sollten sich hinter einem Hostbusadapter (HBA) und einer SAS-Erweiterung befinden. Wir empfehlen dringend die sorgfältig entwickelten und umfassend geprüften Plattformen unserer Partner (demnächst verfügbar).

**Failoverclustering.** Das integrierte Clusteringfeature von Windows Server wird verwendet, um den Server zu verbinden.

**Softwarespeicherbus.** Der Softwarespeicherbus ist neu in „Direkte Speicherplätze“. Er umfasst den Cluster und stellt ein softwaredefiniertes speicherfabric her, in dem alle Server alle lokalen Laufwerke sehen können. Sie können es sich als Ersatz für die kostspielige und eingeschränkte Fibre Channel- oder Shared SAS-Verkabelung vorstellen.

**Cache der Speicherbusebene.** Der Softwarespeicherbus bindet dynamisch die schnellsten vorhandenen Laufwerke (z. B. SSD) mit langsameren Laufwerken (z. B. HDDs), um das Zwischenspeichern von serverseitigen Lese-/Schreibzugriff zum Beschleunigen von E/A-Vorgängen und zum Steigern des Durchsatzes zu ermöglichen.

**Speicher Pool.** Die Sammlung der Laufwerke, die die Grundlage für „Speicherplätze“ darstellt, wird als Speicherpool bezeichnet. Der Speicherpool wird automatisch erstellt, und alle geeigneten Laufwerke werden automatisch ermittelt und hinzugefügt. Es wird dringend empfohlen, einen Pool pro Cluster mit den Standardeinstellungen zu verwenden. Weitere Informationen finden Sie in unserem [Deep Dive-Artikel für den Speicherpool](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deep-dive-the-storage-pool-in-storage-spaces-direct/ba-p/425959).

**Speicherplätze.** Speicherplätze bieten Fehlertoleranz für virtuelle "Datenträger" mithilfe von [Spiegelung, Löschung Coding oder beides](storage-spaces-fault-tolerance.md). Stellen Sie sich „Speicherplätze“ als verteiltes, softwaredefiniertes RAID vor, das die Laufwerken im Pool verwendet. In „Direkte Speicherplätze“ verfügen diese virtuellen Laufwerke in der Regel über Resilienz für zwei gleichzeitige Laufwerk- oder Serverausfälle (z. B. Drei-Wege-Spiegelung, wobei jede Datenkopie auf einem anderen Server gespeichert ist). Zusätzlich ist Gehäuse- und Rack-Fehlertoleranz verfügbar.

**Robustes Datei System (Refs).** ReFS ist das wichtigste, speziell für die Virtualisierung entwickelte Dateisystem. Es bietet erhebliche Beschleunigungen für VHDX-Dateivorgänge, wie Erstellung, Erweiterung und Prüfpunkt-Zusammenführung, sowie integrierte Prüfsummen zum Erkennen und Beheben von Bitfehlern. Außerdem werden echt Zeitebenen eingeführt, die Daten basierend auf der Nutzung zwischen so genannten "heißen" und "kalten" Speicherebenen in Echtzeit drehen.

**Freigegebene Clustervolumes.** Das CSV-Dateisystem vereinigt alle Refs-Volumes in einem einzelnen Namespace, auf den über einen beliebigen Server zugegriffen werden kann, sodass jedes Volume auf jedem Server so aussieht, als ob es lokal bereitgestellt wird.

**Dateiserver mit horizontaler Skalierung.** Diese letzte Ebene ist nur für konvergente Bereitstellungen erforderlich. Der Dateiserver mit horizontaler Skalierung bietet Clients, z. B. einem anderen Cluster mit Hyper-V, mithilfe des SMB3-Zugriffsprotokolls Remotezugriff auf Dateien über das Netzwerk, und wandelt „Direkte Speicherplätze“ dadurch effizient in NAS (Network Attached Storage) um.

## <a name="customer-stories"></a>Kundenstimmen

Es gibt weltweit [mehr als 10.000 Cluster, auf](https://techcommunity.microsoft.com/t5/storage-at-microsoft/storage-spaces-direct-10-000-clusters-and-counting/ba-p/428185) denen direkte Speicherplätze ausgeführt wird. Organisationen aller Größen, von kleinen Unternehmen, die nur zwei Knoten bereitstellen, für große Unternehmen und Regierungsbehörden, die Hunderte von Knoten bereitstellen, hängen von direkte Speicherplätze für Ihre kritischen Anwendungen und Infrastrukturen ab.

Besuchen Sie [Microsoft.com/HCI](https://www.microsoft.com/hci) , um Ihre Geschichten zu lesen:

[![Raster von Kundenlogos](media/storage-spaces-direct-in-windows-server-2016/customer-stories.png)](https://www.microsoft.com/hci)

## <a name="management-tools"></a>Verwaltungstools

Die folgenden Tools können zum Verwalten und/oder Überwachen von direkte Speicherplätze verwendet werden:

| Name | Grafisch oder Befehlszeile? | Kostenpflichtig oder inbegriffen? |
|-----------------|----------------------------|-------------------|
| [Windows Admin Center](../../manage/windows-admin-center/overview.md)     | Grafisch    | Enthalten |
| Server-Manager & Failovercluster-Manager                                 | Grafisch    | Enthalten |
| Windows PowerShell                                                        | Befehlszeile | Enthalten |
| [System Center Virtual Machine Manager (SCVMM)](/system-center/vmm/s2d?view=sc-vmm-2019) <br>& [Operations Manager (SCOM)](https://www.microsoft.com/download/details.aspx?id=54700) | Grafisch    | Bezahlt     |

## <a name="get-started"></a>Erste Schritte

Probieren Sie direkte Speicherplätze [in Microsoft Azure](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)aus, oder laden Sie eine 180-tägige Evaluierungsversion von Windows Server aus den [Windows Server-Auswertungen](https://go.microsoft.com/fwlink/?linkid=842602)herunter.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md)
- [Speicherreplikat](../storage-replica/storage-replica-overview.md)
- [Storage im Microsoft-Blog](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)
- [Direkte Speicherplätze Durchsatz mit IWarp](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) (TechNet-Blog)
- [Neues beim Failoverclustering unter Windows Server](../../failover-clustering/whats-new-in-failover-clustering.md)
- [Quality of Service für Speicher](../storage-qos/storage-qos-overview.md)
- [Windows IT Pro-Support](https://www.microsoft.com/itpro/windows/support)
