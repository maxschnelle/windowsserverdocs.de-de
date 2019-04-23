---
title: Erkennen von Engpässen in einer virtualisierten Umgebung
description: Wie Sie erkennen und beheben potenzielle Leistungsengpässe in Hyper-v
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: cdad5f0cc3b0e49ae46e975e3acc2c48a18e5f70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867531"
---
# <a name="detecting-bottlenecks-in-a-virtualized-environment"></a>Erkennen von Engpässen in einer virtualisierten Umgebung

In diesem Abschnitt erhalten Sie einige Hinweise zu überwachen, indem Sie mit dem Systemmonitor und identifizieren, in dem das Problem liegen könnte, wenn der Host oder einige der virtuellen Computer keine durchführen wie erwartet haben würden.

## <a name="processor-bottlenecks"></a>Prozessorengpässen

Hier sind einige allgemeinen Szenarien, die Prozessorengpässen verursachen könnte:

-   Eine oder mehrere logische Prozessoren werden geladen.

-   Eine oder mehrere virtuelle Prozessoren werden geladen.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Auslastung der logischen Prozessoren - \\Hyper-V Hypervisor Logical Processor (\*)\\% Gesamtausführungszeit

-   Auslastung des virtuellen Prozessors - \\virtueller Hyper-V-Hypervisor-Prozessor (\*)\\% Gesamtausführungszeit

-   Auslastung des virtuellen Prozessors - Root \\virtueller Prozessoren Hyper-V-Hypervisor-Stamm (\*)\\% Gesamtausführungszeit

Wenn die **Hyper-V Hypervisor Logical Processor (\_gesamt)\\% Gesamtlaufzeit** der Host ist überladen, da mehr als 90 % ist. Sie sollten mehr verarbeitungsleistung hinzufügen oder verschieben einige virtuelle Computer auf einen anderen Host.

Wenn die **virtuelle Hyper-V-Hypervisor-Processor(VM Name:VP x)\\% Gesamtlaufzeit** Zähler ist mehr als 90 % für alle virtuellen Prozessoren, sollten Sie Folgendes tun:

-   Stellen Sie sicher, dass der Host nicht überlastet ist

-   Erfahren Sie, wenn die arbeitsauslastung mehr virtuellen Prozessoren nutzen können

-   Weisen Sie weitere virtuellen Prozessoren mit dem virtuellen Computer

Wenn **virtuelle Hyper-V-Hypervisor-Processor(VM Name:VP x)\\% Gesamtlaufzeit** Zähler ist mehr als 90 % für einige, aber nicht alle der virtuellen Prozessoren, sollten Sie Folgendes tun:

-   Wenn Ihre Workload ist netzwerkintensive erhalten, sollten Sie mit vRSS.

-   Wenn die virtuellen Computer nicht mit Windows Server 2012 R2 ausgeführt werden, sollten Sie weitere Netzwerkadapter hinzufügen.

-   Wenn Ihre Workload speicherintensiv ist, sollten Sie aktivieren Sie den virtuellen NUMA und fügen weitere virtuelle Datenträger.

Wenn die **virtueller Prozessor für Hyper-V-Hypervisor Stamm (Root VP X)\\% Gesamtlaufzeit** Leistungsindikator ist mehr als 90 % für einige, aber nicht alle virtuellen Prozessoren und die **Prozessor (X)\\Interruptzeit und Prozessor (X)\\% DPC-Zeit** Leistungsindikator ungefähr addiert den Wert für die **Stamm virtuellen Processor(Root VP x)\\% Gesamtlaufzeit** Leistungsindikator, sollten Sie sicherstellen VMQ auf Aktivieren die Netzwerkadapter.

## <a name="memory-bottlenecks"></a>Speicherengpässe

Hier sind einige allgemeinen Szenarien, die Arbeitsspeicher-Engpässe verursachen könnte:

-   Der Host reagiert nicht.

-   Virtuelle Computer kann nicht gestartet werden.

-   Virtuelle Computer ausführen, nicht genügend Arbeitsspeicher.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Arbeitsspeicher\\"Verfügbare MB"

-   Hyper-V dynamischer Arbeitsspeicherausgleich (\*)\\verfügbarer Speicher

Sie können die folgenden Leistungsindikatoren aus dem virtuellen Computer verwenden:

-   Arbeitsspeicher\\"Verfügbare MB"

Wenn die **Arbeitsspeicher\\"Verfügbare MB"** und **Hyper-V-Ausgleichsmodul für dynamischen Arbeitsspeicher (\*)\\verfügbaren Arbeitsspeicher** Indikatoren auf dem Host mit niedriger sind, sollten Sie beenden vermeidbare Dienste und eine oder mehrere virtuelle Computer auf einen anderen Host migrieren.

Wenn die **Arbeitsspeicher\\"Verfügbare MB"** Indikator auf dem virtuellen Computer mit niedriger ist, sollten Sie den virtuellen Computer mehr Arbeitsspeicher zuweisen. Wenn Sie dynamischen Arbeitsspeicher verwenden, sollten Sie die Einstellung für den maximalen Arbeitsspeicher erhöhen.

## <a name="network-bottlenecks"></a>Netzwerkengpässe

Hier sind einige allgemeinen Szenarien, die den Engpässe verursachen könnte:

-   Der Host ist Netzwerk gebunden.

-   Der virtuelle Computer ist Netzwerk gebunden.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Netzwerkschnittstelle (*Namen des Netzwerkadapters*)\\Bytes/Sek.

Sie können die folgenden Leistungsindikatoren aus dem virtuellen Computer verwenden:

-   Virtuelle Hyper-V-Netzwerkadapter (*Name des virtuellen Computers namens&lt;GUID&gt;*)\\Bytes/Sek.

Wenn die **physische NIC Bytes/Sek.** Leistungsindikator größer oder gleich 90 % der Kapazität ist, sollte die zusätzliche Netzwerkadapter hinzufügen, Migrieren von virtuellen Computern auf einen anderen Host und Konfigurieren von Netzwerk-QoS.

Wenn die **virtuellen Hyper-V-Netzwerkadapter Bytes/Sek.** Leistungsindikator größer oder gleich 250 Mbit/s ist, sollten Sie Hinzufügen zusätzlicher kombinierten Netzwerkadapter auf dem virtuellen Computer, aktivieren Sie vRSS und SR-IOV verwenden.

Wenn Ihre Workloads die Netzwerklatenz nicht erfüllen können, aktivieren Sie SR-IOV auf vorhandenen Ressourcen zum physischen Netzwerk-Adapter mit dem virtuellen Computer.

## <a name="storage-bottlenecks"></a>Speicherengpässe

Hier sind einige allgemeinen Szenarien, die Speicherengpässe verursachen könnte:

-   Der Host und virtueller Computer, die Vorgänge sind langsam oder Timeout.

-   Der virtuelle Computer ist langsam.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Physischer Datenträger (*Datenträger Buchstaben*)\\durchschn. Sek./Lesevorgänge

-   Physischer Datenträger (*Datenträger Buchstaben*)\\durchschn. Sek./Schreibvorgänge

-   Physischer Datenträger (*Datenträger Buchstaben*)\\mittlere Länge der Warteschlange zu lesen

-   Physischer Datenträger (*Datenträger Buchstaben*)\\mittlere Länge der Warteschlange zu schreiben

Wenn die Wartezeiten konstant größer als 50 ms sind, sollten Sie Folgendes:

-   Verteilen von virtuellen Computern für zusätzlichen Speicher

-   Beachten Sie, Erwerb schneller Speicher

-   Betrachten Sie mehrstufige Speicherplätze, die in Windows Server 2012 R2 eingeführt wurde

-   Erwägen Sie die Verwendung von Windows Server 2012 R2 eingeführten Speicher-QoS

-   Verwenden Sie die VHDX

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Server-Konfiguration](configuration.md)

-   [Hyper-V, prozessorbezogene Leistungsdaten](processor-performance.md)

-   [Hyper-V-Memory-Leistung](memory-performance.md)

-   [Hyper-V-Speicher-e/a-Leistung](storage-io-performance.md)

-   [Hyper-V-Netzwerk-e/a-Leistung](network-io-performance.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
