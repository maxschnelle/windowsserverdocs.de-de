---
title: Hyper-V-Architektur
description: Hyper-v-Architektur-Zusammenstellungen für die Leistungsoptimierung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 7ed8522ec34e9e262f835530a248567ebbd0ddc9
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866670"
---
# <a name="hyper-v-architecture"></a>Hyper-V-Architektur

Hyper-V verfügt über eine Hypervisor-basierte Architektur vom Typ 1. Der Hypervisor virtualisiert Prozessoren und Arbeitsspeicher und stellt Mechanismen für den Virtualisierungsstapel in der Stamm Partition bereit, um untergeordnete Partitionen (virtuelle Computer) zu verwalten und Dienste wie z. b. e/a-Geräte für die virtuellen Computer verfügbar zu machen.

Die Stamm Partition besitzt und hat direkten Zugriff auf die physischen e/a-Geräte. Der Virtualisierungsstapel in der Stamm Partition bietet einen Speicher-Manager für virtuelle Computer, Verwaltungs-APIs und virtualisierte e/a-Geräte. Außerdem werden emulierten Geräte wie der IDE-Datenträger Controller (Integrated Device Electronics) und der PS/2-Eingabe Geräteport implementiert, und Hyper-V-spezifische synthetische Geräte werden unterstützt, um die Leistung zu verbessern und den mehr Aufwand zu verringern.

![Hypervisor-basierte Hyper-v-Architektur](../../media/perftune-guide-hyperv-arch.png)

Die Hyper-V-spezifische e/a-Architektur besteht aus virtualisierungdienstanbietern (VSPS) in der Stamm Partition und den virtualisierungdienst-Clients (VSCs) in der untergeordneten Partition. Jeder Dienst wird als Gerät über VMBus bereitgestellt, das als e/a-Bus fungiert und Hochleistungs übergreifende Kommunikation zwischen virtuellen Computern ermöglicht, die Mechanismen wie Shared Memory verwenden. Der Plug & Play-Manager des Gast Betriebssystems listet diese Geräte, einschließlich VMBus, auf und lädt die entsprechenden Gerätetreiber (virtuelle Dienst Clients). Andere Dienste als e/a werden auch durch diese Architektur verfügbar gemacht.

Ab Windows Server 2008 verfügt das Betriebssystem über die entsprechenden Funktionen, um das Verhalten bei der Ausführung auf virtuellen Computern zu optimieren. Zu den Vorteilen gehören das Verringern der Kosten für die Speichervirtualisierung, das Verbessern der Skalierbarkeit von mehreren Kernen und das Verringern der CPU-Auslastung des Gast Betriebssystems.

In den folgenden Abschnitten werden bewährte Methoden für die Leistung von Servern mit Hyper-V-Rolle vorgeschlagen.

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Serverkonfiguration](configuration.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
