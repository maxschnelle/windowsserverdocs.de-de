---
title: Hyper-V-Prozessorleistung
description: Überlegungen zur Prozessorleistung bei der Hyper-V-Leistungsoptimierung
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 5d61d0e37bd80033bfcfb0cf5c601d8bcedda104
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370041"
---
# <a name="hyper-v-processor-performance"></a>Hyper-V-Prozessorleistung


## <a name="virtual-machine-integration-services"></a>Integration Services für virtuelle Computer

Der virtuelle Computer Integration Services enthält aktivierte Treiber für die Hyper-V-spezifischen e/a-Geräte, wodurch der CPU-Overhead für e/a-Vorgänge im Vergleich zu emulierten Geräten erheblich reduziert wird. Sie sollten die neueste Version des virtuellen Computers Integration Services in jedem unterstützten virtuellen Computer installieren. Die Dienste verringern die CPU-Auslastung der Gäste, von den Gastbetriebssystemen auf häufig genutzte Gäste und verbessern den e/a-Durchsatz. Dies ist der erste Schritt beim Optimieren der Leistung auf einem Server, auf dem Hyper-V ausgeführt wird. Eine Liste der unterstützten Gast Betriebssysteme finden Sie unter [Hyper-V: Übersicht](https://technet.microsoft.com/library/hh831531.aspx).

## <a name="virtual-processors"></a>Virtuelle Prozessoren

Hyper-V in Windows Server 2016 unterstützt maximal 240 virtuelle Prozessoren pro virtuellem Computer. Virtuelle Computer mit Lasten, die nicht CPU-intensiv sind, sollten für die Verwendung eines einzelnen virtuellen Prozessors konfiguriert werden. Dies liegt an dem zusätzlichen mehr Aufwand, der mehreren virtuellen Prozessoren zugeordnet ist, z. b. zusätzlichen Synchronisierungs Kosten im Gast Betriebssystem.

Erhöhen Sie die Anzahl virtueller Prozessoren, wenn der virtuelle Computer bei Spitzenlast mehr als eine CPU-Verarbeitung erfordert.

## <a name="background-activity"></a>Hintergrund Aktivität

Wenn Sie die Hintergrund Aktivität auf virtuellen Computern im Leerlauf minimieren, werden CPU-Zyklen freigegeben, die von anderen virtuellen Maschinen verwendet werden können. Windows-Gäste verwenden normalerweise weniger als einen Prozentsatz einer CPU, wenn Sie sich im Leerlauf befinden. Im folgenden finden Sie einige bewährte Methoden zum Minimieren der CPU-Auslastung eines virtuellen Computers:

-   Installieren Sie die neueste Version der virtuellen Maschine Integration Services.

-   Entfernen Sie den emulierten Netzwerkadapter über das Dialogfeld "Einstellungen der virtuellen Maschine" (verwenden Sie den Microsoft Hyper-V spezifischen Adapter).

-   Entfernen Sie nicht verwendete Geräte, z. b. CD-ROM und com-Port, oder trennen Sie Ihre Medien.

-   Behalten Sie das Windows-Gast Betriebssystem auf dem Anmeldebildschirm bei, wenn es nicht verwendet wird, und deaktivieren Sie den Bildschirmschoner.

-   Überprüfen Sie die geplanten Tasks und Dienste, die standardmäßig aktiviert sind.

-   Überprüfen Sie die ETW-Ablauf Verfolgungs Anbieter, die standardmäßig aktiviert sind, indem Sie **logman. exe Query-ETS ausführen.**

-   Verbessern von Server Anwendungen, um regelmäßige Aktivitäten (z. b. Timer) zu reduzieren

-   Schließen Sie Server-Manager sowohl auf dem Host-als auch auf dem Gast Betriebssystem.

-   Lassen Sie den Hyper-V-Manager nicht ausführen, da die Miniaturansicht des virtuellen Computers ständig aktualisiert wird.

Im folgenden finden Sie weitere bewährte Methoden zum Konfigurieren einer *Client Version* von Windows auf einem virtuellen Computer, um die CPU-Gesamtauslastung zu reduzieren:

-   Deaktivieren Sie Hintergrunddienste wie SuperFetch und Windows Search.

-   Deaktivieren Sie geplante Aufgaben, z. b. geplante Defragmentierung.

## <a name="virtual-numa"></a>Virtuelle NUMA

Um die Virtualisierung von großen hochskalierbaren Arbeits Auslastungen zu ermöglichen, wurden von Hyper-V in Windows Server 2016 die Skalierungs Grenzwerte virtueller Computer erweitert. Einem einzelnen virtuellen Computer können bis zu 240 virtuelle Prozessoren und 12 TB Arbeitsspeicher zugewiesen werden. Wenn Sie solche großen virtuellen Maschinen erstellen, wird wahrscheinlich der Arbeitsspeicher von mehreren NUMA-Knoten auf dem Host System genutzt. Wenn virtuelle Prozessoren und Arbeitsspeicher nicht über denselben NUMA-Knoten zugeordnet werden, kann es bei der Konfiguration einer virtuellen Maschine zu einer ungültigen Leistung kommen, da die NUMA-Optimierungen nicht genutzt werden können.

In Windows Server 2016 stellt Hyper-V virtuellen Computern eine virtuelle NUMA-Topologie zur Auswahl. Diese virtuelle NUMA-Topologie ist standardmäßig optimiert, um mit der NUMA-Topologie des zugrunde liegenden Hostcomputers übereinzustimmen. Durch das Verfügbarmachen einer virtuellen NUMA-Topologie in einem virtuellen Computer können das Gastbetriebssystem und alle darauf ausgeführten NUMA-fähigen Anwendungen von den NUMA-Leistungsoptimierungen profitieren, so als würden sie auf einem physischen Computer ausgeführt werden.

Es gibt keinen Unterschied zwischen einem virtuellen und einem physischen NUMA aus der Sicht der Arbeitsauslastung. Wenn eine Arbeitsauslastung in einem virtuellen Computer lokalen Arbeitsspeicher für Daten zuweist und auf die Daten im selben NUMA-Knoten zugreift, führt dies zu einem schnellen lokalen Speicherzugriff auf dem zugrunde liegenden physischen System. Leistungsbenachteiligungen aufgrund des Remotearbeitsspeicherzugriffs wird erfolgreich vermieden. Nur NUMA-fähige Anwendungen können von vnuma profitieren.

Microsoft SQL Server ist ein Beispiel für eine NUMA-fähige Anwendung. Weitere Informationen finden Sie Untergrund Legendes zum [nicht einheitlichen Speicherzugriff](https://technet.microsoft.com/library/ms178144.aspx).

Die Features virtuelles NUMA und dynamischer Arbeitsspeicher können nicht gleichzeitig verwendet werden. Ein virtueller Computer mit aktiviertem dynamischen Arbeitsspeicher hat effektiv nur einen virtuellen NUMA-Knoten, und keine NUMA-Topologie wird mit dem virtuellen Computer angezeigt – unabhängig von den virtuellen NUMA-Einstellungen.

Weitere Informationen zu virtuellem NUMA finden Sie unter [virtueller Hyper-V-NUMA (Übersicht](https://technet.microsoft.com/library/dn282282.aspx)).

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Serverkonfiguration](configuration.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
