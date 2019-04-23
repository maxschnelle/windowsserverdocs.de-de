---
title: Hyper-V-Memory-Leistung
description: Überlegungen zum Arbeitsspeicher in Hyper-V die Optimierung der Leistung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 63a1b654b8ac52725cc5dd87c8b245f9dfaf40f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848071"
---
# <a name="hyper-v-memory-performance"></a>Hyper-V-Memory-Leistung


Der Hypervisor virtualisiert den Gast physischen Speicher, virtuelle Computer voneinander zu isolieren und einen zusammenhängenden, nullbasierten Speicherbereich für Gastbetriebssysteme, bereitstellen, wie auf nicht virtualisierten Systemen.

## <a name="correct-memory-sizing-for-child-partitions"></a>Korrigieren Sie die größenanpassung von Arbeitsspeicher für untergeordneten Partitionen

Sie sollten die Arbeitsspeicher der virtuellen Maschine Größe, wie in der Regel für serveranwendungen auf einem physischen Computer. Sie müssen die Größe, um die erwartete Auslastung zu normalen angemessen behandeln und Spitzenzeiten, da nicht genügend Arbeitsspeicher Antwortzeiten und CPU- oder e/a-Nutzung deutlich erhöhen kann.

Sie können dynamischen Arbeitsspeicher können von Windows, die Arbeitsspeicher der virtuellen Maschine dynamisch Größe ermöglichen. Dynamischer Arbeitsspeicher Wenn große plötzliche speicherbelegung, wodurch Probleme Anwendungen auf dem virtuellen Computer können Sie erhöhen die Größe der Auslagerungsdatei für den virtuellen Computer, um temporäre Sicherung sicherzustellen, dass beim dynamischen Arbeitsspeicher auf die Auslastung des Arbeitsspeichers reagiert.

Weitere Informationen zu dynamischem Arbeitsspeicher finden Sie unter [Hyper-V dynamischer Arbeitsspeicher – Übersicht]( https://go.microsoft.com/fwlink/?linkid=834434) und [Konfigurationshandbuch für Hyper-V Dynamic Memory](https://go.microsoft.com/fwlink/?linkid=834435).

Wenn Windows in der untergeordneten Partition ausgeführt werden, können Sie die folgenden Leistungsindikatoren in einer untergeordneten Partition verwenden, um festzustellen, ob die untergeordnet Partition, dass genügend Arbeitsspeicher zur Verfügung hat und ist wahrscheinlich mit einer höheren Größe des virtuellen Computers Arbeitsspeicher eine bessere Leistung.

| Leistungsindikator                                                         | Vorgeschlagene Schwellenwert                                                                                                                                                           |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Arbeitsspeicher – Standbymodus reservieren – Cachebytes                                        | Summe der Standbymodus reservieren – Cachebytes "und" Free "und" 0 (null) Seite Liste Bytes sollte mindestens 200 MB auf Systemen mit mindestens 1 GB und 300 MB auf Systemen mit 2 GB RAM oder mehr sichtbar. |
| Speicher – freie & Nullbytes Seitenliste                                        | Summe der Standbymodus reservieren – Cachebytes "und" Free "und" 0 (null) Seite Liste Bytes sollte mindestens 200 MB auf Systemen mit mindestens 1 GB und 300 MB auf Systemen mit 2 GB RAM oder mehr sichtbar. |
| Speicher – Seiteneingabe/s                                                    | Durchschnittlichen Wert über einen Zeitraum von 1 Stunde ist kleiner als 10.                                                                                                                                       | 

## <a name="correct-memory-sizing-for-root-partition"></a>Arbeitsspeicher-größenanpassung für die Stammpartition zu beheben

Das Stammpartition müssen genügend Arbeitsspeicher, um Dienste wie z. B. e/a-Virtualisierung, VM-Momentaufnahme und Management zur Unterstützung der untergeordneten Partitionen bereitzustellen.

Hyper-V unter Windows Server 2016 überwacht die Integrität des Verwaltungsbetriebssystem der Stammpartition, um zu bestimmen, wie viel Arbeitsspeicher sicher an untergeordneten Partitionen zugeordnet werden kann und gleichzeitig gewährleistet hohe Leistung und Zuverlässigkeit von der Stammpartition Laufzeit.

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Server-Konfiguration](configuration.md)

-   [Hyper-V, prozessorbezogene Leistungsdaten](processor-performance.md)

-   [Hyper-V-Speicher-e/a-Leistung](storage-io-performance.md)

-   [Hyper-V-Netzwerk-e/a-Leistung](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
