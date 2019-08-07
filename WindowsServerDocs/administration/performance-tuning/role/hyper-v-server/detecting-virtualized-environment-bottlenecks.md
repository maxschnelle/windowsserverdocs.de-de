---
title: Erkennen von Engpässen in einer virtualisierten Umgebung
description: Erkennen und beheben potenzieller Leistungsengpässe bei Hyper-v
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: cdad5f0cc3b0e49ae46e975e3acc2c48a18e5f70
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/31/2019
ms.locfileid: "63722880"
---
# <a name="detecting-bottlenecks-in-a-virtualized-environment"></a>Erkennen von Engpässen in einer virtualisierten Umgebung

In diesem Abschnitt finden Sie einige Hinweise dazu, was Sie mit dem System Monitor überwachen müssen, und wie Sie ermitteln können, wo das Problem möglicherweise auftritt, wenn der Host oder einige der virtuellen Maschinen nicht wie erwartet ausgeführt werden.

## <a name="processor-bottlenecks"></a>Prozessor Engpässe

Im folgenden finden Sie einige häufige Szenarien, die Prozessor Engpässe verursachen können:

-   Mindestens ein logischer Prozessor wird geladen.

-   Mindestens ein virtueller Prozessor wird geladen.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Auslastung des logischen Prozessors: logischer Hyper-V-Hypervisor\\- \\Prozessor (\*)% Gesamtlaufzeit

-   Auslastung des virtuellen Prozessors-virtueller Hyper-V-Hypervisor\\- \\Prozessor (\*)% Gesamtlaufzeit

-   Auslastung des virtuellen Prozessor Stamms-virtueller Hyper-V-Hypervisor\*-\\ \\Stamm Prozessor ()% Gesamtlaufzeit

Wenn der **logische Prozessor des Hyper-V-Hypervisor-\\Prozessors (\_gesamt)% der Lauf** Zeit Zahl über 90% beträgt, wird der Host überladen. Sie sollten eine höhere Verarbeitungsleistung hinzufügen oder einige virtuelle Maschinen auf einen anderen Host verschieben.

Wenn der **virtuelle Hyper-V-Hypervisor-Prozessor (VM-Name:\\VP x)% Total Runtime** Counter für alle virtuellen Prozessoren mehr als 90% beträgt, sollten Sie die folgenden Schritte ausführen:

-   Überprüfen, ob der Host nicht überladen ist

-   Ermitteln, ob die Arbeitsauslastung mehr virtuelle Prozessoren nutzen kann

-   Zuweisen von mehr virtuellen Prozessoren zum virtuellen Computer

Wenn der **virtuelle Hyper-V-Hypervisor-Prozessor (VM-Name\\: VP x)% Total Runtime** Counter bei einigen, jedoch nicht allen virtuellen Prozessoren mehr als 90% beträgt, sollten Sie die folgenden Schritte ausführen:

-   Wenn Ihre Arbeitsauslastung Netzwerk intensiv ist, sollten Sie die Verwendung von vrss in Erwägung gezogen.

-   Wenn auf den virtuellen Computern nicht Windows Server 2012 R2 ausgeführt wird, sollten Sie weitere Netzwerkadapter hinzufügen.

-   Wenn Ihre Arbeitsauslastung Speicher intensiv ist, sollten Sie virtuelle NUMA aktivieren und weitere virtuelle Datenträger hinzufügen.

Wenn der **virtuelle Hyper-V-Hypervisor-Stamm Prozessor (Stamm-\\VP x)% Total Runtime** Counter für einige, aber nicht für alle virtuellen Prozessoren und Prozessor **(x)\\% Interruptzeit und Prozessor (x)\\% DPC-Zeit mehr als 90% beträgt** der Leistungs-Leistungs-Leistungs-Wert addiert den Wert für den Stamm- **virtuellen Prozessor\\(Stamm-VP x) "% Total Runtime** Counter". Sie sollten die Aktivierung von VMQ auf den Netzwerkadaptern sicherstellen

## <a name="memory-bottlenecks"></a>Arbeitsspeicher Engpässe

Im folgenden finden Sie einige häufige Szenarien, die Arbeitsspeicher Engpässe verursachen können:

-   Der Host reagiert nicht.

-   Virtuelle Maschinen können nicht gestartet werden.

-   Nicht genügend Arbeitsspeicher für virtuelle Computer.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Verfüg\\barer Arbeitsspeicher (MB)

-   Verfügbarer Arbeitsspeicher für Hyper-\*V\\dynamischer Arbeitsspeicher Balancer ()

Sie können die folgenden Leistungsindikatoren auf dem virtuellen Computer verwenden:

-   Verfüg\\barer Arbeitsspeicher (MB)

Wenn die Leistungsindikatoren verfügbarer Arbeits **Speicher\\** **(MB) und Hyper-\*V\\dynamischer Arbeitsspeicher Balancer ()** auf dem Host niedrig sind, sollten Sie nicht erforderliche Dienste anhalten und mindestens ein virtuelles Computer auf einem anderen Host.

Wenn der virtuelle Computer im Arbeits **\\Speicher verfügbare** MB nicht verfügbar ist, sollten Sie dem virtuellen Computer mehr Arbeitsspeicher zuweisen. Wenn Sie dynamischer Arbeitsspeicher verwenden, sollten Sie die Einstellung für den maximalen Arbeitsspeicher erhöhen.

## <a name="network-bottlenecks"></a>Netzwerk Engpässe

Im folgenden finden Sie einige häufige Szenarien, die zu Netzwerk Engpässen führen können:

-   Der Host ist Netzwerk gebunden.

-   Der virtuelle Computer ist Netzwerk gebunden.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Netzwerkschnittstelle (*Netzwerkadapter Name*)\\Bytes/Sek.

Sie können die folgenden Leistungsindikatoren auf dem virtuellen Computer verwenden:

-   Hyper-V-Virtual Network Adapter (Name der VM-*namens&gt;&lt;-GUID*)\\Bytes/Sek.

Wenn der Leistungswert für **physische NIC-Bytes/Sek** . größer als oder gleich 90% der Kapazität ist, sollten Sie zusätzliche Netzwerkadapter hinzufügen, virtuelle Maschinen zu einem anderen Host migrieren und Netzwerk-QoS konfigurieren.

Wenn der Wert für den Wert des **Hyper-V-Virtual Network Adapters für Bytes/Sek** . größer oder gleich 250 Mbit/s ist, sollten Sie zusätzliche Netzwerkadapter in der virtuellen Maschine hinzufügen, vrss aktivieren und SR-IOV verwenden.

Wenn Ihre Workloads Ihre Netzwerk Latenz nicht erreichen können, aktivieren Sie SR-IOV, um dem virtuellen Computer physische Netzwerkadapter Ressourcen bereitzustellen.

## <a name="storage-bottlenecks"></a>Speicher Engpässe

Im folgenden finden Sie einige häufige Szenarien, die Speicher Engpässe verursachen können:

-   Der Host und die Vorgänge der virtuellen Maschine sind langsam oder Timeout.

-   Der virtuelle Computer ist träge.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Physischer Datenträger(Datenträger\\Buchstabe) \ Mittlere Sek./Lesevorgänge

-   Physischer Datenträger(Datenträger\\Buchstabe) Mittlere Sek./Schreibvorgänge

-   Physischer Datenträger(Datenträger\\Buchstabe) Durchschn. Warteschlangen Länge des Datenträgers

-   Physischer Datenträger(Datenträger\\Buchstabe) Durchschn. Warteschlangen Länge des Datenträgers

Wenn die Latenzzeit konstant größer als 50 ms ist, sollten Sie folgende Schritte ausführen:

-   Verteilen virtueller Maschinen auf zusätzlichen Speicher

-   Kauf eines schnelleren Speichers in Erwägung gezogen

-   Beachten Sie Tiered Storage Leerzeichen, die in Windows Server 2012 R2 eingeführt wurden.

-   Verwenden Sie ggf. QoS für Speicher, das in Windows Server 2012 R2 eingeführt wurde.

-   Verwenden von vhdx

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Serverkonfiguration](configuration.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
