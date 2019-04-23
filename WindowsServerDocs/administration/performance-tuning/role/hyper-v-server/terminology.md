---
title: Hyper-V-Terminologie
description: Hyper-V-Terminologie, die insbesondere für die leistungsoptimierung für Hyper-V
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bc970633ff24827207eb3a27e282656f2486a6eb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841141"
---
# <a name="hyper-v-terminology"></a>Hyper-V-Terminologie
In diesem Abschnitt werden die wichtigen Begriffen, die spezifisch für das virtuelle computertechnologie, die in diesem Thema die Optimierung der Leistung verwendet wird:

| Begriff        | Definition           |
| ------------- |:------------|
|*untergeordnete partition* | Alle virtuellen Computer, die von der rootpartition erstellt wird.|
|*Gerät-Virtualisierung* | Ein Mechanismus, mit dem eine Hardware Ressource abstrahiert und von mehreren Consumern gemeinsam genutzt werden.|
|*emulierte Gerät*|Eine virtualisierte Gerät, das ein tatsächlichen physischen Hardwaregerät imitiert, sodass Gäste die typische Treiber für das Hardwaregerät verwenden können.|
|*enlightenment*|Eine Optimierung zu einem Gast-Betriebssystem aufmerksam zu machen es von Umgebungen mit virtuellen Maschinen und das Verhalten für virtuelle Computer zu optimieren.|
|*guest*|Software, die in einer Partition ausgeführt wird. Es kann ein Betriebssystem mit vollem Funktionsumfang oder einen kleinen, spezielle Kernel sein. Der Hypervisor ist die Unabhängigkeit von der Gast.|
|*hypervisor*|Eine Softwareebene, die sich über die Hardware und unter einem oder mehreren Betriebssystemen befindet. Ihre Hauptaufgabe ist die Ausführung isolierter Ausführungsumgebungen, die man Partitionen nennt. Jede Partition verfügt über einen eigenen Satz von virtualisierter Hardware-Ressourcen (Central Processing Unit oder CPU, Arbeitsspeicher und Geräte). Der Hypervisor steuert und vermittelt den Zugriff auf die zugrunde liegende Hardware.|
|*Logischer Prozessor*| Eine Verarbeitungseinheit, die von einem Thread der Ausführung (Anweisungsstream) verarbeitet. Es kann eine oder mehrere logische Prozessoren pro Prozessorkern und einen oder mehrere Kerne pro prozessorsocket vorhanden sein.|
| *Pass-Through-Datenträgerzugriff*|Eine Darstellung eines gesamten physischen Datenträgers als einen virtuellen Datenträger im Gastbetriebssystem. Die Daten und Befehle werden mit dem physikalischen Datenträger (über die rootpartition native Speicherstapel) ohne dazwischenliegende Verarbeitung durch den virtuellen Stapel übergeben.|
|*Root-partition*|Der Stammpartition, die zuerst erstellt wird und alle Ressourcen, die der Hypervisor nicht der Fall ist, einschließlich der Großteil der Geräte und den Systemspeicher besitzt. Das Stammpartition die virtualisierungsstapels hostet und erstellt und verwaltet die untergeordneten Partitionen.|
|*Hyper-V-spezifischen Gerät*|Eine virtualisierte Gerät mit keine physische Hardware Analog, also Gäste einen Treiber (Virtualization Service Client) für das Hyper-V-spezifischen Gerät möglicherweise. Der Treiber kann Bus des virtuellen Computers (VMBus) für die Kommunikation mit der Software virtualisierten Geräte in der rootpartition verwenden.|
|*virtual machine*|Ein virtueller Computer, der Softwareemulation erstellt wurde und die gleichen Eigenschaften wie der eines realen Computers.|
| *virtuelles Netzwerk-switch*|(auch als einen virtuellen Switch "bezeichnet) Eine virtuelle Version der einem physischen Netzwerkswitch. ein virtuelles Netzwerk kann so konfiguriert werden, dass es für eine oder mehrere virtuelle Maschinen den Zugriff auf lokale oder externe Netzwerkressourcen bereitstellt.|
|*virtueller Prozessor*|Eine virtuelle Abstraktion der einen Prozessor, der auf einem logischen Prozessor ausgeführt werden soll. Ein virtueller Computer kann eine oder mehrere virtuelle Prozessoren verfügen.|
|*Virtualisierung-Dienstclient (VSC)*|Ein Softwaremodul, die von ein Gast geladen wird, um eine Ressource oder einen Dienst zu nutzen. Für e/a-Geräte kann der Virtualization-Dienst-Client einen Gerätetreiber sein, den der Betriebssystemkernel zu laden.|
| *Virtualisierungs-Service-Anbieter (VSP)*|  Ein Anbieter, die von der virtualisierungsstapels in der Stammpartition verfügbar gemacht werden, die Ressourcen oder Dienste wie e/a zu einer untergeordneten Partition bereitstellt.|
| *virtualisierungsstapels*|Eine Auflistung von Softwarekomponenten in der Stammpartition, die zusammenarbeiten, um virtuelle Computer unterstützen. Die virtualisierungsstapels funktioniert mit und befindet sich oberhalb der Hypervisor. Darüber hinaus Verwaltungsfunktionen.|
|*VMBus*|Channel-basierten Kommunikationsmechanismus für die Enumeration Kommunikation und Gerät Inter-Partition, auf Systemen mit mehreren aktiven virtualisierten Partitionen verwendet wird. Die VMBus wird mit Hyper-V-Integrationsdiensten installiert.|

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Server-Konfiguration](configuration.md)

-   [Hyper-V, prozessorbezogene Leistungsdaten](processor-performance.md)

-   [Hyper-V-Memory-Leistung](memory-performance.md)

-   [Hyper-V-Speicher-e/a-Leistung](storage-io-performance.md)

-   [Hyper-V-Netzwerk-e/a-Leistung](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
