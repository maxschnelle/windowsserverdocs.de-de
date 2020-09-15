---
title: Übersicht über Leistungs-und Leistungsoptimierung für Windows Server
description: Übersicht über die Optimierung der Prozessor Energie Verwaltung (ppm) für den Windows-Server.
ms.topic: conceptual
ms.author: qizha
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 1e1f409e5c84a603c628e1ceebe97317864c8785
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077612"
---
# <a name="power-and-performance-tuning"></a>Energie- und Leistungsoptimierung

Die Energieeffizienz ist in Enterprise-und Rechenzentrums Umgebungen immer wichtiger, und es werden weitere Kompromisse in der Mischung der Konfigurationsoptionen hinzugefügt.

Windows Server 2016 ist für eine ausgezeichnete Energieeffizienz mit minimalen Auswirkungen auf die Leistung in einer Vielzahl von Workloads von Kunden optimiert. Durch die Optimierung der [Prozessor Energie Verwaltung (ppm) für den Windows Server-ausgeglichenen Energie Sparplan](processor-power-management-tuning.md) werden die Arbeits Auslastungen beschrieben, die zum Optimieren der Standardparameter in Windows Server 2016 verwendet werden, und Vorschläge für angepasste Tunings bereitgestellt.

In diesem Abschnitt werden die vor-und Nachteile der Energieeffizienz erweitert, damit Sie fundierte Entscheidungen treffen können, wenn Sie die Standardeinstellungen für die Energie Einstellungen auf dem Server anpassen müssen. Der Großteil der Server Hardware und Arbeits Auslastungen sollte bei Ausführung von Windows Server 2016 jedoch keine Administrator Energieoptimierung erfordern.

## <a name="calculating-server-energy-efficiency"></a>Berechnen der Server Energieeffizienz

Wenn Sie Ihren Server auf Energieeinsparung optimieren, müssen Sie auch die Leistung in Erwägung gezogen. Die Optimierung wirkt sich auf die Leistung und Leistung aus, manchmal unverhältnismäßig. Für jede mögliche Anpassung sollten Sie den Energiehaushalt und die Leistungsziele in Erwägung gezogen, um zu bestimmen, ob der Kompromiss akzeptabel ist.

Sie können das energieeffizienzverhältnis Ihres Servers für eine nützliche Metrik berechnen, die Leistungs-und Leistungsinformationen enthält. Bei der Energieeffizienz handelt es sich um das Verhältnis zwischen Arbeitsaufwand und der durchschnittlichen Stromversorgung, die während eines bestimmten Zeitraums erforderlich ist.

![Formel für Energieeffizienz](../../media/perftune-guide-power-formula.png)

Sie können diese Metrik verwenden, um praktische Ziele festzulegen, die den Kompromiss zwischen Strom und Leistung berücksichtigen. Im Gegensatz dazu können durch das Ziel von 10 Prozent Energieeinsparungen im Rechenzentrum die entsprechenden Auswirkungen auf die Leistung und umgekehrt nicht erfasst werden.

Ebenso gilt: Wenn Sie Ihren Server optimieren, um die Leistung um 5 Prozent zu steigern, und dies zu 10 Prozent höheren Energieverbrauch führt, ist das Gesamtergebnis für Ihre Geschäftsziele möglicherweise nicht akzeptabel. Die Metrik "Energieeffizienz" ermöglicht eine besser informierte Entscheidungsfindung als Leistungs-oder Leistungsmetriken.

## <a name="measuring-system-energy-consumption"></a>Messen des System Energieverbrauchs

Sie sollten eine grundlegende Strommessung einrichten, bevor Sie Ihren Server auf Energieeffizienz optimieren.

Wenn Ihr Server über die erforderliche Unterstützung verfügt, können Sie mithilfe der Funktionen für Energiemessung und Budgetierung in Windows Server 2016 den Energieverbrauch auf Systemebene mithilfe des System Monitors anzeigen.

Eine Möglichkeit, um zu bestimmen, ob Ihr Server die Unterstützung für Messung und Budgetierung bietet, ist die Überprüfung des [Windows Server-Katalogs](https://www.windowsservercatalog.com). Wenn Ihr Server Modell für die neue Qualifizierung der verbesserten Energie Verwaltung im Windows-Hardware Zertifizierungsprogramm qualifiziert ist, ist es garantiert, dass die Messungs-und Budgetierungs Funktionen unterstützt werden.

Eine weitere Möglichkeit zum Überprüfen der Messungs Unterstützung besteht darin, die Leistungsindikatoren im System Monitor manuell zu suchen. Öffnen Sie den System Monitor, wählen Sie Leistungsindikatoren **Hinzufügen**aus, und suchen Sie dann die **Leistungs** Indikator Gruppe.

Wenn benannte Instanzen von Power Meter in dem Feld mit der Bezeichnung **Instanzen des ausgewählten Objekts**angezeigt werden, unterstützt die Plattform die Messung. In der ausgewählten Leistungsanzeige wird der **Leistungs Leistungs-Leistungs-Leistungs-Leistungs-Leistungs-Leistungs-Leistungs** Anzeige Die genaue Ableitung des Power Data-Werts ist nicht angegeben. Beispielsweise kann es sich um eine sofortige Stromversorgung oder eine durchschnittliche Stromversorgung über ein Zeitintervall handeln.

Wenn Ihre Server Plattform die Messung nicht unterstützt, können Sie ein physisches Messungs Gerät verwenden, das mit der Stromversorgung-Eingabe verbunden ist, um den System Strom oder den Energieverbrauch zu messen.

Zum Einrichten einer Baseline sollten Sie die durchschnittliche Stromversorgung für verschiedene System Ladepunkte Messen, von Leerlauf auf 100 Prozent (maximaler Durchsatz), um eine Auslastungs Linie zu generieren. Die folgende Abbildung zeigt Lade Zeilen für drei Beispielkonfigurationen:

![Beispiel lade Zeilen](../../media/perftune-guide-sample-loadlines.png)

Mit Lade Linien können Sie die Leistung und den Energieverbrauch von Konfigurationen an allen ladepunkten auswerten und vergleichen. In diesem speziellen Beispiel ist es ganz einfach, die beste Konfiguration zu sehen. Es können jedoch problemlos Szenarien eingesetzt werden, in denen eine Konfiguration für hohe Workloads am besten geeignet ist, und eine Konfiguration eignet sich am besten für einfache Workloads.

Sie müssen ihre workloadanforderungen gründlich verstehen, um eine optimale Konfiguration auszuwählen. Gehen Sie nicht davon aus, dass Sie beim Auffinden einer guten Konfiguration immer optimal bleiben. Sie sollten die System Auslastung und den Energieverbrauch in regelmäßigen Abständen und nach Änderungen an Arbeits Auslastungen, Arbeits Auslastungs Stufen oder Server Hardware messen.

## <a name="diagnosing-energy-efficiency-issues"></a>Diagnostizieren von energieeffizienzproblemen

**PowerCfg.exe** unterstützt eine Befehlszeilenoption, die Sie verwenden können, um die Energieeffizienz im Leerlauf Ihres Servers zu analysieren. Wenn Sie PowerCfg.exe mit der Option **/Energy** ausführen, führt das Tool einen 60-Sekunden-Test aus, um potenzielle Probleme mit der Energieeffizienz zu erkennen. Das Tool generiert einen einfachen HTML-Bericht im aktuellen Verzeichnis.

> [!Important]
> Stellen Sie sicher, dass alle lokalen apps geschlossen sind, bevor Sie **PowerCfg.exe**ausführen, um eine genaue Analyse sicherzustellen. 

Verkürzte Zeit Geber Raten, Treiber, die keine Unterstützung der Energie Verwaltung haben, und übermäßige CPU-Auslastung sind einige der Verhaltensprobleme, die vom Befehl " **powercfg/Energy** " erkannt werden. Dieses Tool bietet eine einfache Möglichkeit, Probleme mit der Energie Verwaltung zu erkennen und zu beheben, was potenziell zu erheblichen Kosteneinsparungen in einem großen Rechenzentrum führen kann.

Weitere Informationen zu PowerCfg.exe finden [Sie unter Verwenden von PowerCfg zum Auswerten der Energieeffizienz des Systems](/previous-versions/windows/hardware/download/dn550976(v=vs.85)).

## <a name="using-power-plans-in-windows-server"></a>Verwenden von Energie Sparplänen in Windows Server

Windows Server 2016 verfügt über drei integrierte Energie Sparpläne, die auf unterschiedliche Geschäftsanforderungen zugeschnitten sind. Diese Pläne bieten eine einfache Möglichkeit zum Anpassen eines Servers, um Leistungs-oder Leistungsziele zu erreichen. In der folgenden Tabelle werden die Pläne beschrieben, die gängigen Szenarien aufgelistet, in denen die einzelnen Pläne verwendet werden, und es werden einige Implementierungsdetails für jeden Plan aufgeführt.

| **Planen** | **Beschreibung** | **Allgemeine anwendbare Szenarien** | **Implementierungs Highlights** |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ausgeglichen (empfohlen) | Standardeinstellung. Zielt auf eine gute Energieeffizienz mit minimalen Auswirkungen auf die Leistung ab. | Allgemeines Computing | Entspricht der Kapazität für die Nachfrage. Energiesparende Features sind ein ausgewogenes Verhältnis zwischen Leistung und Leistung. |
| Hohe Leistung | Steigert die Leistung auf Kosten des hohen Energieverbrauchs. Leistungs-und wärmegrenzen, Betriebsausgaben und Zuverlässigkeits Überlegungen gelten. | Apps mit geringer Latenz und app-Code, der von den Prozessor Leistungsänderungen abhängig ist | Prozessoren werden immer mit dem höchsten Leistungsstatus (einschließlich der Frequenzen "Turbo") gesperrt. Alle Kerne werden entgeparkt. Die thermische Ausgabe kann signifikant sein. |
| Energiesparmodus | Schränkt die Leistung ein, um Energie zu sparen und Betriebskosten zu senken. Nicht empfohlen, ohne gründliche Tests, um sicherzustellen, dass die Leistung ausreichend ist. | Bereit Stellungen mit eingeschränkten Energie Budgets und thermischen Einschränkungen | Begrenzt die Prozessorfrequenz mit einem Prozentsatz des maximalen Werts (falls unterstützt) und ermöglicht andere energiesparende Features. |


Diese Energie Sparpläne sind in Windows für abwechselnde aktuelle (AC) und Direct Current (DC) Systeme vorhanden, aber wir gehen davon aus, dass die Server immer eine Stromversorgung der Stromversorgung verwenden.

Weitere Informationen zu Energie Sparplänen und Energierichtlinien Konfigurationen finden Sie unter [Energierichtlinien Konfiguration und-Bereitstellung in Windows](/previous-versions/windows/hardware/design/dn642106(v=vs.85)).

> [!Note]
> Einige Serverhersteller verfügen über eigene Energie Verwaltungs Optionen, die über die BIOS-Einstellungen verfügbar sind. Wenn das Betriebssystem keine Kontrolle über die Energie Verwaltung hat, wirkt sich das Ändern der Energie Sparpläne in Windows nicht auf die Systemleistung und-Leistung aus.

## <a name="tuning-processor-power-management-parameters"></a>Optimieren der Energie Verwaltungs Parameter des Prozessors

Jeder Energie Sparplan stellt eine Kombination aus zahlreichen zugrunde liegenden Energie Verwaltungs Parametern dar. Bei den integrierten Plänen handelt es sich um drei Sammlungen empfohlener Einstellungen, die eine Vielzahl von Arbeits Auslastungen und Szenarios abdecken. Wir erkennen jedoch, dass diese Pläne nicht den Anforderungen aller Kunden entsprechen.

In den folgenden Abschnitten wird beschrieben, wie Sie einige spezifische Parameter für die Prozessor Energie Verwaltung optimieren, um die Ziele zu erreichen, die von den drei integrierten Plänen nicht behandelt werden. Wenn Sie eine größere Anzahl von Strom Parametern verstehen müssen, finden Sie weitere Informationen unter [Energierichtlinien Konfiguration und-Bereitstellung in Windows](/previous-versions/windows/hardware/design/dn642106(v=vs.85)).

## <a name="processor-performance-boost-mode"></a>Boost-Modus für Prozessorleistung

Intel Turbo Boost-und AMD Turbo Core-Technologien sind Features, die es Prozessoren ermöglichen, eine zusätzliche Leistung zu erzielen, wenn Sie am nützlichsten ist (d. h. bei hohen System Belastungen). Diese Funktion erhöht jedoch den CPU-Kernenergie Verbrauch, sodass Windows Server 2016 Turbo Technologien basierend auf der verwendeten Energierichtlinie und der spezifischen Prozessor Implementierung konfiguriert.

Turbo ist für hochleistungsfähige Energie Sparpläne auf allen Intel-und AMD-Prozessoren aktiviert und ist für Energiespar Energie Sparpläne deaktiviert. Für ausgeglichene Energie Sparpläne auf Systemen, die auf einer herkömmlichen P-State-basierten Frequenzverwaltung basieren, ist Turbo standardmäßig nur aktiviert, wenn die Plattform das EPB-Register unterstützt.

> [!Note]
> Das EPB-Register wird nur in Intel Westmere-Prozessoren und höher unterstützt.

Für Intel Nehalem-und AMD-Prozessoren ist Turbo standardmäßig auf P-State-basierten Plattformen deaktiviert. Wenn ein System jedoch die kollaborative Prozessor Leistungskontrolle (cppc) unterstützt, bei der es sich um einen neuen alternativen Modus für die Leistungs Kommunikation zwischen dem Betriebssystem und der Hardware handelt (definiert in ACPI 5,0), kann Turbo eingeschaltet werden, wenn das Windows-Betriebssystem die Hardware dynamisch zum Bereitstellen der höchstmöglichen Leistungsstufen anfordert.

Um die Funktion "Turbo Boost" zu aktivieren oder zu deaktivieren, muss der Parameter "Processor Performance Boost Mode" vom Administrator oder durch die Standardparameter Einstellungen für den ausgewählten Energie Sparplan konfiguriert werden. Der Streamingmodus für die Prozessorleistung weist fünf zulässige Werte auf, wie in Tabelle 5 dargestellt.

Bei der P-State-basierten Steuerung sind die Optionen deaktiviert, aktiviert (Turbo ist für die Hardware verfügbar, wenn eine nominale Leistung angefordert wird) und effizient (Turbo ist nur verfügbar, wenn das EPB-Register implementiert ist).

Für cppc-basiertes Steuerelement sind die Optionen deaktiviert, effizient aktiviert (Windows gibt die genaue Menge an Turbo an, die bereitgestellt werden soll) und aggressiv (Windows fragt nach "maximale Leistung", um Turbo zu aktivieren).

In Windows Server 2016 ist der Standardwert für den Boost-Modus 3.

| **Name** | **P-Zustands basiertes Verhalten** | **Cppc-Verhalten** |
|--------------------------|------------------------|-------------------|
| 0 (deaktiviert) | Disabled | Disabled |
| 1 (aktiviert) | Aktiviert | Effizient aktiviert |
| 2 (aggressiv) | Aktiviert | Aggressive |
| 3 (effizient aktiviert) | Effizient | Effizient aktiviert |
| 4 (effizient aggressiv) | Effizient | Aggressive |


Die folgenden Befehle aktivieren den Prozessor Leistungs Boost-Modus für den aktuellen Energie Sparplan (geben Sie die Richtlinie mit einem GUID-Alias an):

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor PERFBOOSTMODE 1
Powercfg -setactive scheme_current
```

> [!Important]
> Sie müssen den **POWERCFG-SETACTIVE-** Befehl ausführen, um die neuen Einstellungen zu aktivieren. Der Server muss nicht neu gestartet werden.

Wenn Sie diesen Wert für andere Energie Sparpläne als den aktuell ausgewählten Plan festlegen möchten, können Sie \_ anstelle des aktuellen Schemas Aliase wie "Schema Max (Strom Schoner)", "Schema \_ Min (hohe Leistung)" und "Schema \_ ausgeglichen" (ausgeglichen) verwenden \_ . Ersetzen Sie "Schema Current" in den POWERCFG-SETACTIVE-Befehlen, die zuvor durch den gewünschten Alias angezeigt wurden, um diesen Energie Sparplan zu aktivieren.

Wenn Sie z. b. den Boost-Modus im Energiespar Plan anpassen und diesen als aktuellen Plan festlegen möchten, führen Sie die folgenden Befehle aus:

``` syntax
Powercfg -setacvalueindex scheme_max sub_processor PERFBOOSTMODE 1
Powercfg -setactive scheme_max
```

## <a name="minimum-and-maximum-processor-performance-state"></a>Minimaler und maximaler Prozessor Leistungsstatus

Prozessoren ändern sich sehr schnell zwischen Leistungszuständen (P-Zustände), um die Bedarfs gesteuerte Bereitstellung zu erfüllen, die Leistung bei Bedarf zu erfüllen und nach Möglichkeit Energie zu sparen. Wenn für Ihren Server bestimmte Anforderungen an eine hohe Leistung oder einen minimalen Energieverbrauch gelten, empfiehlt es sich ggf., den **minimalen Prozessor Leistungsstatus** -Parameter oder den Parameter " **Maximum Processor Performance State** " zu konfigurieren.

Die Werte für die Parameter " **Minimal Prozessorleistung** " und " **maximaler Prozessorleistung** " werden als Prozentsatz der maximalen Prozessorfrequenz mit einem Wert im Bereich von 0 – 100 ausgedrückt.

Wenn für Ihren Server eine extrem geringe Latenz, eine invariante CPU-Frequenz (z. b. für wiederholbare Tests) oder die höchsten Leistungsstufen erforderlich sind, möchten Sie möglicherweise nicht, dass die Prozessoren zu den niedrigeren Leistungszuständen wechseln. Für einen solchen Server können Sie mit den folgenden Befehlen den minimalen Prozessor Leistungsstatus auf 100 Prozent begrenzen:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor PROCTHROTTLEMIN 100
Powercfg -setactive scheme_current
```

Wenn der Server einen niedrigeren Energieverbrauch erfordert, sollten Sie den Leistungsstatus des Prozessors in einem Prozentsatz des maximalen Werts begrenzen. Beispielsweise können Sie den Prozessor auf 75 Prozent seiner maximalen Häufigkeit beschränken, indem Sie die folgenden Befehle verwenden:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor PROCTHROTTLEMAX 75
Powercfg -setactive scheme_current
```

> [!Note]
> Die Abdeckung der Prozessorleistung mit einem Prozentsatz des maximalen Werts erfordert Prozessorunterstützung. Überprüfen Sie in der Prozessor Dokumentation, ob eine solche Unterstützung vorhanden ist, oder zeigen Sie den Leistungs Monitor Leistungsindikatoren **% der maximalen Häufigkeit** in der **Prozessor** Gruppe an, um festzustellen, ob Häufigkeits Grenzwerte angewendet wurden.

## <a name="processor-performance-increase-and-decrease-of-thresholds-and-policies"></a>Prozessorleistung erhöhen und verringern von Schwellenwerten und Richtlinien

Die Geschwindigkeit, mit der sich der Leistungszustand eines Prozessors erhöht oder verringert, wird von mehreren Parametern gesteuert. Die folgenden vier Parameter haben die offensichtlichste Auswirkung:

-   Schwellenwert für die **Prozessor Leistungs Erhöhung** definiert den Auslastungs Wert, oberhalb dessen sich der Leistungsstatus eines Prozessors erhöht. Größere Werte verlangsamen die Rate der Erhöhung des Leistungs Zustands als Reaktion auf erhöhte Aktivitäten.

-   Schwellenwert für die **Verringerung der Prozessorleistung** definiert den Verwendungs Wert, unter dem sich der Leistungsstatus eines Prozessors verringert. Größere Werte erhöhen die Rate der Abnahme für den Leistungszustand während Leerlaufzeiten.

-   **Verringerung der Prozessorleistung und Verringerung der Prozessorleistung** Die Richtlinie bestimmt, welcher Leistungsstatus bei einer Änderung festgelegt werden sollte. Die Richtlinie "Single" bedeutet, dass Sie den nächsten Status auswählt. "Rocket" bezeichnet den maximalen oder minimalen Leistungszustand. "Ideal" versucht, ein Gleichgewicht zwischen Leistung und Leistung zu finden.

Wenn Ihr Server z. b. eine extrem geringe Latenz erfordert, während Sie während Leerlaufzeiten weiterhin von geringer Leistung profitieren möchten, können Sie die Leistungs Zustands Zunahme für jede Zunahme der Auslastung versetzen und die Abnahme verlangsamen, wenn die Auslastung ausfällt. Mit den folgenden Befehlen wird die Erhöhung der Richtlinie auf "Rocket" festgelegt, um eine schnellere Zustands Erhöhung zu erhöhen, und die Richtlinie zum verringern auf "Single". Die Schwellenwerte für erhöhen und verringern werden auf 10 bzw. 8 festgelegt.

``` syntax
Powercfg.exe -setacvalueindex scheme_current sub_processor PERFINCPOL 2
Powercfg.exe -setacvalueindex scheme_current sub_processor PERFDECPOL 1
Powercfg.exe -setacvalueindex scheme_current sub_processor PERFINCTHRESHOLD 10
Powercfg.exe -setacvalueindex scheme_current sub_processor PERFDECTHRESHOLD 8
Powercfg.exe /setactive scheme_current
```

## <a name="processor-performance-core-parking-maximum-and-minimum-cores"></a>Prozessorleistung Core-Platz für maximale und minimale Kerne

Das Core-Parken ist ein Feature, das in Windows Server 2008 R2 eingeführt wurde. Die Prozessor Energie Verwaltung (ppm) und der Scheduler arbeiten zusammen, um die Anzahl der Kerne, die zum Ausführen von Threads zur Verfügung stehen, dynamisch anzupassen. Das ppm-Modul wählt eine Mindestanzahl von Kernen für die Threads aus, die geplant werden.

Für Kern Computer, die in der Regel geparkt sind, sind keine Threads geplant, und Sie werden in sehr niedrige Strom Zustände verschoben, wenn Interrupts, DPCs oder andere streng nicht ordnungs gleiche arbeiten verarbeitet werden. Die restlichen Kerne sind für den Rest der Arbeitsauslastung verantwortlich. Durch die Kern-Parkplätze kann die Energieeffizienz bei geringerer Auslastung potenziell gesteigert werden

Bei den meisten Servern bietet das standardmäßige standardmäßige Parkverhalten einen angemessenen Saldo aus Durchsatz und Energieeffizienz. Bei Prozessoren, bei denen die Kerne von Kern-Arbeits Auslastungen nicht so stark genutzt werden können, kann Sie standardmäßig deaktiviert werden.

Wenn für Ihren Server bestimmte Anforderungen an die Kernspeicher Plätze gelten, können Sie die Anzahl der Kerne steuern, die für das Parken verfügbar sind, indem Sie den Parameter Leistungsparameter für **Maximale Kerne der Prozessorleistung** oder den Parameter für die Parameter für die **minimale Kerne der Prozessorleistung** in Windows Server 2016.

Ein Szenario, bei dem die Kern-Parkplätze nicht immer optimal sind, ist, wenn mindestens ein aktiver Thread einer nicht trivialen Teilmenge von CPUs in einem NUMA-Knoten zugeordnet ist (d. h. mehr als 1 CPU, aber kleiner als der gesamte Satz von CPUs auf dem Knoten). Wenn der kernelingalgorithmus Kerne zum Aufheben der Wiederaufnahme (vorausgesetzt, dass eine Erhöhung der workloadintensität auftritt) abwählt, werden die Kerne innerhalb der aktiven, affininitiierten Teilmenge (bzw. Teilmengen) nicht immer zum Aufheben der Wiederaufnahme ausgewählt

Die Werte für diese Parameter sind Prozentwerte im Bereich von 0 – 100. Der Parameter für die maximale Anzahl von Kernen für die **Prozessorleistung** steuert den maximalen Prozentsatz der Kerne, die für das Entsperren (verfügbar zum Ausführen von Threads) verfügbar sein können, während der Parameter " **Prozessorleistung Core-minimal Kerne** " den minimalen Prozentsatz der Kerne steuert, die freigestellt werden können. Legen Sie zum Deaktivieren der Kern Parken den Parameter für die **Prozessorleistung Kerne für die minimale Kerne** auf 100 Prozent fest, indem Sie die folgenden Befehle verwenden:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor CPMINCORES 100
Powercfg -setactive scheme_current
```

Legen Sie den Parameter für die maximale Anzahl der **Prozessor Leistungs** Kerne auf 50 fest, um die Anzahl der Zeit Planungs Kerne auf 50 Prozent der maximalen Anzahl zu verringern:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor CPMAXCORES 50
Powercfg -setactive scheme_current
```

## <a name="processor-performance-core-parking-utility-distribution"></a>Prozessorleistung Core-Parkplatz Verteilung

Die hilfsprogrammverteilung ist eine algorithmische Optimierung in Windows Server 2016, die entwickelt wurde, um die Energieeffizienz für einige Workloads zu verbessern. Dabei werden nicht verschiebbare CPU-Aktivitäten (d. h. DPCs, Interrupts oder streng affinitialisierte Threads) nachverfolgt, und es wird die zukünftige Arbeit für jeden Prozessor basierend auf der Annahme vorhergesagt, dass verschiebbare Arbeit gleichmäßig auf alle nicht geparkten Kerne verteilt werden kann.

Die hilfsprogrammverteilung ist für einige Prozessoren standardmäßig für den ausgeglichenen Energie Sparplan aktiviert. Dadurch kann der Prozessor Stromverbrauch reduziert werden, indem die angeforderten CPU-Frequenzen von Arbeits Auslastungen gesenkt werden, die sich in einem relativ stabilen Zustand befinden. Die hilfsprogrammverteilung ist jedoch nicht notwendigerweise eine gute algorithmische Wahl für Workloads, die hohen Aktivitäts Spitzen unterliegen, oder für Programme, bei denen die Arbeitsauslastung schnell und nach dem Zufallsprinzip über Prozessoren verlagert wird.

Für solche Workloads empfiehlt es sich, die hilfsprogrammverteilung mithilfe der folgenden Befehle zu deaktivieren:

``` syntax
Powercfg -setacvalueindex scheme_current sub_processor DISTRIBUTEUTIL 0
Powercfg -setactive scheme_current
```

## <a name="additional-references"></a>Weitere Verweise

- [Überlegungen zur Leistung von Serverhardware](../index.md)
- [Server Hardware Power Considerations](../power.md) (Überlegungen zum Energiebedarf von Serverhardware)
- [Processor Power Management (PPM) Tuning for the Windows Server Balanced Power Plan](processor-power-management-tuning.md) (Optimieren der Prozessorenergieverwaltung (Processor Power Management (PPM)) für den ausgewogenen Energiesparplan von Windows Server)
- [Recommended Balanced Power Plan Parameters for Workloads Requiring Quick Response Times](recommended-balanced-plan-parameters.md) (Empfohlene Parameter für den ausgewogenen Energiesparplan für Workloads, die kurze Antwortzeiten erfordern)