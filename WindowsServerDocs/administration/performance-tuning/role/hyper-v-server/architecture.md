---
title: Hyper-V-Architektur
description: Hyper-V-Architektur Condsiderations zum Optimieren der Leistung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fcc87b04698a44e115c8f49150fe33443f8e6a88
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890281"
---
# <a name="hyper-v-architecture"></a>Hyper-V-Architektur

Hyper-V-Funktionen eine type1-Hypervisor-basierte Architektur. Der Hypervisor virtualisiert, Prozessoren und Arbeitsspeicher und stellt Mechanismen für die virtualisierungsstapels in der Stammpartition zum Verwalten von untergeordneten Partitionen (virtuelle Computer) und Dienste, z. B. e/a-Geräte mit den virtuellen Computern verfügbar machen.

Das Stammpartition besitzt und direkten Zugriff auf die physischen e/a-Geräte. Die virtualisierungsstapels in der rootpartition stellt einen Speicher-Manager für virtuelle Computer, Verwaltungs-APIs und virtualisierte e/a-Geräte bereit. Es implementiert auch emulierte Geräte, z. B. die Datenträger-Controller von integrated Device Electronics (IDE) und Port der PS/2-Eingabegeräts und unterstützt bei synthetischen Geräten Hyper-V-spezifischer für eine höhere Leistung und niedrigere Gemeinkosten.

![Hyper-V-Hypervisor-basierte Architektur](../../media/perftune-guide-hyperv-arch.png)

Die Hyper-V-spezifischer e/a-Architektur besteht aus Virtualization Service Provider (VSPs) in der Root-Partition und Virtualisierung Dienstclients (VSCs) in der untergeordneten Partition. Jeder Dienst wird als Gerät über VMBus, verfügbar gemacht, die fungiert als ein i/o-Bus und ermöglicht die leistungsstarke Kommunikation zwischen virtuellen Computern, die Mechanismen wie z. B. freigegebenen Speicher verwenden. Das Gastbetriebssystem Plug & Play-Manager listet auf diesen Geräten, einschließlich VMBus, und lädt die geeigneten Gerätetreibern (virtual Service Clients). Andere Dienste als e/a sind auch über diese Architektur verfügbar.

Beginnend mit Windows Server 2008, das Betriebssystem Features Enlightenments um sein Verhalten zu optimieren, wenn es auf virtuellen Computern ausgeführt wird. Zu den Vorteilen gehören Senkung der Kosten der arbeitsspeichervirtualisierung, Verbessern der Skalierbarkeit mit mehreren Kernen und den Hintergrund des Gastbetriebssystems CPU-Auslastung zu verringern.

In den folgenden Abschnitten empfohlen, bewährte Methoden, die höhere Leistung auf Servern mit Hyper-V-Rolle zu erhalten.

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Server-Konfiguration](configuration.md)

-   [Hyper-V, prozessorbezogene Leistungsdaten](processor-performance.md)

-   [Hyper-V-Memory-Leistung](memory-performance.md)

-   [Hyper-V-Speicher-e/a-Leistung](storage-io-performance.md)

-   [Hyper-V-Netzwerk-e/a-Leistung](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
