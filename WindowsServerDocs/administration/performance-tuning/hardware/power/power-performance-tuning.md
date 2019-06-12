---
title: Leistungsfähigkeit Optimierung
description: Optimierung der Energiesparplan von Windows Server mit Lastenausgleich für die Energieverwaltung (PPM)
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Qizha;TristanB
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 4ad58e9b477f61844dedd9f6638efb12f1a96500
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811565"
---
# <a name="power-and-performance-tuning"></a>Leistung und leistungsoptimierung

Energieeffizienz wird immer wichtiger, in der Enterprise und Data Center-Umgebung, und die Kombination von Optionen für die Konfiguration einen anderen Satz von Kompromisse hinzugefügt.

Windows Server 2016 wird für eine Vielzahl von kundenworkloads für ausgezeichnete Energieeffizienz mit Auswirkungen auf die minimale Leistung optimiert. [Processor Power Management (PPM)-Optimierung für die Windows Server mit Lastenausgleich – Energiesparplanüberwachung](processor-power-management-tuning.md) beschreibt die Workloads für die Optimierung die Standardparameter in Windows Server 2016 und Vorschläge zur benutzerdefinierten Feinabstimmungen.

Dieser Abschnitt befasst sich mit Energieeffizienz vor-und Nachteile können Sie fundierte Entscheidungen zu treffen, wenn Sie die Standard-Power-Einstellungen auf Ihrem Server anpassen müssen. Die Mehrzahl der Serverhardware und Workloads sollte jedoch keine Administrator Power Optimierung, bei der Ausführung von Windows Server 2016 erfordern.

## <a name="calculating-server-energy-efficiency"></a>Berechnen der Energieeffizienz von server

Wenn Sie Ihren Server für die energieeinsparung optimieren, müssen Sie auch die Leistung berücksichtigen. Optimieren von wirkt sich auf Leistung und Energie, manchmal in unverhältnismäßig große Mengen. Sollten Sie für jede mögliche Anpassung Ihre Power Budget und die Leistung der Ziele zu bestimmen, ob der Kompromiss akzeptabel ist.

Sie können Ihres Servers Energie Effizienz Verhältnis für eine wichtige Messgröße berechnen, die Leistungsfähigkeit Informationen enthält. Energieeffizienz ist das Verhältnis von Arbeit, die für die durchschnittliche Leistung ausgeführt wird, die bei einem angegebenen Zeitraum benötigt wird.

![Energie Effizienz Formel](../../media/perftune-guide-power-formula.png)

Mit dieser Metrik können Sie praktische Ziele festgelegt haben, die den Kompromiss zwischen Leistung und die Leistung berücksichtigen. Im Gegensatz dazu kann ein Ziel von 10 % energieeinsparungen im Rechenzentrum nicht die entsprechenden Auswirkungen auf die Leistung und umgekehrt zu erfassen.

Auf ähnliche Weise, wenn Sie den Server, um die Leistung von 5 Prozent, und dies führt zu höheren Energieverbrauch von 10 Prozent zu steigern optimieren, das gesamte Ergebnis möglicherweise oder ist möglicherweise nicht für Ihre Geschäftsziele akzeptabel. Die Metrik der Energie Effizienz ermöglicht als Leistung oder Energieverbrauch Metriken allein informiertere Entscheidungen treffen zu können.

## <a name="measuring-system-energy-consumption"></a>Messen von Energieverbrauch system

Sie sollten einen Vergleichswert für die Power einrichten, bevor Sie Ihren Server für die Steigerung der Energieeffizienz optimieren.

Wenn Ihr Server die erforderliche Unterstützung hat, können Sie die Leistungsfähigkeit, Messung und Funktionen in Windows Server 2016 Budgetierung, auf Systemebene Energieverbrauch anzeigen, indem Sie mit dem Systemmonitor.

Eine Möglichkeit, um festzustellen, ob Ihr Server verfügt über Unterstützung für die Messung und die Budgetierung zur Überprüfung wird der [Windows Server-Katalog](http://www.windowsservercatalog.com). Wenn Ihr Servermodell für die neue Qualifikation der Enhanced Power Management in der Windows-Hardware Certification-Programm qualifiziert werden, ist es garantiert die softwaremessung und budgetbezogene Aspekte Funktionen zu unterstützen.

Eine weitere Möglichkeit zum Prüfen der Messung unterstützt wird, manuell für die Leistungsindikatoren im Systemmonitor zu suchen. Systemmonitor zu öffnen, wählen Sie **Leistungsindikatoren hinzufügen**, und suchen Sie dann die **Energiemessgerät** Indikatorengruppe.

Wenn benannte Instanzen von energiemessgeräten angezeigt, in das Feld mit der Bezeichnung **Instanzen für ausgewähltes Objekt**, Ihre Plattform unterstützt, die softwaremessung. Die **Power** Indikator, Strom in Watt anzeigt, wird, in der ausgewählten Leistungsindikator-Gruppe. Die genaue Ableitung des Datenwerts Power ist nicht angegeben. Es kann z. B. eine sofortige Leistungsaufnahme oder ein Draw Durchschnittswerten über einige Zeitraum sein.

Wenn Ihre Serverplattform Messung nicht unterstützt wird, können Sie ein physisches softwaremessungs-Gerät mit der Stromversorgung Eingabe verbunden sind, zum Stromverbrauch zeichnen- oder Energieverbrauch des Systems messen.

Um eine Basislinie zu erstellen, sollten Sie den verschiedenen Zeitpunkten System laden, aus dem Leerlauf auf 100 % (maximaler Durchsatz) zum Generieren einer Zeile laden erforderlichen Durchschnittswerten messen. Die folgende Abbildung zeigt drei Beispielkonfigurationen Zeilen laden:

![Laden von Beispielzeilen](../../media/perftune-guide-sample-loadlines.png)

Sie können Load Zeilen zu bewerten und vergleichen die Leistung und Energieverbrauch von Konfigurationen laden alle Punkte. In diesem speziellen Beispiel ist es leicht zu erkennen, was die beste Konfiguration ist. Jedoch möglich gibt es problemlos, in denen eine Konfiguration funktioniert am besten für hohe Workloads und eine funktioniert am besten für kleine Workloads.

Sie müssen die Anforderungen für die Workload auf eine optimale Konfiguration gründlich zu verstehen. Denken Sie nicht, dass wenn Sie eine gute Konfiguration gefunden, es immer eine optimale bleibt. Sie sollten die Auslastung und Energieverbrauch des Systems in regelmäßigen Abständen und nach dem Ändern von arbeitsauslastungen, arbeitsauslastungsstufen oder Serverhardware messen.

## <a name="diagnosing-energy-efficiency-issues"></a>Diagnostizieren von Problemen der Energie-Effizienz

**PowerCfg.exe** unterstützt eine Befehlszeilenoption, die Sie verwenden können, um die im Leerlauf Energieeffizienz des Servers zu analysieren. Beim Ausführen von PowerCfg.exe mit dem **/energy** -Option, das Tool führt einen Test 60 Sekunden, um Probleme mit der Effizienz von möglichen energieeinsparungen zu erkennen. Das Tool generiert einen einfachen HTML-Bericht im aktuellen Verzeichnis.

> [!Important]
> Um eine präzise Analyse zu gewährleisten, stellen Sie sicher, dass alle lokalen apps geschlossen werden, vor dem Ausführen **PowerCfg.exe**. 

Timer Tick abgerechnet, Treiber, die fehlende Unterstützung für die energieverwaltung und übermäßiger CPU-Auslastung der verhaltensbasierten Probleme sind, die vom erkannt werden verkürzt die **Powercfg /energy** Befehl. Dieses Tool bietet eine einfache Möglichkeit zum Identifizieren und beheben Sie Probleme Power, was ggf. zu erheblichen kosteneinsparungen in einem großen Rechenzentrum.

Weitere Informationen zu PowerCfg.exe, finden Sie unter [mithilfe von PowerCfg zum Bewerten der Energieeffizienz](https://msdn.microsoft.com/windows/hardware/gg463250.aspx).

## <a name="using-power-plans-in-windows-server"></a>Verwenden Energiesparpläne in Windows Server

Windows Server 2016 verfügt über drei integrierte Energiesparpläne, die unterschiedliche geschäftsanforderungen zu erfüllen. Diese Pläne bieten eine einfache Möglichkeit, einen Server anzupassen, Leistung oder Energieverbrauch Ziele zu erreichen. In der folgende Tabelle wird beschrieben, die Pläne, enthält die allgemeinen Szenarien, in denen Sie jeden Plan zu verwenden und bietet einige Implementierungsdetails für jeden Plan.

| **Planen** | **Beschreibung** | **Allgemeine anwendbare Szenarios** | **Implementierungshighlights** |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Mit Lastenausgleich (empfohlen) | Die Standardeinstellung. Ziele gute Energieeffizienz bei minimalen Leistungseinbußen. | Allgemeine computing | Entspricht die Kapazität auf den Bedarf an. Energie sparen Features abwägen Leistungsfähigkeit. |
| Hohe Leistung | Erhöht die Leistung auf Kosten der hohen Energieverbrauch. Power temperaturüberwachung, Betrieb, Ausgaben und Zuverlässigkeit Überlegungen gelten. | Mit geringer Latenz-apps und app-Code, die anfällig für den Prozessor leistungsänderungen | Prozessoren sind immer mit dem höchsten Leistungszustand (einschließlich "Turbo" Frequenzen) beschränkt. Es werden alle Kerne unparked. Temperaturüberwachung Ausgabe kann erheblich sein. |
| Energiesparmodus | Schränkt die Leistung, Energie gespart, und Reduzieren der Betriebskosten. Nicht empfohlen wird, ohne gründliche Tests stellen Sie sicher, dass Leistung geeignet ist. | Bereitstellungen mit begrenzten Power Budgets und temperaturüberwachung Einschränkungen | Initialen der Prozessorfrequenz auf einen Prozentsatz der Höchstwert (sofern unterstützt) und andere Funktionen energiesparende ermöglicht. |


Von diesen Energiesparplänen in Windows für Wechselstrom (AC) vorhanden sein und (Gleichstrom) unterstützt Systeme, jedoch wird davon ausgegangen, dass der Server immer eine Stromquelle an verwenden.

Weitere Informationen zur Energiesparpläne "und" Power-Konfigurationen für Gruppenrichtlinien, finden Sie unter [Energierichtlinienkonfiguration und Bereitstellung in Windows](https://msdn.microsoft.com/windows/hardware/gg463243.aspx).

> [!Note]
> Einige Herstellern Server haben ihre eigenen Energieverwaltungsoptionen über die BIOS-Einstellungen zur Verfügung. Wenn das Betriebssystem keine Kontrolle über die energieverwaltung, wirkt ändern die Energiesparpläne in Windows Stromnetz und Leistung sich nicht.

## <a name="tuning-processor-power-management-parameters"></a>Processor Power Management Optimierungsparameter

Jedes Energiesparplans stellt eine Kombination aus zahlreichen zugrunde liegenden Power Management-Parameter dar. Die integrierten sind drei Auflistungen von empfohlenen Einstellungen, die eine Vielzahl von Workloads und Szenarien abdecken. Es erkennt jedoch, dass diese Pläne nicht jede kundenanforderungen erfüllt.

Den folgenden Abschnitten werden die Möglichkeiten zum Optimieren von einige bestimmten Prozessor Power Management-Parameter, um die drei integrierten Pläne nicht Gegenstand Ziele zu erreichen. Wenn Sie ein größeres Array an die Power-Parameter kennen müssen, finden Sie unter [Energierichtlinienkonfiguration und Bereitstellung in Windows](https://msdn.microsoft.com/windows/hardware/gg463243.aspx).

## <a name="processor-performance-boost-mode"></a>Prozessor-Leistungsmodus boost

Intel Turbo Boost und Turbo-CORE AMD-Technologien sind Funktionen, mit denen Prozessoren, um zusätzliche Leistung zu erzielen, wenn es am sinnvollsten ist (d. h. unter hoher lädt). Dieses Feature erhöht jedoch Energieverbrauch für CPU-Core, damit Windows Server 2016 konfiguriert Turbo-Technologien, die basierend auf der Power-Richtlinie, die in Verwendung und die Implementierung von bestimmten Prozessor ist.

Turbo für hohe Leistung Energiesparpläne auf allen Intel- und AMD-Prozessoren aktiviert ist, und für den Energiesparmodus Energiesparpläne deaktiviert. Für ausgewogene Energiesparpläne auf Systemen, die auf herkömmlichen P-Status-basierte Häufigkeit Management basieren, ist Turbo standardmäßig aktiviert, nur dann, wenn die Plattform das Register EPB unterstützt.

> [!Note]
> Das EPB Register ist nur in Intel Westmere und höher Prozessoren unterstützt.

Für Nehalem von Intel und AMD-Prozessoren ist Turbo auf P-Status-basierten Plattformen standardmäßig deaktiviert. Aber wenn ein System Zusammenarbeit Prozessor Leistung Control (CPPC), einen neuen alternativen Modus Leistung-Kommunikation zwischen dem Betriebssystem und die Hardware unterstützt (definiert in ACPI 5.0) handelt, Turbo kann möglicherweise belegt sein wenn die Windows-Betriebssystem System fordert dynamisch an die Hardware die höchste Leistung zu liefern.

Zum Aktivieren oder Deaktivieren der Turbo Boost-Funktion, muss der Prozessor Leistung Boost-Mode-Parameter durch den Administrator oder durch die Standardeinstellungen für die Parameter für den ausgewählten Energiesparplan konfiguriert werden. Prozessor Boost Leistungsmodus enthält fünf zulässige Werte aus, wie in Tabelle 5 dargestellt.

Die Optionen für P-Status-basierte-Steuerelement sind deaktiviert, aktiviert (Turbo ist die Hardware zur Verfügung, wenn geringe Leistung angefordert wird), und effiziente (Turbo ist nur verfügbar, wenn das Register EPB implementiert wird).

Für CPPC basierenden Steuerelements, die Optionen deaktiviert sind, effizient aktiviert (Windows gibt die genaue Menge der Turbo bereitstellen), und aggressives (Windows fordert, "Höchstleistung" Turbo aktivieren).

In Windows Server 2016 ist der Standardwert für den Boost-Modus 3.

| **Name** | **P-Status-basierte Verhalten** | **CPPC-Verhalten** |
|--------------------------|------------------------|-------------------|
| 0 (deaktiviert) | Disabled | Disabled |
| 1 (aktiviert) | Enabled | Effiziente aktiviert |
| 2 (aggressives) | Enabled | Aggressive |
| 3 (effiziente aktiviert) | Effizienz | Effiziente aktiviert |
| 4 (effiziente Aggressive) | Effizienz | Aggressive |

 
Die folgenden Befehle Prozessor Leistung Boost-Modus auf der aktuelle Energiesparplan aktivieren (die Richtlinie mit einem GUID-Alias angeben):

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor PERFBOOSTMODE 1
Powercfg -setactive scheme_current
```

> [!Important]
> Führen Sie die **Powercfg - Setactive** Befehl aus, um die neuen Einstellungen zu aktivieren. Sie müssen nicht den Server neu starten.

Zum Festlegen dieses Werts für Energiesparpläne als den derzeit ausgewählten Plan können Sie Aliase wie z. B. Schema\_MAX (Energiesparmodus), SCHEME\_MIN (hohe Leistungsfähigkeit), und das Schema\_AUSGEGLICHEN (ausgeglichen) anstelle von Schema\_Aktuelle. Ersetzen Sie "Schema aktuellen" in den Befehlen der Powercfg - Setactive zuvor gezeigten mit den gewünschten Alias, Energiesparplan von Computern zu aktivieren.

Beispielsweise ist zum Anpassen der Boost-Modus in den Energiesparplan, und stellen diese Energiesparmodus den aktuellen Plan können die folgenden Befehle ausführen:

``` syntax
Powercfg -setacvalueindex scheme_max sub_processor PERFBOOSTMODE 1
Powercfg -setactive scheme_max
```

## <a name="minimum-and-maximum-processor-performance-state"></a>Minimale und maximale Leistung Prozessorzustand

Prozessoren zwischen leistungszustände (P-Zustände) sehr schnell ändern Übereinstimmung Supply gefordert wird, liefert der Leistung bei Bedarf und nach Möglichkeit um Energie zu sparen. Wenn Ihr Server bestimmte Anforderungen für hohe Leistung oder Energieverbrauch mindestens hat, sollten Sie erwägen, konfigurieren die **mindestens Prozessor Leistungsstatus** Parameter oder die **maximale Prozessorleistung Status** Parameter.

Die Werte für die **mindestens Prozessor Leistungsstatus** und **maximale Leistung Prozessorzustand** Parameter werden als Prozentsatz des maximal Häufigkeit, mit dem Wert im Bereich 0 – ausgedrückt. 100.

Wenn der Server mit extrem geringer Latenz, invarianten CPU-Frequenz (z. B. für testwiederholungen) oder die höchsten Leistungsstufen erfordert, sollten Sie nicht die Prozessoren, die auf niedrigeren Leistung wechseln. Sie können für einen Server des Leistungsstatus der Mindestanforderungen zu 100 Prozent begrenzen, mithilfe der folgenden Befehle:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor PROCTHROTTLEMIN 100
Powercfg -setactive scheme_current
```

Wenn Ihr Server niedrigeren Stromverbrauch erfordert, empfiehlt es sich um den Prozessorzustand der Leistung auf einen Prozentsatz der maximale Obergrenze. Sie können z. B. den Prozessor auf 75 Prozent der die maximale Häufigkeit einschränken, indem Sie mit den folgenden Befehlen wird:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor PROCTHROTTLEMAX 75
Powercfg -setactive scheme_current
```

> [!Note]
> Taskausführungsanforderungen begrenzt wird, prozessorbezogene Leistungsdaten auf einen Prozentsatz der Höchstwert muss Prozessor unterstützt werden. Überprüfen Sie die Prozessor-Dokumentation, um zu bestimmen, ob diese Unterstützung vorhanden ist, oder zeigen Sie den Leistungsindikator des Systemmonitors **% der maximalen Frequenz** in die **Prozessor** Gruppe, um festzustellen, ob alle Häufigkeit Caps wurden angewendet.

## <a name="processor-performance-increase-and-decrease-of-thresholds-and-policies"></a>Prozessor-Leistungssteigerung und Verringerung von Schwellenwerten und Richtlinien

Die Geschwindigkeit an, an der einen Prozessor Leistungsstatus erhöht oder verringert, wird durch mehrere Parameter gesteuert. Die folgenden vier Parameter haben die offensichtlichsten Auswirkungen:

-   **Prozessor-Leistungsschwellenwert erhöhen** definiert den Wert für die Auslastung oben wodurch Leistungsstatus des Prozessors erhöht wird. Größere Werte langsam verlängert, die für den Leistungsstatus als Reaktion auf höhere Aktivitäten.

-   **Prozessor-Leistungsschwellenwert verringern** definiert der Wert für die Auslastung unten die Leistungsstatus des Prozessors verringert wird. Größere Werte vergrößern die Rate der Verringerung der für den Leistungsstatus während der Leerlaufzeiten.

-   **Prozessor-Leistungsrichtlinie erhöhen und Prozessor zu Leistungseinbußen führen** Richtlinie zu bestimmen, welche Leistungsstatus festgelegt werden soll, wenn eine Änderung erfolgt. Richtlinie für "Einfach" bedeutet, dass es sich bei wählt den nächsten Zustand. "Rocket" bedeutet, dass maximale oder minimale Zustand die Leistung. "Ideale" versucht, ein Gleichgewicht zwischen Leistung und die Leistung zu finden.

Wenn der Server mit extrem geringer Latenz erfordert, während Sie weiterhin mit niedriger Leistung während der Leerlaufzeiten profitieren möchten, können Sie z. B. beschleunigen die Leistungssteigerung der Status für alle Anstieg der Last und die Verringerung der verlangsamen, Last ausfällt. Die folgenden Befehle die Erhöhung Richtlinie so festlegen "Rocket" für eine schnellere Erhöhung des Status, und legen Sie die Verringerung der Richtlinie auf "Single". Die Erhöhung und Verringerung Schwellenwerte werden auf 10 und 8 festgelegt.

``` syntax
Powercfg.exe -setacvalueindex scheme_current sub_processor PERFINCPOL 2
Powercfg.exe -setacvalueindex scheme_current sub_processor PERFDECPOL 1
Powercfg.exe -setacvalueindex scheme_current sub_processor PERFINCTHRESHOLD 10
Powercfg.exe -setacvalueindex scheme_current sub_processor PERFDECTHRESHOLD 8
Powercfg.exe /setactive scheme_current
```

## <a name="processor-performance-core-parking-maximum-and-minimum-cores"></a>Parken von Kernen für maximale und minimale Leistung Prozessorkern

Parken von Kernen ist ein Feature, das in Windows Server 2008 R2 eingeführt wurde. Die Processor Power Management (PPM)-Engine und der Scheduler arbeiten zusammen, um dynamisch anpassen, die Anzahl von Kernen, die Ausführung von Threads verfügbar sind. Die PPM-Engine wählt eine Mindestanzahl von Kernen für die Threads, die geplant werden.

Kerne, die in der Regel geparkt sind keine Threads geplant, und sie werden in sehr geringem Energieverbrauch gelöscht, wenn sie Unterbrechungen, DPCs oder andere streng kategorisierter Arbeit nicht verarbeitet werden. Verbleibende Kerne sind verantwortlich für den Rest der Workload. Parken von Kernen kann potenziell Energieeffizienz bei niedriger Auslastung erhöhen.

Für die meisten Server bietet standardmäßig Parken von Kernen – ein vernünftiges Gleichgewicht von Durchsatz und Energieeffizienz. Auf die Prozessoren, in denen Parken von Kernen nicht so viele Vorteile für generische Workloads angezeigt werden kann, kann es standardmäßig deaktiviert werden.

Wenn Ihr Server bestimmte Anforderungen für die kernparkens hat, können Sie steuern die Anzahl von Kernen, die mithilfe von Parken zur Verfügung stehen die **Leistung Core Parking maximale Prozessorkerne** Parameter oder die **Prozessor Leistung Core Parking Mindestanzahl von Kernen** Parameter in Windows Server 2016.

Ein Szenario, das Parken von Kernen nicht immer optimal für die ist, wenn eine oder mehrere aktive Threads zugeordnet, eine nicht triviale Teilmenge der CPUs in einem NUMA-Knoten vorhanden sind (d. h. mehr als 1 CPU, aber kleiner als der gesamte Satz von CPUs auf dem Knoten). Wenn der Parkmöglichkeiten Kernalgorithmus Kerne unpark übernommen werden (sofern eine Zunahme der Workload Intensität auftritt), möglicherweise nicht immer die Kerne im aktiven kategorisierter Teilmenge (oder Teilmengen) zu unpark ausgewählt und daher möglicherweise am Ende unparking Kerne, die nicht tatsächlich verwendet.

Die Werte für diese Parameter sind Prozentsätze im Bereich von 0 bis 100. Die **Leistung Core Parking maximale Prozessorkerne** Parameter legt den maximalen Prozentsatz der Kerne, die (Ausführung von Threads verfügbar) unparked können zu jedem Zeitpunkt während der **Prozessor Leistung Parken Mindestanzahl von Kernen** Parameter steuert den Mindestprozentsatz von Kernen, die unparked sein können. Um die Parken von Kernen zu deaktivieren, setzen die **Leistung Core Parking mindestens Prozessorkerne** Parameter, um 100 Prozent mit den folgenden Befehlen:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor CPMINCORES 100
Powercfg -setactive scheme_current
```

Um die Anzahl der planbare Kerne auf 50 Prozent der die maximale Anzahl zu reduzieren, legen Sie die **Leistung Core Parking maximale Prozessorkerne** -Parameter auf 50 wie folgt:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor CPMAXCORES 50
Powercfg -setactive scheme_current
```

## <a name="processor-performance-core-parking-utility-distribution"></a>Prozessorkern-Leistung "Parken" Hilfsprogramm-Verteilung

Hilfsprogramm-Verteilung ist eine algorithmische Optimierung in Windows Server 2016, die zur Verbesserung der Energieeffizienz bei einigen Workloads entwickelt wurde. Es verfolgt nicht verschiebbare CPU-Aktivität (d. h. DPCs, Unterbrechungen oder streng kategorisierter Threads), und es prognostiziert zukünftige Aufgaben auf jedem Prozessor basierend auf der Annahme, dass bewegliche Arbeit gleichmäßig auf alle unparked Kerne verteilt werden kann.

Hilfsprogramm-Verteilung ist standardmäßig für die ausgewogene Energiesparplan von Computern einige Prozessoren aktiviert. Sie können die prozessorenergieverbrauch reduzieren, durch die Senkung der angeforderten CPU-Frequenzen von Workloads, die in einem relativ stabilen Zustand sind. Allerdings ist Hilfsprogramm Verteilung nicht unbedingt eine algorithmische gute Wahl für Workloads, bei die hoher Aktivität anfrageanstieg sind oder Programme, die, in denen die arbeitsauslastung schnell und nach dem Zufallsprinzip zwischen Prozessoren verlagert.

Es wird empfohlen, für Workloads dieser Art Deaktivieren der Hilfsprogramm-Verteilung mit den folgenden Befehlen:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor DISTRIBUTEUTIL 0
Powercfg -setactive scheme_current
```

## <a name="see-also"></a>Siehe auch
- [Überlegungen zur Leistung von Server-Hardware](../index.md)
- [Server Hardware Power Considerations](../power.md) (Überlegungen zum Energiebedarf von Serverhardware)
- [Processor Power Management (PPM) Tuning for the Windows Server Balanced Power Plan](processor-power-management-tuning.md) (Optimieren der Prozessorenergieverwaltung (Processor Power Management (PPM)) für den ausgewogenen Energiesparplan von Windows Server)
- [Recommended Balanced Power Plan Parameters for Workloads Requiring Quick Response Times](recommended-balanced-plan-parameters.md) (Empfohlene Parameter für den ausgewogenen Energiesparplan für Workloads, die kurze Antwortzeiten erfordern)
