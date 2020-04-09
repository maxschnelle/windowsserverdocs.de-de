---
title: Hyper-V-Netzwerk-e/a-Leistung
description: Überlegungen zur Netzwerk-e/a-Leistung bei der Hyper-V-Leistungsoptimierung
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 17551da6cd270f05cf2d6b1a8147958f82b2c9b3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851803"
---
# <a name="hyper-v-network-io-performance"></a>Hyper-V-Netzwerk-e/a-Leistung

Server 2016 enthält mehrere Verbesserungen und neue Funktionen zur Optimierung der Netzwerkleistung unter Hyper-V.  Eine Dokumentation zur Optimierung der Netzwerkleistung wird in einer zukünftigen Version dieses Artikels enthalten sein.

## <a name="live-migration"></a>Livemigration

Mit Livemigration können Sie die Ausführung virtueller Computer transparent von einem Knoten eines Failoverclusters auf einen anderen Knoten im gleichen Cluster verschieben, ohne dass eine Netzwerkverbindung oder eine nicht erkannte Ausfallzeiten auftreten.

> [!NOTE]
> Failoverclustering erfordert freigegebenen Speicher für die Cluster Knoten.

Der Prozess zum Verschieben eines laufenden virtuellen Computers kann in zwei Hauptphasen unterteilt werden. In der ersten Phase wird der Speicher der virtuellen Maschine vom aktuellen Host auf den neuen Host kopiert. In der zweiten Phase wird der Zustand der virtuellen Maschine vom aktuellen Host auf den neuen Host übertragen. Die Dauer beider Phasen hängt stark von der Geschwindigkeit ab, mit der Daten vom aktuellen Host auf den neuen Host übertragen werden können.

Das Bereitstellen eines dedizierten Netzwerks für den Live Migrations Datenverkehr verringert die Zeit, die zum Durchführen einer Live Migration erforderlich ist, und stellt eine konsistente Migrationszeit sicher.

![Beispiel für die Konfiguration der Hyper-v-Live Migration](../../media/perftune-guide-live-migration.png)

Außerdem kann das Erhöhen der Anzahl der Sende-und Empfangs Puffer auf jedem Netzwerkadapter, der an der Migration beteiligt ist, die Migrations Leistung verbessern.

Windows Server 2012 R2 hat eine Option eingeführt, um Livemigration zu beschleunigen, indem Sie Speicher vor der Übertragung über das Netzwerk komprimieren oder den Remote Zugriff auf den direkten Speicher (RDMA) verwenden, wenn Ihre Hardware dies unterstützt.

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Serverkonfiguration](configuration.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
