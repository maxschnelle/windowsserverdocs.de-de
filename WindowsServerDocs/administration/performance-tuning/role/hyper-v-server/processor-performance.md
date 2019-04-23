---
title: Hyper-V, Prozessorbezogene Leistungsdaten
description: Prozessor Überlegungen zur Leistung in Hyper-V zur leistungsoptimierung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 2a49fdaba89a01c8daf6483f72dbc88daa91452b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843241"
---
# <a name="hyper-v-processor-performance"></a>Hyper-V, Prozessorbezogene Leistungsdaten


## <a name="virtual-machine-integration-services"></a>VM-Integrationsdienste

Die VM-Integrationsdienste sind aktivierte Treiber für den Hyper-V-spezifischer e/a-Geräten durch CPU für e/a im Vergleich zu emulierten Geräte Aufwand reduziert. Sie sollten die neueste Version der Integrationsdienste der virtuellen Computer in jedem unterstützten virtuellen Computer installieren. Die Dienste Verringerung der CPU-Auslastung der Gäste, aus dem Leerlauf stark, Gäste Gäste verwendet und verbessert die e/a-Durchsatz. Dies ist der erste Schritt bei der Optimierung der Leistung auf einem Server mit Hyper-V. Eine Liste der Gastbetriebssysteme, finden Sie unter [Hyper-V: Übersicht](https://technet.microsoft.com/library/hh831531.aspx).

## <a name="virtual-processors"></a>Virtuelle Prozessoren

Hyper-V unter Windows Server 2016 unterstützt bis zu 240 virtuelle Prozessoren pro virtuellem Computer. Virtuelle Computer mit Lasten, die nicht die CPU-intensiv sind, sollten einen virtuellen Prozessor konfiguriert werden. Dies ist aufgrund der zusätzlichen Aufwand, der mehrere virtuelle Prozessoren, wie z. B. die Kosten für zusätzliche Synchronisierung in das Gastbetriebssystem zugeordnet ist.

Erhöhen Sie die Anzahl virtueller Prozessoren, wenn der virtuelle Computer mehr als eine CPU Verarbeitung unter Spitzenlast benötigt.

## <a name="background-activity"></a>Hintergrundaktivität

Minimierung von Hintergrundaktivitäten im Leerlauf virtuelle Computer frei CPU-Zyklen, die von anderen virtuellen Maschinen an anderer Stelle verwendet werden können. Windows-Gäste verwenden in der Regel weniger als ein Prozent einer CPU, wenn sie sich im Leerlauf befinden. Es folgen einige bewährte Methoden für die Minimierung der hintergrundnutzung CPU-Nutzung eines virtuellen Computers:

-   Installieren Sie die neueste Version der Integrationsdienste der virtuellen Computer.

-   Entfernen Sie den emulierten Netzwerkadapter über das Dialogfeld des VM-Einstellungen (Verwenden der Microsoft Hyper-V-spezifischer Adapter).

-   Entfernen Sie nicht verwendete Geräte wie z. B. den CD-ROM- und COM-Port, oder Trennen von Medien.

-   Behalten Sie das Windows-Gastbetriebssystem auf der Anmeldeseite angezeigt, wenn sie nicht verwendet wird, und deaktivieren Sie des Bildschirmschoners.

-   Überprüfen Sie die geplanten Aufgaben und Dienste, die standardmäßig aktiviert sind.

-   Überprüfen Sie die ETW-Ablaufverfolgung-Anbieter, die auf durch Ausführen standardmäßig sind **logman.exe Abfragen - Ets**

-   Verbessern Sie die Server-Anwendungen, um regelmäßige Aktivität (z. B. Zeitgeber) zu reduzieren.

-   Schließen Sie Server-Manager auf die Host- und Gastbetriebssysteme Betriebssystemen.

-   Lassen Sie nicht Hyper-V-Manager ausgeführt wird, da es ständig des virtuellen Computers Miniaturansicht aktualisiert.

Im folgenden werden weitere bewährte Methoden für die Konfiguration einer *Clientversion* von Windows auf einem virtuellen Computer aus, um die gesamte CPU-Auslastung zu verringern:

-   Deaktivieren Sie z. B. SuperFetch und Windows Search-Diensten im Hintergrund.

-   Deaktivieren Sie geplante Aufgaben z. B. geplante defragmentieren.

## <a name="virtual-numa"></a>Virtuelle NUMA

Zum ermöglichen der Virtualisierung von großen hochskalierbaren arbeitsauslastungen, erweitert die Hyper-V unter Windows Server 2016 für virtuelle Computer. Ein einzelner virtueller Computer kann bis zu 240 virtuelle Prozessoren und 12 TB Arbeitsspeicher zugewiesen werden. Wenn Sie eine solche große virtuelle Computer zu erstellen, wird wahrscheinlich Arbeitsspeicher mehrerer NUMA-Knoten, auf dem Hostsystem genutzt werden. In eine solche Konfiguration des virtuellen Computers wenn die virtuellen Prozessoren und Arbeitsspeicher nicht aus dem gleichen NUMA-Knoten zugeordnet werden Workloads schlechte Leistung aufgrund von die Unfähigkeit, die von NUMA-Optimierungen profitieren möglicherweise.

In Windows Server 2016 stellt Hyper-V virtuelle NUMA-Topologie zu virtuellen Computern. Diese virtuelle NUMA-Topologie ist standardmäßig optimiert, um mit der NUMA-Topologie des zugrunde liegenden Hostcomputers übereinzustimmen. Durch das Verfügbarmachen einer virtuellen NUMA-Topologie in einem virtuellen Computer können das Gastbetriebssystem und alle darauf ausgeführten NUMA-fähigen Anwendungen von den NUMA-Leistungsoptimierungen profitieren, so als würden sie auf einem physischen Computer ausgeführt werden.

Aus Sicht der Arbeitsauslastung gibt es keinen Unterschied zwischen einem virtuellen und physischen NUMA. Wenn eine Arbeitsauslastung in einem virtuellen Computer lokalen Arbeitsspeicher für Daten zuweist und auf die Daten im selben NUMA-Knoten zugreift, führt dies zu einem schnellen lokalen Speicherzugriff auf dem zugrunde liegenden physischen System. Leistungsbenachteiligungen aufgrund des Remotearbeitsspeicherzugriffs wird erfolgreich vermieden. Nur die NUMA-fähige Anwendungen können von vNUMA profitieren.

Microsoft SQL Server ist ein Beispiel für NUMA-fähige Anwendung. Weitere Informationen finden Sie unter [Grundlegendes zu Non-Uniform Memory Access](https://technet.microsoft.com/library/ms178144.aspx).

Die Features virtuelles NUMA und dynamischer Arbeitsspeicher können nicht gleichzeitig verwendet werden. Ein virtueller Computer mit aktiviertem dynamischen Arbeitsspeicher hat effektiv nur einen virtuellen NUMA-Knoten, und keine NUMA-Topologie wird mit dem virtuellen Computer angezeigt – unabhängig von den virtuellen NUMA-Einstellungen.

Weitere Informationen zum virtuellen NUMA, finden Sie unter [Hyper-V virtuellen NUMA (Übersicht)](https://technet.microsoft.com/library/dn282282.aspx).

##<a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Server-Konfiguration](configuration.md)

-   [Hyper-V-Memory-Leistung](memory-performance.md)

-   [Hyper-V-Speicher-e/a-Leistung](storage-io-performance.md)

-   [Hyper-V-Netzwerk-e/a-Leistung](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
