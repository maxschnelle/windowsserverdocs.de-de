---
ms.assetid: d11acbc2-40c6-4ab2-9514-2bc3ad81499a
title: Neuigkeiten bei der Datendeduplizierung
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: 4a69221548d9defff5a45413ccfe824f9788755a
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="whats-new-in-data-deduplication"></a>Neuigkeiten bei der Datendeduplizierung

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Die [Datendeduplizierung](overview.md) in Windows Server 2016 wurde optimiert und bietet nun auch für private Clouds eine hohe Leistung und Flexibilität sowie erstklassige Verwaltbarkeit. Weitere Informationen zum softwaredefinierten Speicherstapel in Windows Server 2016 finden Sie unter [Neuerungen beim Speicher in Windows Server2016](../whats-new-in-storage.md).

Die Datendeduplizierung wurde in Windows Server2016 wie folgt verbessert:

| Funktion | Neu oder aktualisiert | Beschreibung |
|---------------|----------------|-------------|
| [Unterstützung für große Volumes](whats-new.md#large-volume-support) | Aktualisiert | Vor Windows Server 2016 musste die Größe der Volumes speziell für die erwartete Änderung konfiguriert werden, wobei Volumes mit über 10TB keine geeigneten Kandidaten für die Deduplizierung waren. In Windows Server 2016 unterstützt die Datendeduplizierung Volumegrößen von bis zu 64TB. |
| [Unterstützung für große Dateien](whats-new.md#large-file-support) | Aktualisiert | Vor Windows Server2016 waren Dateien mit einer Größe von knapp 1TB keine geeigneten Kandidaten für die Deduplizierung. In Windows Server 2016 werden Dateien mit einer Größe von bis zu 1TB vollständig unterstützt. |
| [Unterstützung für Nano Server](whats-new.md#nano-server-support) | „Neu“, | Die Datendeduplizierung ist in der neuen Nano Server-Bereitstellungsoption für Windows Server2016 verfügbar und wird von dieser Option vollständig unterstützt. |
| [Vereinfachte Unterstützung von Sicherungen](whats-new.md#simple-backup-support) | „Neu“, | In Windows Server 2012 R2 mussten eine Reihe manueller Konfigurationsschritte ausgeführt werden, um virtualisierte Sicherungsanwendungen wie Microsoft [Data Protection Manager](https://technet.microsoft.com/library/hh758173.aspx) zu unterstützten. In Windows Server 2016 wurde ein neuer Standardverwendungstyp (Sicherung) hinzugefügt, um eine nahtlose Bereitstellung der Datendeduplizierung für virtualisierte Sicherungsanwendungen zu ermöglichen.|
| [Unterstützung für parallele Upgrades des Clusterbetriebssystems](whats-new.md#cluster-upgrade-support) | „Neu“, | Die Datendeduplizierung bietet vollständige Unterstützung für das neue Feature für [parallele Upgrades des Clusterbetriebssystems](../..//failover-clustering/cluster-operating-system-rolling-upgrade.md) von Windows Server 2016. |

## <a name="large-volume-support"></a>Unterstützung für große Volumes

**Welchen Nutzen bietet diese Änderung?**  
Um eine maximale Leistung bei der Datendeduplizierung in Windows Server 2012 R2 zu erreichen, muss die Größe von Volumes ordnungsgemäß konfiguriert werden, damit der Optimierungsauftrag mit der Geschwindigkeit von Datenänderungen Schritt halten kann. Das bedeutet, dass typischerweise nur bei Volumes mit einer Größe von maximal 10TB eine gute Leistung bei der Datendeduplizierung erreicht wird (abhängig von den Schreibmustern der Workload).

In Windows Server2016 bietet die Datendeduplizierung bei Volumes mit einer Größe von bis zu 64 TB eine hervorragende Leistung.

**Worin bestehen die Unterschiede?**  
In Windows Server 2012 R2 verwendet die Datendeduplizierungs-Auftragspipeline eine Singlethread- und E/A-Warteschlange für jedes Volume. Um eine ausreichende Geschwindigkeit der Optimierungsaufträge sicherzustellen, damit die Speichergeschwindigkeit für das Volume insgesamt nicht sinkt, müssen große Datasets in kleinere Volumes unterteilt werden. Die geeignete Volumegröße hängt von dem erwarteten Änderungsumfang für dieses Volume ab. Der Höchstwert beträgt durchschnittlich etwa 6-7TB für Volumes mit hohem Änderungsumfang und etwa 9-10TB für Volumes mit niedrigem Änderungsumfang.

In Windows Server 2016 wurde die Deduplizierungs-Auftragspipeline überarbeitet, um mithilfe mehrerer E/A-Warteschlangen für jedes Volume mehrere Threads parallel ausführen zu können. Dies führt zu Leistung, die bisher nur durch Aufteilen der Daten auf mehrere kleinere Volumes möglich war. Diese Änderung wird in der folgenden Abbildung dargestellt:

![Visualisierung zum Vergleich der Datendeduplizierungs-Auftragspipeline in Windows Server 2012 R2 und Windows Server2016](media/server-2016-dedup-job-pipeline.png)

Diese Optimierungen gelten nicht nur für den Optimierungsauftrag, sondern für [alle Datendeduplizierungsaufträge](understand.md#job-info).

## <a name="large-file-support"></a>Unterstützung für große Dateien
**Welchen Nutzen bietet diese Änderung?**  
In Windows Server 2012 R2 sind sehr große Dateien keine geeigneten Kandidaten für die Datendeduplizierung, da die Leistung der Deduplizierungs-Verarbeitungspipeline bei diesen Dateien sinkt. In Windows Server2016 wird bei der Deduplizierung von Dateien mit einer Größe von bis zu 1TB eine hervorragende Leistung erreicht, sodass Administratoren bei einer breiteren Palette von Workloads von der Deduplizierung profitieren können. Ein Beispiel ist die Deduplizierung von sehr großen Dateien, die normalerweise mit Sicherungsworkloads einhergehen.

**Worin bestehen die Unterschiede?**  
In Windows Server 2016 werden bei der Datendeduplizierung neue Streamzuordnungsstrukturen sowie weitere „verdeckte“ Verbesserungen genutzt, um den Optimierungsdurchsatz und die Zugriffsleistung zu verbessern. Darüber hinaus kann die Deduplizierungs-Verarbeitungspipeline die Optimierung jetzt nach einem Failover fortsetzen (die Optimierung muss nicht neu gestartet werden). Durch diese Änderungen wird bei der Deduplizierung von Dateien mit einer Größe von bis zu 1TB eine erstklassige Leistung erzielt.

## <a name="nano-server-support"></a>Unterstützung für Nano Server
**Welchen Nutzen bietet diese Änderung?**  
Nano Server ist eine neue monitorlose Bereitstellungsoption in Windows Server2016 mit wesentlich geringerer Systemressourcennutzung und erheblich kürzerer Startzeit, für die weniger Updates und Neustarts erforderlich sind als bei der Windows Server Core-Bereitstellungsoption. Die Datendeduplizierung wird bei Nano Server vollständig unterstützt. Weitere Informationen zu Nano Server finden Sie unter [Getting Started with Nano Server](../../get-started/getting-started-with-nano-server.md) (Erste Schritte mit Nano Server).

## <a name="simple-backup-support">Vereinfachte Konfigurationen für virtualisierte Sicherungsanwendungen</a>
**Welchen Nutzen bietet diese Änderung?**  
Die Datendeduplizierung für virtualisierte Sicherungsanwendungen wird in Windows Server 2012 R2 unterstützt, die Deduplizierungseinstellungen müssen aber bei dieser Windows Server-Version manuell angepasst und optimiert werden. Die Konfiguration der Deduplizierung für virtualisierte Sicherungsanwendungen wurde in Windows Server 2016 stark vereinfacht. Beim Aktivieren der Deduplizierung für ein Volume wird eine vordefinierte Verwendungstypoption verwendet, vergleichbar mit den Optionen für allgemeine Dateiserver und VDI.

## <a name="cluster-upgrade-support">Unterstützung für parallele Upgrades des Clusterbetriebssystems</a>
**Welchen Nutzen bietet diese Änderung?**  
Windows Server-Failovercluster, auf denen die Datendeduplizierung ausgeführt wird, können über eine Kombination aus Knoten mit Windows Server 2012 R2-Versionen der Datendeduplizierung und Windows Server 2016-Versionen der Datendeduplizierung verfügen. Diese Verbesserung ermöglicht während eines parallelen Clusterupgrades vollen Datenzugriff auf alle deduplizierten Volumes, sodass der Rollout der neuen Datendeduplizierungsversion auf einem vorhandenen Windows Server2012R2-Cluster schrittweise erfolgen kann. Auf diese Weise lässt sich Downtime verhindern, da die Knoten nicht gleichzeitig, sondern nacheinander aktualisiert werden.

**Worin bestehen die Unterschiede?**<br />
Bei früheren Versionen von Windows Server mussten alle Knoten eines Windows Server-Failoverclusters dieselbe Windows Server-Version aufweisen. Ab Windows Server2016 ermöglicht das Feature für parallele Clusterupgrades die Ausführung des Clusters im gemischten Modus. Die Datendeduplizierung unterstützt diese neue Clusterkonfiguration im gemischten Modus, um während eines parallelen Clusterupgrades vollen Datenzugriff zu ermöglichen.
