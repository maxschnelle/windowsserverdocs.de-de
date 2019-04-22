---
title: Hyper-V-Netzwerk-e/a-Leistung
description: Netzwerk-e/a-Überlegungen zur Leistung in Hyper-V zur leistungsoptimierung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: d52c4fff6c7e06fb0a9f2b44ea51a0a790e6674d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814361"
---
# <a name="hyper-v-network-io-performance"></a>Hyper-V-Netzwerk-e/a-Leistung

Server 2016 enthält verschiedene Verbesserungen und neue Funktionen zum Optimieren der Leistung des Netzwerks unter Hyper-V.  Dokumentation zum Optimieren der Leistung des Netzwerks wird in einer zukünftigen Version dieses Artikels enthalten sein.

## <a name="live-migration"></a>Livemigration

Live-Migration können Sie transparent verschieben aktiver virtueller Computer von einem Knoten eines Failoverclusters auf einen anderen Knoten im selben Cluster ohne eine Unterbrechung der Netzwerkverbindung oder wahrgenommene Ausfallzeit.

**Beachten Sie**    Failover-Clusterunterstützung erfordert freigegebenen Speicher für die Clusterknoten.

Der Prozess der Verschiebung eines ausgeführten virtuellen Computers kann in zwei Hauptphasen unterteilt werden. Die erste Phase kopiert Arbeitsspeicher des virtuellen Computers aus dem aktuellen Host auf den neuen Host. In der zweite Phase werden die Status des virtuellen Computers aus dem aktuellen Host auf den neuen Host übertragen. Die Dauer von beiden Phasen richtet sich erheblich durch die Geschwindigkeit, mit der Daten aus dem aktuellen Host auf den neuen Host übertragen werden können.

Für die Livemigration Datenverkehr minimiert die Zeit, die erforderlich sind, um eine live-Migration abzuschließen, und stellt eine konsistente Migrationszeiten ein dediziertes Netzwerk bereitstellen.

![Beispielkonfiguration für hyper-V-Livemigration](../../media/perftune-guide-live-migration.png)

Darüber hinaus Erhöhen der Anzahl von senden und Empfangen von Puffern in jedem Netzwerk kann Adapter, die bei der Migration ist die migrationsleistung verbessern.

Windows Server 2012 R2 eingeführt eine Option zum Beschleunigen der Livemigration durch Komprimieren von Arbeitsspeicher, bevor über das Netzwerk übertragen, oder verwenden Sie Remote Direct Memory Access (RDMA), wenn Ihre Hardware unterstützt.

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Server-Konfiguration](configuration.md)

-   [Hyper-V, prozessorbezogene Leistungsdaten](processor-performance.md)

-   [Hyper-V-Memory-Leistung](memory-performance.md)

-   [Hyper-V-Speicher-e/a-Leistung](storage-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
