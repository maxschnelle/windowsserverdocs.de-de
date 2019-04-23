---
title: Ausgeglichene Power-Plan-Parameter empfohlen für die schnelle Antwortzeiten
description: Ausgeglichene Power-Plan-Parameter empfohlen für die schnelle Antwortzeit
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Qizha;TristanB
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 134e868e1400729f754039fc8120cea0c73945bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878791"
---
# <a name="recommended-balanced-power-plan-parameters-for-workloads-requiring-quick-response-times"></a>Für Workloads empfohlen mit Lastenausgleich Power-Plan-Parameter erfordern schnelle Antwortzeiten

Der Standardwert **ausgeglichen** power Plans verwendet **Durchsatz** als die Leistungsmetrik für die Optimierung. Während der stabilen Zustand **Durchsatz** ändert sich nicht mit unterschiedlichen von Nutzungsdaten bis das System vollständig überladene (~ Auslastung von 100 %) ist.  Daher die **ausgeglichen** Energiesparplan begünstigt Leistung sehr viel mit der Prozessorfrequenz minimieren und Maximieren der Nutzung.

Jedoch **Antwortzeit** konnte mit Auslastung steigt exponentiell steigen. Heutzutage ist die Anforderung der schnelle Antwortzeit deutlich gestiegen. Obwohl Microsoft die Benutzern, wechseln zu vorgeschlagenen der **High Performance** Energiesparplan von Computern bei Bedarf schnell Antwortzeit, einige Benutzer möchten nicht den Vorteil, dass Power während Licht auf mittlerer Last Ebenen zu verlieren. Daher stellt Microsoft die folgenden empfohlenen Parameternamen Änderungen für die arbeitsauslastungen, die schnelle Antwortzeit erfordern.


| Parameter | Beschreibung | Standardwert | Vorgeschlagener Wert |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Prozessor-Leistungsschwellenwert erhöhen | Verwendungsschwellenwert oben wird die Häufigkeit erhöhen | 90 | 60 |
| Prozessor-Leistungsschwellenwert verringern | Verwendungsschwellenwert unten wird die Häufigkeit zu verringern | 80 | 40 |
| Erhöhen der Leistung Prozessorzeit | Anzahl von Seiten pro Minute überprüfen, bevor die Häufigkeit ist, erhöhen | 3 | 1 |
| Prozessor-Leistungsrichtlinie erhöhen | Wie schnell kann die Häufigkeit erhöhen | einzelne | Ideal |

Um die vorgeschlagenen Werte festzulegen, können die Benutzer mit Administrator die folgenden Befehle in einem Fenster ausführen:

``` syntax
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCTHRESHOLD 60
Powercfg -setacvalueindex scheme_balanced sub_processor PERFDECTHRESHOLD 40
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCTIME 1
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCPOL 0
Powercfg -setactive scheme_balanced
```

Diese Änderung basiert auf die Leistung und die Analyse der Stromversorgung Kompromiss verwenden die folgenden Workloads. Optimieren der Benutzer, denen weiter genau die Energieeffizienz mit bestimmten SLA-Anforderungen finden Sie in [Überlegungen zur Leistung von Server-Hardware](../power.md).

>[!Note]
> Finden Sie weitere Empfehlungen und Einblick in die Nutzung von Energiesparplänen, virtualisierte arbeitsauslastungen zu optimieren, [Hyper-V-Konfiguration](../../role/hyper-v-server/configuration.md)

## <a name="specpower--java-workload"></a>SPECpower – JAVA-workload

[SPECpower\_ssj2008](http://spec.org/power_ssj2008/), wird die beliebte Industriestandard-SPEC-Benchmark für Servereigenschaften Leistungsfähigkeit, wird verwendet, um überprüfen Sie die Auswirkungen des Power. Da es nur verwendet **Durchsatz** als Leistungsmetrik, die Standardeinstellung **ausgeglichen** Energiesparplan von Computern bietet den besten Energieeffizienz.

Die vorgeschlagene parameteränderung leicht höhere Leistung auf das Licht verbraucht (d. h. < = 20 %) Laden Sie die Ebenen. Aber mit der höheren Ebene der Unterschied steigt geladen, und Nutzen der gleichen Leistungsstärke wie beginnt der **hohe Leistung** Energiesparplan von Computern nach der 60 % Load-Ebene. Um die vorgeschlagene Änderung-Parameter verwenden, sollten die Benutzer bei der kapazitätsplanung ihre Rack Beachten der Stromkosten in mittleren bis hohen Auslastungsgrad sein.

## <a name="geekbench-3"></a>GeekBench 3

[GeekBench 3](http://www.geekbench.com/geekbench3/) ist eine plattformübergreifende-Prozessor-Benchmark, die die Ergebnisse für die Leistung von Einzelkern- und mit mehreren Kernen trennt. Es wird eine Reihe von Workloads, einschließlich Integer-Workloads (Verschlüsselungen, kompatibel, das eine bildverarbeitung, usw.), floating Point-Workloads (Modellierung, Fraktal, Schärfe Image, Abbild Unschärfe, usw.) und Memory-Workloads (streaming) simuliert.

**Antwortzeit** ist eine wichtige Kennzahl in seiner bewertungsberechnung. In unserem getesteten System, der Standardwert **ausgeglichen** Energiesparplan hat ca. 18 % Regression Einzelkern-Tests und etwa 40 % der Regression mit mehreren Kernen-Tests, die im Vergleich zu den **hohe Leistung** Energiesparplan. Die vorgeschlagene Änderung entfernt diese Regressionen.

## <a name="diskspd"></a>DiskSpd

[Diskspd](https://en.wikipedia.org/wiki/Diskspd) ist ein Befehlszeilentool, bei Vergleichstests Speicher, die von Microsoft entwickelt wurden. Es wird häufig verwendet, um eine Vielzahl von Anforderungen von Speichersystemen für die Leistungsanalyse für Speicher zu generieren.

Wir richten Sie einen [Failovercluster] und Diskspd zum Generieren von zufälligen und sequenzielle und read und Schreibvorgänge, die auf die lokalen und Remotespeicher-Systeme in unterschiedlichen e/a-Größen verwendet. Unsere Tests haben gezeigt, dass die e/a-Antwortzeit unter unterschiedliche Energiesparpläne sehr empfindlich, was Prozessorfrequenz befindet. Die **ausgeglichen** Energiesparplan konnte double die Antwortzeit, die von der **hohe Leistung** Energiesparplan von Computern unter bestimmten Arbeitsbedingungen. Die vorgeschlagene Änderung entfernt die meisten Regressionen.

>[!Important]
>[Broadwell]-Intel-Prozessoren, die unter Windows Server 2016 ab, die meisten der Processor Power managemententscheidungen im Prozessor anstelle von OS-Ebene erfolgen schneller macht eine Anpassung, um die Änderungen der arbeitsauslastung zu erreichen. Die ältere PPM-Parameter, die vom Betriebssystem verwendet eine minimale Auswirkung auf die tatsächliche Häufigkeit Entscheidungen treffen – mit Ausnahme dem Prozessor mitgeteilt wird, ob es Leistung oder Energieverbrauch bewährten vorziehen sollen oder Taskausführungsanforderungen begrenzt wird, die minimalen und maximalen Häufigkeit an. Daher ist die vorgeschlagene Änderung der PPM-Parameter nur für die Pre-Broadwell-Systeme als Ziel.

## <a name="see-also"></a>Siehe auch
- [Überlegungen zur Leistung von Server-Hardware](../index.md)
- [Überlegungen zur Power von Server-Hardware](../power.md)
- [Leistung und Leistungsoptimierung](power-performance-tuning.md)
- [Processor Power Management-Optimierung](processor-power-management-tuning.md)
- [Failovercluster](https://technet.microsoft.com/library/cc725923.aspx)
