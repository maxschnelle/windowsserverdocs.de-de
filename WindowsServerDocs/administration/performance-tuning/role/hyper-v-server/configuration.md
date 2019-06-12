---
title: Hyper-V – Konfiguration
description: Hyper-V-Konfiguration-Überlegungen zum Optimieren der Leistung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: baea091482818c581414ba1d9c1c01db2a52e3d7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435663"
---
# <a name="hyper-v-configuration"></a>Hyper-V – Konfiguration

## <a name="hardware-selection"></a>Hardwareauswahl

Die Überlegungen zur Hardware für Server mit Hyper-V in der Regel ähneln denen der Server nicht virtualisiert, Server mit Hyper-V können jedoch weisen eine höhere CPU-Auslastung, erfordert mehr Arbeitsspeicher und benötigen größere e/a-Bandbreite aufgrund der serverkonsolidierung.

-   **Prozessoren**

    Hyper-V unter Windows Server 2016 stellt die logischen Prozessoren, als eine oder mehrere virtuelle Prozessoren zu jedem aktiven virtuellen Computer. Hyper-V erfordert jetzt die Prozessoren, die Second Level Address Translation (SLAT)-Technologien wie z. B. Extended Page Tables (EPT) oder Nested Page Tables (NPT) zu unterstützen.

-   **Cache**

    Hyper-V kann größere Caches für den Prozessor, insbesondere bei Lasten nutzen, die eine große Arbeitssatz im Arbeitsspeicher und in die Konfiguration der virtuellen Maschinen in denen das Verhältnis von virtuellen Prozessoren zu logischen Prozessoren hoch ist.

-   **Arbeitsspeicher**

    Der physische Server erfordert ausreichend Arbeitsspeicher für die sowohl den Stamm und untergeordneten Partitionen. Das Stammpartition erfordert Arbeitsspeicher, um effizient die e/as für die virtuellen Computer und Vorgänge wie z. B. eine Momentaufnahme des virtuellen Computers auszuführen. Hyper-V stellt sicher, dass genügend Arbeitsspeicher auf der Stammpartition verfügbar ist, und ermöglicht es, des verbleibenden Arbeitsspeichers untergeordneten Partitionen zugewiesen werden. Größe untergeordneten Partitionen müssen je nach den Anforderungen der erwarteten Last für jeden virtuellen Computer angepasst werden.

-   **Speicher**

    Die Speicherhardware sollte genügend e/a-Bandbreite und die Kapazität zum Erfüllen der aktuellen und zukünftigen Anforderungen des virtuellen Computer, die dem physischen Server gehostet. Berücksichtigen Sie diese Anforderungen, wenn Sie, Speichercontroller und Festplatten auswählen, und wählen Sie die RAID-Konfiguration. Platzieren virtuelle Computer mit sehr festplattenintensiven arbeitsauslastungen auf unterschiedlichen physischen Datenträgern wird wahrscheinlich die gesamtleistung verbessern. Wenn vier virtuellen Computern ein einzelnes Datenträgers freigeben und aktiv verwenden, kann jeder virtuelle Computer z. B. nur 25 Prozent der Bandbreite des Datenträgers führen.

## <a name="power-plan-considerations"></a>Überlegungen zum Wiederherstellungsplan "Power"

Eine Core-Technologie und ist die Virtualisierung ein leistungsfähiges Tool, das in die Dichte der Server-arbeitsauslastung steigen, Reduzieren der Anzahl der erforderlichen physischen Servern in Ihrem Datencenter, die betriebliche Effizienz steigern und die Reduzierung der Stromkosten nützlich. Energieverwaltung ist entscheidend für Cost Management. 

In einer idealen Datacenter-Umgebung wird Stromverbrauch von Aufgaben auf Computern konsolidieren, bis sie größtenteils ausgelastet sind, und klicken Sie dann im Leerlauf Computer ausschalten verwaltet. Wenn dieser Ansatz nicht möglich ist, können Administratoren Energiesparpläne auf physischen Hosts, um sicherzustellen, dass sie nicht zwingend, dass mehr Energie als nötig nutzen. 

Power Management-Serververfahren haben Ihren Preis, insbesondere, wenn Mandanten Workloads sind nicht vertrauenswürdig ist und die physische Infrastruktur, die Hoster Richtlinie zu bestimmen. Die Layer-Hostsoftware bleibt wie Durchsatz zu maximieren und gleichzeitig der Stromverbrauch minimiert abgeleitet werden soll. Auf Computern vor allem im Leerlauf befindet kann dies verursachen, die physische Infrastruktur zum Abschließen, moderate Leistungsaufnahme eignet sich, was zu einzelnen Mandanten-arbeitsauslastungen, die langsamer als sie andernfalls möglicherweise ausgeführt.

Windows Server verwendet die Virtualisierung in einer Vielzahl von Szenarien. Von einem geringfügig ausgelasteten IIS-Server zu SQL Server nicht so ausgelastet um einen Cloud-Host mit Hyper-V ausgeführt Hunderte virtueller Computer pro Server. Jedes dieser Szenarien möglicherweise die besonderen Anforderungen für Hardware, Software und Leistung. Standardmäßig verwendet WindowsServer und empfiehlt die **ausgeglichen** Energiesparplan dadurch energieeinsparung durch die Skalierung der prozessorleistung basierend auf der CPU-Auslastung.

Mit der **ausgeglichen** Energiesparplan von Computern, die höchste Energiezustände (und niedrigste Latenz von Antwort mandantenworkloads) werden nur angewendet, wenn der physische Host relativ ausgelastet ist. Wenn Sie deterministisch und geringer Latenz Antwort Wert für alle Workloads von Mandanten, sollten Sie erwägen, wechseln von der Standardeinstellung **ausgeglichen** Energiesparplan verwenden, die **hohe Leistung** Energiesparplan. Die **hohe Leistung** Energiesparplan von Computern ausgeführt wird die Prozessoren in vollem Tempo jederzeit deaktiviert effektiv bei Bedarf basierenden Wechsel zusammen mit anderen Power Management-Techniken, und Optimieren der Leistung über Energie zu sparen.

Für Kunden, die die kosteneinsparungen durch Reduzierung der Anzahl von physischen Servern damit zufrieden sind, und um sicherzustellen, dass sie die maximale Leistung für ihre virtualisierten Workloads erzielen möchten, sollten Sie verwenden die **hohe Leistung** Energiesparplan von Computern.

Finden Sie weitere Empfehlungen und Einblick in die Nutzung von Energiesparplänen, Ihre Infrastruktur optimieren, [empfohlen ausgeglichen Power planen Sie Parameter für die schnelle Antwortzeiten](../../hardware/power/recommended-balanced-plan-parameters.md)



## <a name="server-core-installation-option"></a>Server Core-Installationsoption

Der Server Core-Installationsoption für Windows Server 2016-Funktion. Server Core bietet eine minimale Umgebung zum Hosten einer ausgewählten Reihe von Serverrollen wie Hyper-V. Es bietet einen geringeren Speicherbedarf der Datenträger für das Hostbetriebssystem, und ein kleiner Angriff und Wartung der Oberfläche. Aus diesem Grund wird dringend empfohlen, Hyper-V-Virtualisierung-Servern die Server Core-Installationsoption verwenden.

Server Core-Installation bietet ein Konsolenfenster nur, wenn der Benutzer angemeldet ist, aber Hyper-V verfügbar, remote-Management-Funktionen macht, einschließlich [Windows Powershell](https://technet.microsoft.com/library/hh848559.aspx) damit Administratoren Remote verwaltet werden können.

## <a name="dedicated-server-role"></a>Dedizierte Serverrolle

Das Stammpartition sollten Hyper-V verwendet werden. Ausführen von zusätzlichen Serverrollen auf einem Server mit Hyper-V kann die Leistung des virtualisierungsservers, beeinträchtigen insbesondere dann, wenn sie erhebliche CPU, Arbeitsspeicher oder e/a-Bandbreite belegen. Minimieren die Serverfunktionen in der Stammpartition bietet weitere Vorteile wie z. B. das Reduzieren der Angriffsfläche.

Systemadministratoren sollten sorgfältig abwägen, welche Software in der rootpartition installiert ist, da es sich bei Software, die gesamtleistung des Servers mit Hyper-V beeinträchtigen kann.

## <a name="guest-operating-systems"></a>Gastbetriebssystem

Hyper-V unterstützt und wurde für eine Reihe von verschiedene Gastbetriebssysteme optimiert. Die Anzahl virtueller Prozessoren, die pro Gastbetriebssystem unterstützt werden, hängt von Gast-Betriebssystems ab. Eine Liste der unterstützten Gastbetriebssysteme, finden Sie unter [Hyper-V: Übersicht](https://technet.microsoft.com/library/hh831531.aspx).

## <a name="cpu-statistics"></a>CPU-Statistiken

Hyper-V veröffentlicht, Leistungsindikatoren, um das Verhalten des virtualisierungsservers charakterisieren und die Ressourcenverwendung gemeldet wird. Der Standardsatz von Tools zum Anzeigen von Leistungsindikatoren in Windows umfasst Performance Monitor und Logman.exe, die anzeigen, und melden Sie sich die Hyper-V-Leistungsindikatoren können. Die Namen der relevanten Zählerobjekte weisen das Präfix **Hyper-V**.

Sie sollten immer die CPU-Auslastung des physischen Systems messen, mithilfe der Hyper-V Hypervisor Logical Processor-Leistungsindikatoren. Die CPU-Auslastung, Leistungsindikatoren, Task-Manager und Performance Monitor-Bericht in den Stamm und untergeordneten Partitionen spiegeln nicht die tatsächliche physische CPU-Auslastung. Verwenden Sie die folgenden Leistungsindikatoren zum Überwachen der Leistung:

- **Hyper-V Hypervisor Logical Processor (\*)\\% Gesamtzeit ausführen** die nicht im Leerlauf befindlichen Gesamtzeit der logischen Prozessoren

- **Hyper-V Hypervisor Logical Processor (\*)\\% Gast-Laufzeit** verbrachte Zeit ausgeführte Zyklen in einem Gast oder innerhalb des Hosts

- **Hyper-V Hypervisor Logical Processor (\*)\\% Hypervisor-Laufzeit** ausgeführt innerhalb der Hypervisor verbrachte Zeit

- **Hyper-V-Hypervisor Stamm virtuellen Prozessor (\*)\\\\** * misst die CPU-Auslastung der Stammpartition

- **Virtueller Hyper-V-Hypervisor-Prozessor (\*)\\\\** * misst die CPU-Auslastung der Gast-Partitionen


## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
