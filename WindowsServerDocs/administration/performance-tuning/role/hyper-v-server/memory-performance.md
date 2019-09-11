---
title: Hyper-V-Speicherleistung
description: Überlegungen zum Arbeitsspeicher bei der Leistungsoptimierung in Hyper
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: ddb336e0d6e16342dd60f2f61e50afeda61837e9
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866578"
---
# <a name="hyper-v-memory-performance"></a>Hyper-V-Speicherleistung


Der Hypervisor virtualisiert den physischen Gast Speicher, um virtuelle Maschinen voneinander zu isolieren und um einen zusammenhängenden, NULL basierten Speicherbereich für jedes Gast Betriebssystem bereitzustellen, ebenso wie auf nicht virtualisierten Systemen.

## <a name="correct-memory-sizing-for-child-partitions"></a>Korrekte Arbeitsspeicher Größe für untergeordnete Partitionen

Sie sollten die Größe des Arbeitsspeichers der virtuellen Maschine in der Regel für Server Anwendungen auf einem physischen Computer anpassen. Sie müssen die Größe anpassen, um die erwartete Auslastung zu normalen und Spitzenzeiten zu verarbeiten, da nicht genügend Arbeitsspeicher die Reaktionszeiten und die CPU-oder e/a-Auslastung erheblich erhöhen kann.

Sie können dynamischer Arbeitsspeicher aktivieren, damit Windows den Arbeitsspeicher der virtuellen Maschine dynamisch anpassen kann. Wenn dynamischer Arbeitsspeicher bei Anwendungen auf dem virtuellen Computerprobleme auftreten, die zu großen plötzlichen Speicher Belegungen führen, können Sie die Größe der Auslagerungs Datei für den virtuellen Computer erhöhen, um eine vorübergehende Sicherung sicherzustellen, während dynamischer Arbeitsspeicher auf die Arbeitsspeicher Auslastung antwortet.

Weitere Informationen zu dynamischer Arbeitsspeicher finden Sie unter [Hyper-v dynamischer Arbeitsspeicher Übersicht]( https://go.microsoft.com/fwlink/?linkid=834434) und [Hyper-v dynamischer Arbeitsspeicher Konfigurations Handbuch](https://go.microsoft.com/fwlink/?linkid=834435).

Wenn Sie in der untergeordneten Partition Windows ausführen, können Sie die folgenden Leistungsindikatoren in einer untergeordneten Partition verwenden, um zu ermitteln, ob die untergeordnete Partition Arbeitsspeicher belegt und wahrscheinlich besser mit einer höheren Arbeitsspeicher Größe für virtuelle Computer ausgeführt wird.

| Leistungs Zählers                                                         | Vorgeschlagene Schwellenwert                                                                                                                                                           |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Arbeitsspeicher – reservierte Bytes im standbycache                                        | Die Summe der reservierten Bytes für den standbycache und die Anzahl der freien und null-Seiten Listen sollte 200 MB oder mehr auf Systemen mit 1 GB und 300 MB oder mehr auf Systemen mit mindestens 2 GB sichtbarem RAM betragen. |
| Arbeitsspeicher – freie & NULL-Seitenliste (Bytes)                                        | Die Summe der reservierten Bytes für den standbycache und die Anzahl der freien und null-Seiten Listen sollte 200 MB oder mehr auf Systemen mit 1 GB und 300 MB oder mehr auf Systemen mit mindestens 2 GB sichtbarem RAM betragen. |
| Arbeitsspeicher – Seiten Eingabe/Sek.                                                    | Der Durchschnitt über einen Zeitraum von 1 Stunde ist kleiner als 10.                                                                                                                                       | 

## <a name="correct-memory-sizing-for-root-partition"></a>Korrigieren der Arbeitsspeicher Größe für die Stamm Partition

Die Stamm Partition muss über ausreichend Arbeitsspeicher verfügen, um Dienste wie die e/a-Virtualisierung, die Momentaufnahme des virtuellen Computers und die Verwaltung zur Unterstützung der untergeordneten Partitionen bereitzustellen.

Hyper-V in Windows Server 2016 überwacht den Lauf Zeit Zustand des Verwaltungs Betriebssystems der Stamm Partition, um zu bestimmen, wie viel Arbeitsspeicher den untergeordneten Partitionen sicher zugeordnet werden kann, während gleichzeitig hohe Leistung und Zuverlässigkeit der Stamm Partition sichergestellt werden.

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Serverkonfiguration](configuration.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
