---
title: Hyper-V – Konfiguration
description: Überlegungen zur Hyper-V-Konfiguration für die Leistungsoptimierung
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 3fb1001c99e084ab69f37db9779e5d5ae7acf58e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471435"
---
# <a name="hyper-v-configuration"></a>Hyper-V – Konfiguration

## <a name="hardware-selection"></a>Hardware Auswahl

Die Hardware Überlegungen für Server, auf denen Hyper-v ausgeführt wird, ähneln in der Regel den nicht virtualisierten Servern, aber Server, auf denen Hyper-v ausgeführt wird, können eine höhere CPU-Auslastung aufweisen, mehr Speicher beanspruchen und aufgrund der Serverkonsolidierung eine größere e/a-Bandbreite

-   **Prozessoren**

    Hyper-V in Windows Server 2016 stellt die logischen Prozessoren als einen oder mehrere virtuelle Prozessoren für die einzelnen aktiven virtuellen Maschinen dar. Hyper-V erfordert nun Prozessoren, die slat (Second Level Address Translation)-Technologien wie erweiterte Seitentabellen (EPT) oder geschlagelte Seitentabellen (NVV) unterstützen.

-   **Cache**

    Hyper-V kann von größeren Prozessor Caches profitieren, insbesondere bei Lasten mit einem großen Workingset im Arbeitsspeicher und in Konfigurationen für virtuelle Maschinen, bei denen das Verhältnis zwischen virtuellen Prozessoren und logischen Prozessoren hoch ist.

-   **Arbeitsspeicher**

    Der physische Server benötigt ausreichend Arbeitsspeicher für die Stamm-und untergeordneten Partitionen. Die Stamm Partition benötigt Arbeitsspeicher, um e/a-Vorgänge im Auftrag der virtuellen Computer und Vorgänge (z. b. einer Momentaufnahme eines virtuellen Computers) effizient auszuführen. Hyper-V stellt sicher, dass genügend Arbeitsspeicher für die Stamm Partition verfügbar ist, und ermöglicht die Zuweisung von verbleibenden Arbeitsspeicher zu untergeordneten Partitionen. Untergeordnete Partitionen sollten basierend auf den Anforderungen der erwarteten Auslastung für jeden virtuellen Computer skaliert werden.

-   **Speicher**

    Die Speicherhardware muss über ausreichend e/a-Bandbreite und Kapazität verfügen, um die aktuellen und zukünftigen Anforderungen der virtuellen Maschinen zu erfüllen, die der physische Server hostet. Beachten Sie diese Anforderungen, wenn Sie Speichercontroller und Datenträger auswählen und die RAID-Konfiguration auswählen. Das Platzieren virtueller Maschinen mit stark Datenträger intensiven Workloads auf verschiedenen physischen Datenträgern führt wahrscheinlich zu einer Verbesserung der Gesamtleistung. Wenn z. b. vier virtuelle Computer einen einzelnen Datenträger gemeinsam nutzen und ihn aktiv nutzen, kann jeder virtuelle Computer nur 25% der Bandbreite des Datenträgers liefern.

## <a name="power-plan-considerations"></a>Überlegungen zum Energie Tarif

Als Kerntechnologie ist die Virtualisierung ein leistungsfähiges Tool, das für die Erhöhung der Server Arbeitsauslastung nützlich ist, die Anzahl der erforderlichen physischen Server in Ihrem Rechenzentrum verringert, die operative Effizienz erhöht und die Kosten für den Energieverbrauch reduziert. Die Energie Verwaltung ist wichtig für die Kostenverwaltung.

In einer idealen Rechenzentrumsumgebung wird der Energieverbrauch durch Konsolidieren der Arbeit auf Computern verwaltet, bis Sie größtenteils ausgelastet sind, und die Computer im Leerlauf ausschalten. Wenn dieser Ansatz nicht praktikabel ist, können Administratoren Energie Sparpläne auf den physischen Hosts nutzen, um sicherzustellen, dass Sie nicht mehr Leistung als notwendig beanspruchen.

Die Verfahren zur Server Energie Verwaltung sind mit Kosten verbunden, besonders weil Mandanten Arbeits Auslastungen nicht vertrauenswürdig sind, um Richtlinien zur physischen Infrastruktur des anheters zu überschreiben. Die Software auf der Hostebene gibt an, wie der Durchsatz maximiert werden soll, während der Energieverbrauch minimiert wird. In den Computern, die sich größtenteils im Leerlauf befinden, kann dies dazu führen, dass die physische Infrastruktur den Schluss ergibt, dass eine mittlere Stromversorgung angemessen ist, was dazu führt, dass einzelne mandantenworkloads langsamer ausgeführt werden

Windows Server verwendet die Virtualisierung in einer Vielzahl von Szenarien. Von einem leicht geladenen IIS-Server zu einem mäßig ausgelasteten SQL Server auf einen Cloud-Host mit Hyper-V, auf dem Hunderte von virtuellen Computern pro Server ausgeführt werden. Für jedes dieser Szenarien gelten möglicherweise eindeutige Hardware-, Software-und Leistungsanforderungen. Windows Server verwendet und empfiehlt standardmäßig den ausgeglichenen Energie Sparplan, der den Energie Schutz ermöglicht, indem die Prozessorleistung basierend auf der CPU-Auslastung **skaliert** wird.

Mit dem **ausgeglichenen** Energie Sparplan werden die höchsten Energiezustände (und die niedrigsten Antwortzeiten bei mandantenworkloads) nur angewendet, wenn der physische Host relativ ausgelastet ist. Wenn Sie für alle mandantenworkloads eine deterministische Antwort mit niedriger Latenz nutzen, sollten Sie einen Wechsel vom standardmäßigen **ausgeglichenen** Energie Sparplan zum **hochleistungsfähigen** Energie Sparplan in Erwägung gezogen. Mit dem **hochleistungsfähigen** Energie Sparplan werden die Prozessoren jederzeit vollständig ausgeführt, wodurch die Bedarfs gesteuerte Umstellung zusammen mit anderen Energie Verwaltungsverfahren deaktiviert und die Leistung im Vergleich zur Energieeinsparung optimiert wird.

Für Kunden, die mit den Kosteneinsparungen bei der Reduzierung der Anzahl der physischen Server zufrieden sind und sicherstellen möchten, dass Sie eine maximale Leistung für Ihre virtualisierten Workloads erzielen, sollten Sie die Verwendung des **hochleistungsfähigen** Energie Sparplans in Erwägung gezogen.

Weitere Empfehlungen und Einblicke in die Nutzung von Energie Sparplänen zur Optimierung Ihrer Infrastruktur finden Sie unter [Empfohlene ausgeglichene Energie Sparplan Parameter für schnelle Reaktionszeiten](../../hardware/power/recommended-balanced-plan-parameters.md) .



## <a name="server-core-installation-option"></a>Server Core-Installationsoption

Windows Server 2016 ist die Server Core-Installationsoption. Server Core bietet eine minimale Umgebung zum Hosten eines ausgewählten Satzes von Server Rollen, einschließlich Hyper-V. Es verfügt über einen geringeren Datenträger Bedarf für das Host Betriebssystem und eine kleinere Angriffs-und Wartungs Oberfläche. Daher wird dringend empfohlen, dass Hyper-V-Virtualisierungsserver die Server Core-Installationsoption verwenden.

Eine Server Core-Installation bietet nur dann ein Konsolenfenster, wenn der Benutzer angemeldet ist, Hyper-V aber Remote Verwaltungsfunktionen wie [Windows PowerShell](https://technet.microsoft.com/library/hh848559.aspx) verfügbar macht, damit Administratoren diese remote verwalten können.

## <a name="dedicated-server-role"></a>Dedizierte Server Rolle

Die Stamm Partition sollte für Hyper-V dediziert sein. Das Ausführen zusätzlicher Server Rollen auf einem Server, auf dem Hyper-V ausgeführt wird, kann sich negativ auf die Leistung des Virtualisierungsservers auswirken, insbesondere, wenn Sie eine beträchtliche CPU-, Arbeitsspeicher-oder e/a-Bandbreite Das Minimieren der Server Rollen in der Stamm Partition bietet weitere Vorteile, wie z. b. die Verringerung der Angriffsfläche.

System Administratoren sollten sorgfältig überlegen, welche Software in der Stamm Partition installiert ist, da sich die Gesamtleistung des Servers, auf dem Hyper-V ausgeführt wird, negativ auf die Gesamtleistung auswirken kann.

## <a name="guest-operating-systems"></a>Gast Betriebssysteme

Hyper-V unterstützt und wurde für eine Reihe von unterschiedlichen Gastbetriebssystemen optimiert. Die Anzahl virtueller Prozessoren, die pro Gast unterstützt werden, hängt vom Gast Betriebssystem ab. Eine Liste der unterstützten Gast Betriebssysteme finden Sie unter [Hyper-V Overview (Übersicht über Hyper-V](https://technet.microsoft.com/library/hh831531.aspx)).

## <a name="cpu-statistics"></a>CPU-Statistik

Hyper-V veröffentlicht Leistungsindikatoren, um das Verhalten des virtualisierungsserverservers zu bestimmen und die Ressourcenverwendung zu melden. Der Standardsatz von Tools zum Anzeigen von Leistungsindikatoren in Windows umfasst System Monitor und Logman.exe, mit denen die Hyper-V-Leistungsindikatoren angezeigt und protokolliert werden können. Die Namen der relevanten Counter-Objekte haben das Präfix **Hyper-V**.

Die CPU-Auslastung des physischen Systems sollte immer mithilfe der Leistungsindikatoren für den logischen Hyper-V-Hypervisor-Prozessor gemessen werden. Die CPU-Auslastungs Indikatoren, die der Task Manager und der System Monitor in den Stamm-und untergeordneten Partitionen melden, entsprechen nicht der tatsächlichen physischen CPU-Auslastung. Verwenden Sie die folgenden Leistungsindikatoren, um die Leistung zu überwachen:

- **Logischer Hyper-V-Hypervisor-Prozessor ( \* ) \\ % Gesamtlaufzeit** die gesamte nicht im Leerlauf befindliche Zeit der logischen Prozessoren

- **Logischer Hyper-V-Hypervisor-Prozessor ( \* ) \\ % Gast Laufzeit Zeit** für das Ausführen von Zyklen innerhalb eines Gast Betriebssystems oder innerhalb des Hosts

- **Logischer Hyper-V-Hypervisor-Prozessor ( \* ) \\ % Hypervisor Laufzeit** die Zeit, die für die Ausführung im Hypervisor aufgewendet wurde

- **Virtueller Hyper-V-Hypervisor-Stamm \* Prozessor \\ \\ ()*** misst die CPU-Auslastung der Stamm Partition.

- **Virtueller Hyper-V-Hypervisor-Prozessor ( \* ) \\ \\ *** misst die CPU-Auslastung von Gast Partitionen.


## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
