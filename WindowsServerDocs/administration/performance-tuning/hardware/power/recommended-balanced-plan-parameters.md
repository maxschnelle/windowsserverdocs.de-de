---
title: Empfohlene ausgeglichene Energie Sparplan Parameter für schnelle Antwortzeiten
description: Empfohlene ausgeglichene Energie Sparplan Parameter für die schnelle Reaktionszeit
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: qizha;tristanb
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 288746b5361c550e167f64886a929c96c81ff8d0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851963"
---
# <a name="recommended-balanced-power-plan-parameters-for-workloads-requiring-quick-response-times"></a>Empfohlene ausgeglichene Energie Sparplan Parameter für Workloads, die schnelle Antwortzeiten erfordern

Der standardmäßige **ausgeglichene** Energie Sparplan verwendet den **Durchsatz** als Leistungs Metrik für die Optimierung. Während des stabilen Zustands ändert sich der **Durchsatz** nicht mit unterschiedlichen Verwendungs Anforderungen, bis das System vollständig überladen ist (~ 100% Auslastung).  Demzufolge begünstigt der **ausgeglichene** Energie Sparplan die Leistung erheblich, indem die Prozessorfrequenz minimiert und die Auslastung maximiert wird.

Die **Reaktionszeit** kann jedoch exponentiell zunehmen, wenn die Auslastung zunimmt. Heutzutage hat sich die Anforderung der schnellen Reaktionszeit erheblich erhöht. Obwohl Microsoft die Benutzer dazu vorgeschlagen hat, zum **hochleistungsfähigen** Energie Sparplan zu wechseln, wenn er eine schnelle Reaktionszeit benötigt, ist es für einige Benutzer nicht empfehlenswert, den energievorteil bei der leichten bis mittleren Auslastung zu verlieren. Daher bietet Microsoft die folgenden vorgeschlagenen Parameteränderungen für die Arbeits Auslastungen, die eine schnelle Reaktionszeit erfordern.


| Parameter | Beschreibung | Standardwert | Vorgeschlagene Werte |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Schwellenwert für die Prozessorleistung erhöhen | Schwellenwert für die Auslastung oberhalb der Häufigkeit | 90 | 60 |
| Schwellenwert für die Prozessorleistung verringern | Schwellenwert für die Auslastung, unter dem die Häufigkeit verringert werden soll | 80 | 40 |
| Zeit zur Steigerung der Prozessorleistung | Anzahl von ppm-Check Fenstern, bevor die Häufigkeit erhöht wird | 3 | 1 |
| Richtlinie zur Erhöhung der Prozessorleistung | Wie schnell die Häufigkeit erhöht werden muss | Single | Ideal |

Um die vorgeschlagenen Werte festzulegen, können die Benutzer die folgenden Befehle in einem Fenster mit Administratorrechten ausführen:

``` syntax
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCTHRESHOLD 60
Powercfg -setacvalueindex scheme_balanced sub_processor PERFDECTHRESHOLD 40
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCTIME 1
Powercfg -setacvalueindex scheme_balanced sub_processor PERFINCPOL 0
Powercfg -setactive scheme_balanced
```

Diese Änderung basiert auf der Leistungs-und Leistungsanalyse Analyse mithilfe der folgenden Arbeits Auslastungen. Informationen zu den Benutzern, die die Energieeffizienz mit bestimmten SLA-Anforderungen optimieren möchten, finden Sie unter [Überlegungen zur Server Hardware Leistung](../power.md).

>[!Note]
> Weitere Empfehlungen und Einblicke in die Nutzung von Energie Sparplänen zum Optimieren virtualisierter Workloads finden Sie unter [Hyper-v-Konfiguration](../../role/hyper-v-server/configuration.md) .

## <a name="specpower--java-workload"></a>Specpower – Java-Arbeitsauslastung

[Specpower\_ssj2008](http://spec.org/power_ssj2008/), der beliebteste Industriestandard-Spezifikations Benchmark für Serverleistung und Leistungsmerkmale, wird verwendet, um die Auswirkungen auf die Leistung zu überprüfen. Da es nur einen **Durchsatz** als Leistungs Metrik verwendet, bietet der standardmäßige **ausgeglichene** Energie Sparplan die beste Energieeffizienz.

Die vorgeschlagene Parameter Änderung verbraucht etwas höhere Stromversorgung (d. h. < = 20%). Lade Ebenen. Mit der höheren Auslastung erhöht sich der Unterschied, und es wird damit begonnen, die gleiche Leistung wie der **High Performance** -Energie Sparplan nach der Auslastung von 60% zu verbrauchen. Um die vorgeschlagenen Änderungs Parameter zu verwenden, sollten die Benutzer während der Planung der Gestell-Kapazität die Stromkosten bei mittelgroßen bis hohen Lade Graden berücksichtigen.

## <a name="geekbench-3"></a>Geekbench 3

[Geekbench 3](http://www.geekbench.com/geekbench3/) ist ein plattformübergreifender Prozessor-Benchmark, der die Ergebnisse für die Einzel-und multikernleistung trennt. Es simuliert eine Reihe von Arbeits Auslastungen, z. b. ganzzahlige Workloads (Verschlüsselungen, Komprimierungen, Bildverarbeitung usw.), Gleit Komma-Arbeits Auslastungen (Modellierung, Dezimalstelle, Bildschärfung, Bildunschärfe usw.) und arbeitsspeicherworkloads (Streaming).

Die **Antwortzeit** ist ein wichtiges Measure in der Ergebnisberechnung. In unserem getesteten System hat der standardmäßige **ausgeglichene** Energie Sparplan eine Regression von ungefähr 18% in einzelkerntests und eine Regression von ungefähr 40% bei mehr Kern Tests im Vergleich zum **Hochleistungs** Energie Sparplan. Durch die vorgeschlagene Änderung werden diese Regressionen entfernt.

## <a name="diskspd"></a>DiskSpd

[Diskspd](https://en.wikipedia.org/wiki/Diskspd) ist ein Befehlszeilen Tool für Speicher Benchmarktests, das von Microsoft entwickelt wurde. Es wird häufig verwendet, um eine Vielzahl von Anforderungen für Speichersysteme für die Speicher Leistungsanalyse zu generieren.

Wir haben einen [Failovercluster] eingerichtet und mithilfe von diskspd zufällige und sequenzielle Generierung erstellt und IOS in den lokalen und Remote-Speichersystemen mit unterschiedlichen e/a-Größen gelesen und geschrieben. Unsere Tests zeigen, dass die e/a-Antwortzeit für die Prozessor Häufigkeit unter verschiedenen Energie Sparplänen sehr empfindlich ist. Der **ausgeglichene** Energie Sparplan könnte die Antwortzeit des **hochleistungsfähigen** Energie Sparplans unter bestimmten Workloads verdoppeln. Die vorgeschlagene Änderung entfernt die meisten Regressionen.

>[!Important]
>Ab Intel [Broadwell]-Prozessoren, die Windows Server 2016 ausführen, werden die meisten Verwaltungsentscheidungen für die Prozessorleistung im Prozessor statt auf der Betriebssystemebene vorgenommen, um eine schnellere Anpassung an die Änderungen an der Arbeitsauslastung zu erzielen. Die vom Betriebssystem verwendeten älteren ppm-Parameter wirken sich nur minimal auf die tatsächlichen Häufigkeits Entscheidungen aus, mit dem Unterschied, dass der Prozessor eine Stromversorgung oder Leistungsfähigkeit bevorzugen oder die minimalen und maximalen Frequenzen umrechnen muss. Daher ist die vorgeschlagene Änderung von ppm-Parametern nur für die Pre-Broadwell-Systeme ausgelegt.

## <a name="see-also"></a>Weitere Informationen
- [Überlegungen zur Server Hardware Leistung](../index.md)
- [Server Hardware Power Considerations](../power.md) (Überlegungen zum Energiebedarf von Serverhardware)
- [Power and Performance Tuning](power-performance-tuning.md) (Leistungs- und Energieoptimierung)
- [Processor Power Management (PPM) Tuning for the Windows Server Balanced Power Plan](processor-power-management-tuning.md) (Optimieren der Prozessorenergieverwaltung (Processor Power Management (PPM)) für den ausgewogenen Energiesparplan von Windows Server)
- [Failovercluster](https://technet.microsoft.com/library/cc725923.aspx)
