---
title: Hyper-V-Terminologie
description: In der Hyper-v-Leistungsoptimierung Nützliche Hyper-v-Terminologie
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: acd61e9edef3ac88027d0cc89618c537fa6aa25f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385029"
---
# <a name="hyper-v-terminology"></a>Hyper-V-Terminologie
In diesem Abschnitt wird die Schlüssel Terminologie für die Technologie virtueller Computer zusammengefasst, die in diesem Thema zur Leistungsoptimierung verwendet wird:

| Begriff        | Definition           |
| ------------- |:------------|
|*untergeordnete Partition* | Alle virtuellen Computer, die von der Stamm Partition erstellt werden.|
|*gerätevirtualisierung* | Ein Mechanismus, mit dem eine Hardware Ressource abstrahiert und von mehreren Consumern gemeinsam genutzt werden kann.|
|*emulierten Gerät*|Ein virtualisiertes Gerät, das ein tatsächliches physisches Hardware Gerät imitiert, sodass Gäste die typischen Treiber für das Hardware Gerät verwenden können.|
|*Anti*|Eine Optimierung eines Gast Betriebssystems, um die virtuellen Computerumgebungen zu erkennen und das Verhalten virtueller Maschinen zu optimieren.|
|*Gästen*|Software, die in einer Partition ausgeführt wird. Dabei kann es sich um ein Betriebssystem mit vollem Funktionsumfang oder einen kleinen, speziellen Kernel handeln. Der Hypervisor ist Gast agnostisch.|
|*hypervisor*|Eine Software Ebene, die über der Hardware und unter einem oder mehreren Betriebssystemen liegt. Ihre Hauptaufgabe ist die Ausführung isolierter Ausführungsumgebungen, die man Partitionen nennt. Jede Partition verfügt über einen eigenen Satz virtualisierter Hardware Ressourcen (zentrale Verarbeitungseinheit, CPU, Arbeitsspeicher und Geräte). Der Hypervisor steuert und vermittelt den Zugriff auf die zugrunde liegende Hardware.|
|*Logischer Prozessor*| Eine Verarbeitungseinheit, die einen Ausführungs Thread verarbeitet (Anweisungs Datenstrom). Es können ein oder mehrere logische Prozessoren pro Prozessorkern und ein oder mehrere Kerne pro Prozessor-Socket vorhanden sein.|
| *Pass-Through-Datenträger Zugriff*|Eine Darstellung eines gesamten physischen Datenträgers als virtueller Datenträger innerhalb des Gast Betriebssystems. Die Daten und Befehle werden an den physischen Datenträger (über den systemeigenen Speicher Stapel der Stamm Partition) übermittelt, ohne dass eine Verarbeitung durch den virtuellen Stapel besteht.|
|*Stamm Partition*|Die Stamm Partition, die zuerst erstellt wird und alle Ressourcen besitzt, die der Hypervisor nicht enthält, einschließlich der meisten Geräte und des System Speichers. Die Stamm Partition hostet den Virtualisierungsstapel und erstellt und verwaltet die untergeordneten Partitionen.|
|*Hyper-V-spezifisches Gerät*|Ein virtualisiertes Gerät ohne physische Hardware, sodass Gäste möglicherweise einen Treiber (virtualisierungdienst-Client) für das Hyper-V-spezifische Gerät benötigen. Der Treiber kann Virtual Machine Bus (VMBus) verwenden, um mit der virtualisierten Geräte Software in der Stamm Partition zu kommunizieren.|
|*virtueller Computer*|Ein virtueller Computer, der von der Software Emulation erstellt wurde und die gleichen Merkmale wie ein echter Computer aufweist.|
| *virtueller Netzwerk Switch*|(wird auch als virtueller Switch bezeichnet) Eine virtuelle Version eines physischen Netzwerk Schalters. ein virtuelles Netzwerk kann so konfiguriert werden, dass es für eine oder mehrere virtuelle Maschinen den Zugriff auf lokale oder externe Netzwerkressourcen bereitstellt.|
|*virtueller Prozessor*|Eine virtuelle Abstraktion eines Prozessors, der auf einem logischen Prozessor ausgeführt werden soll. Ein virtueller Computer kann über einen oder mehrere virtuelle Prozessoren verfügen.|
|*virtualisierungdienst-Client (VSC)*|Ein Softwaremodul, das ein Gast lädt, um eine Ressource oder einen Dienst zu nutzen. Für e/a-Geräte kann der virtualisierungsdienstanbieter ein Gerätetreiber sein, den der Kernel des Betriebssystems lädt.|
| *virtualisierungsdienstanbieter (VSP)*|  Ein Anbieter, der vom Virtualisierungsstapel in der Stamm Partition verfügbar gemacht wird und Ressourcen oder Dienste wie e/a-Vorgänge für eine untergeordnete Partition bereitstellt.|
| *Virtualisierungsstapel*|Eine Sammlung von Softwarekomponenten in der Stamm Partition, die zur Unterstützung virtueller Maschinen zusammenarbeiten. Der Virtualisierungsstapel funktioniert mit und befindet sich über dem Hypervisor. Außerdem werden Verwaltungsfunktionen bereitstellt.|
|*VMBus*|Kanal basierter Kommunikationsmechanismus, der für die Kommunikation zwischen Partitionen und Geräteenumeration in Systemen mit mehreren aktiven virtualisierten Partitionen verwendet wird. Die VMBus wird mit Hyper-V-Integrationsdiensten installiert.|

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Serverkonfiguration](configuration.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
