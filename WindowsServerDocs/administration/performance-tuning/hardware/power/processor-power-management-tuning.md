---
title: Optimieren der Prozessor Energie Verwaltung (ppm) für den Energie Sparplan von Windows Server ausgeglichen
description: Optimieren der Prozessor Energie Verwaltung (ppm) für den Energie Sparplan von Windows Server ausgeglichen
ms.topic: conceptual
ms.author: qizha;tristanb
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 1fcc21df93d9963ee83159c1df2fcf918ddbbfba
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992375"
---
# <a name="processor-power-management-ppm-tuning-for-the-windows-server-balanced-power-plan"></a>Optimieren der Prozessor Energie Verwaltung (ppm) für den Energie Sparplan von Windows Server ausgeglichen

Ab Windows Server 2008 bietet Windows Server drei Energie Sparpläne: **ausgeglichen**, **hohe Leistung**und **Energiespar**Modus. Der **ausgeglichene** Energie Sparplan ist die Standardoption, mit der die beste Energieeffizienz für eine Reihe typischer Server Arbeits Auslastungen erzielt werden soll. In diesem Thema werden die Arbeits Auslastungen beschrieben, die verwendet wurden, um die Standardeinstellungen für das **ausgeglichene** Schema für die letzten Versionen von Windows zu ermitteln.

Wenn Sie ein Server System mit stark unterschiedlichen workloadmerkmalen oder Leistungs-und Leistungsanforderungen als diese Arbeits Auslastungen ausführen, sollten Sie die Standardeinstellungen für Energie Einstellungen (d. h. Erstellen eines benutzerdefinierten Energie Sparplans) optimieren. Eine Quelle nützlicher Optimierungs Informationen sind die [Leistungsaspekte der Server Hardware](../power.md). Alternativ können Sie sich entscheiden, dass der **High Performance** -Energie Sparplan die richtige Wahl für Ihre Umgebung ist. Dadurch wird erkannt, dass Sie für eine gewisse höhere Reaktionsfähigkeit wahrscheinlich eine beträchtliche Stromversorgung in Exchange erreichen werden.

> [!IMPORTANT]
> Sie sollten die in Windows Server enthaltenen Energierichtlinien nutzen, es sei denn, Sie müssen ein benutzerdefiniertes erstellen und wissen, dass Ihre Ergebnisse abhängig von den Merkmalen der Arbeitsauslastung variieren.

## <a name="windows-processor-power-tuning-methodology"></a>Methodik der Energieoptimierung für Windows-Prozessoren

### <a name="tested-workloads"></a>Getestete Workloads

Arbeits Auslastungen werden ausgewählt, um einen bestmöglichen Satz von "typischen" Windows Server-Workloads abzudecken. Natürlich ist dieser Satz nicht für die gesamte Breite der realen Serverumgebungen repräsentativ.

Die Optimierung der einzelnen Energierichtlinien basiert auf den Daten, die von den folgenden fünf Workloads gesteuert werden:

- **IIS-Webserver-Arbeitsauslastung**

    Ein interner Microsoft-Vergleichstest mit dem Namen "Web Fundamentals" wird verwendet, um die Energieeffizienz von Plattformen mit IIS-Webserver zu optimieren Das Setup enthält einen Webserver und mehrere Clients, die den Web Access-Datenverkehr simulieren. Die Verteilung dynamischer, statischer (in-Memory) und statischer kalter (Datenträger Zugriff erforderlich) Web Pages basiert auf statistischen Studien von Produktionsservern. Um die CPU-Kerne des Servers auf die vollständige Auslastung (ein Ende des getesteten Spektrums) zu übersetzen, benötigt das Setup ausreichend schnelle Netzwerk-und Datenträger Ressourcen.

- **Arbeitsauslastung der SQL Server Datenbank**

    [TPC-E](http://www.tpc.org/tpce/default.asp) Benchmark ist ein beliebter Benchmark für die Analyse der Datenbankleistung. Es wird verwendet, um eine OLTP-Arbeitsauslastung für ppm-Optimierungs Optimierungen zu generieren. Diese Arbeitsauslastung weist eine beträchtliche Datenträger-e/a auf und hat daher eine hohe Leistungsanforderung für das Speichersystem und die Speichergröße.

- **Datei Server-Arbeitsauslastung**

    Ein von Microsoft entwickelter Benchmark namens [FSCT](http://www.snia.org/sites/default/files2/sdc_archives/2009_presentations/tuesday/BartoszNyczkowski-JianYan_FileServerCapacityTool.pdf) wird verwendet, um eine SMB-Dateiserver-Arbeitsauslastung zu generieren. Er erstellt einen großen Datei Satz auf dem Server und verwendet viele Client Systeme (tatsächlich oder virtualisiert) zum Generieren von Datei Öffnungs-, Schließ-, Lese-und Schreibvorgängen. Die Vorgangs Mischung basiert auf statistischen Studien von Produktionsservern. Er betont CPU-, Datenträger-und Netzwerkressourcen.

- **Specpower – Java-Arbeitsauslastung**

    [Specpower \_ ssj2008](http://spec.org/power_ssj2008/) ist der erste Branchen standardspezifikations-Benchmark, der die Leistungs-und Leistungsmerkmale zusammen wertet. Dabei handelt es sich um eine serverseitige Java-Arbeitsauslastung mit unterschiedlichen CPU-Lade Graden. Es sind nicht viele Datenträger-oder Netzwerkressourcen erforderlich, es sind jedoch bestimmte Anforderungen an die Arbeitsspeicher Bandbreite erforderlich. Fast alle CPU-Aktivitäten werden im Benutzermodus ausgeführt. die kernelmodusaktivität hat keine großen Auswirkungen auf die Leistungs-und Leistungsmerkmale der Benchmarks, mit Ausnahme der Energie Verwaltungsentscheidungen.

- **Anwendungs Server-Arbeitsauslastung**

    Der [SAP-SD-](http://global.sap.com/campaigns/benchmark/index.epx) Vergleichstest wird verwendet, um eine Anwendungsserver-Arbeitsauslastung zu generieren. Es wird eine zweistufige Installation mit der-Datenbank und dem Anwendungsserver auf demselben Server Host verwendet. Diese Arbeitsauslastung nutzt auch die Antwortzeit als Leistungs Metrik, die von anderen getesteten Workloads abweicht. Daher wird es verwendet, um die Auswirkung von ppm-Parametern auf Reaktionsfähigkeit zu überprüfen. Es ist jedoch nicht für alle Latenz sensiblen produktionsworkloads repräsentativ.

Alle Benchmarks außer specpower wurden ursprünglich für die Leistungsanalyse entwickelt und daher für die Ausführung bei Spitzenlast Ebenen erstellt. Allerdings sind Mittel-zu-Licht-Ladestufen für reale Produktionsserver häufiger und für **ausgeglichene** Plan Optimierungen interessanter. Wir führen die Benchmarks mit verschiedenen einschränkenden Methoden (z. b. durch Verringern der Anzahl aktiver Benutzer/Clients) auf unterschiedlichen Belastungsstufen von 100% bis zu 10% (in 10%-Schritten) aus.

### <a name="hardware-configurations"></a>Hardwarekonfigurationen

Für jede Version von Windows werden die aktuellen Produktionsserver in der Energie Sparplan-Analyse und-Optimierung verwendet. In einigen Fällen wurden die Tests in präproduktionssystemen ausgeführt, deren releasezeitplan mit der nächsten Windows-Version übereinstimmt.

Da die meisten Server mit 1 bis 4 Prozessor Sockets verkauft werden, und da die Wahrscheinlichkeit, dass für Server mit horizontaler Skalierung die Energieeffizienz als Hauptanliegen festgestellt wird, werden die Tests der Energiespar Plan Optimierung hauptsächlich auf zwei socketsystemen und vier socketsystemen ausgeführt. Die Größe der RAM-, Datenträger-und Netzwerkressourcen für jeden Test wird ausgewählt, damit jedes System bis zu seiner vollständigen Kapazität ausgeführt werden kann. dabei werden die Kosteneinschränkungen berücksichtigt, die normalerweise für reale Serverumgebungen gelten, wie z. b. die angemessene Beibehaltung der Konfigurationen.

> [!IMPORTANT]
> Obwohl das System bei Spitzenlast ausgeführt werden kann, optimieren wir in der Regel eine höhere Auslastung, da Server, die mit ihren Spitzenlast Ebenen konsistent ausgeführt werden, den **hochleistungsfähigen** Energie Sparplan verwenden sollten, wenn die Energieeffizienz eine hohe Priorität ist.

### <a name="metrics"></a>Metriken

Alle getesteten Benchmarks verwenden den Durchsatz als Leistungs Metrik. Die Antwortzeit wird als eine SLA-Anforderung für diese Arbeits Auslastungen betrachtet (mit Ausnahme von SAP, bei der es sich um eine primäre Metrik handelt). Beispielsweise wird ein benchmarklauf als "gültig" betrachtet, wenn die mittlere oder Maximale Antwortzeit kleiner als ein bestimmter Wert ist.

Daher verwendet die ppm-Optimierungs Analyse auch einen Durchsatz als Leistungs Metrik.  Bei der höchsten Auslastung (100% CPU-Auslastung) ist unser Ziel, dass der Durchsatz aufgrund von Optimierungen der Energie Verwaltung nicht mehr als ein paar Prozent verringern sollte. Der wichtigste Aspekt ist jedoch, die Energieeffizienz (wie unten definiert) auf mittlerer und niedriger Auslastung zu maximieren.

![Formel für Energieeffizienz](../../media/serverperf-ppm-formula.jpg)

Durch das Ausführen der CPU-Kerne bei niedrigeren Frequenzen wird der Energieverbrauch reduziert. Niedrigere Frequenzen verringern jedoch in der Regel den Durchsatz und erhöhen die Reaktionszeit. Für den **ausgeglichenen** Energie Sparplan ist ein beabsichtigter Kompromiss von Reaktionsfähigkeit und Energieeffizienz vorhanden. Die SAP-workloadtests und die Antwortzeit-SLAs für die anderen Arbeits Auslastungen stellen sicher, dass die Erhöhung der Antwortzeit für diese spezifischen Workloads keinen bestimmten Schwellenwert (z. b. 5%) überschreitet.

> [!NOTE]
> Wenn die Arbeitsauslastung die Antwortzeit als Leistungs Metrik verwendet, sollte das System entweder zum **hochleistungsfähigen** Energie Sparplan wechseln oder einen **ausgeglichenen** Energie Sparplan ändern, wie in [Empfohlene ausgeglichene Energie Sparplan Parameter für die schnelle Reaktionszeit empfohlen](recommended-balanced-plan-parameters.md).

### <a name="tuning-results"></a>Optimierungsergebnisse

Ab Windows Server 2008 hat Microsoft mit Intel und AMD gearbeitet, um die ppm-Parameter für die aktuellsten Server Prozessoren für die einzelnen Windows-Releases zu optimieren. Für jede der zuvor erläuterten Workloads wurde eine enorme Anzahl von ppm-Parameterkombinationen getestet, um die optimale Energieeffizienz auf unterschiedlichen Auslastungs Ebenen zu ermitteln. Bei der Optimierung von Software Algorithmen und bei der Entwicklung von Hardware-Energie Architekturen hatte jeder neue Windows-Server immer eine bessere oder gleichmäßige Energieeffizienz als seine früheren Versionen im Bereich der getesteten Workloads.

Die folgende Abbildung zeigt ein Beispiel für die Energieeffizienz unter verschiedenen TPC-E-Ladestufen auf einem 4-socketproduktionsserver, auf dem Windows Server 2008 R2 ausgeführt wird. Im Vergleich zu Windows Server 2008 wird eine Verbesserung von 8% auf mittlerer Auslastung angezeigt.

![Energieeffizienz Vergleich](../../media/serverperf-ppm-figure1.jpg)

## <a name="customized-tuning-suggestions"></a>Angepasste Optimierungsvorschläge

Wenn sich Ihre primären workloadmerkmale erheblich von den fünf Arbeits Auslastungen unterscheiden, die für die standardmäßige **ausgeglichene** Power Plan ppm-Optimierung verwendet werden, können Sie experimentieren, indem Sie einen oder mehrere ppm-Parameter ändern, um die optimale Eignung für Ihre Umgebung

Aufgrund der Anzahl und Komplexität von Parametern ist dies möglicherweise eine schwierige Aufgabe. Wenn Sie jedoch nach dem optimalen Kompromiss zwischen Energieverbrauch und workloadwirksamkeit für Ihre spezielle Umgebung suchen, ist es möglicherweise sinnvoll, dies zu tun.

 Den gesamten Satz von anpassbaren ppm-Parametern finden Sie unter [Optimieren der Prozessor Energie Verwaltung](/previous-versions/windows/hardware/design/dn613983(v=vs.85)). Einige der einfachsten Leistungsparameter, mit denen Sie beginnen können, sind:

-   **Prozessorleistung erhöhen Sie den Schwellenwert und die Prozessorleistung erhöhen** – größere Werte verlangsamen die Leistungs-Antwort auf eine erhöhte Aktivität

-   **Schwellenwert für die Prozessorleistung verringern** – große Werte versetzen die Energie Antwort auf Leerlauf Zeiträume.

-   **Prozessorleistung verringern** – größere Werte erhöhen die Leistung allmählich in Leerlaufzeiten.

-   **Richtlinie zur Erhöhung der Prozessorleistung** – die "einzelne" Richtlinie verlangsamt die Leistungs-Antwort auf eine erhöhte und anhaltende Aktivität. die Richtlinie "Raketen" reagiert schnell auf eine größere Aktivität

-   **Richtlinie zur Verringerung der Prozessorleistung** – die "einzelne" Richtlinie verringert die Leistung in längeren Leerlaufzeiten allmählich. die Richtlinie "Raketen" sinkt bei der Eingabe eines Leerlauf Zeitraums sehr schnell.

>[!Important]
> Bevor Sie mit Experimenten beginnen, sollten Sie sich zunächst mit den Workloads vertraut machen, die Ihnen dabei helfen, die richtigen ppm-Parameter Optionen zu treffen und den Optimierungs Aufwand zu verringern.

### <a name="understand-high-level-performance-and-power-requirements"></a>Grundlegendes zu Leistungs-und Energieanforderungen auf hoher Ebene

Wenn Ihre Arbeitsauslastung "Echt Zeit" ist (z. b. anfällig für das Durchsuchen oder andere sichtbare Auswirkungen des Endbenutzers) oder eine sehr strenge Reaktions Anforderung (z. b. eine Aktien Vermittler) ist, und wenn der Energieverbrauch für Ihre Umgebung kein primäres Kriterium ist, sollten Sie wahrscheinlich einfach zum **hochleistungsfähigen** Energie Sparplan wechseln. Andernfalls sollten Sie die Reaktionszeit Anforderungen ihrer Arbeits Auslastungen kennen und dann die ppm-Parameter für die bestmögliche Energieeffizienz optimieren, die diese Anforderungen erfüllt.

### <a name="understand-underlying-workload-characteristics"></a>Grundlagen der Merkmale

Sie sollten Ihre Arbeits Auslastungen kennen und die Experiment Parametersätze für die Optimierung entwerfen. Wenn beispielsweise die Häufigkeit der CPU-Kerne sehr schnell beschleunigt werden muss (vielleicht haben Sie eine bursty-Arbeitsauslastung mit erheblichen Leerlaufzeiten), Sie benötigen jedoch sehr schnelle Reaktionsfähigkeit, wenn eine neue Transaktion durchgeführt wird, und die Leistungs Erhöhung der Prozessorleistung muss möglicherweise auf "Rocket" festgelegt werden (was bedeutet, dass die CPU-Kern Frequenz auf den maximalen Wert stößt, anstatt Sie über einen bestimmten Zeitraum hinweg zu überschreiten).

Wenn Ihre Arbeitsauslastung sehr gut ist, kann das Intervall von ppm verkürzt werden, damit die CPU-Frequenz schneller nach Erreichen eines Burst Vorgangs beschleunigt wird. Wenn Ihre Arbeitsauslastung keine hohe Thread Parallelität hat, können Sie mit der Kern-Platz Überschreitung aktivieren, um die Ausführung der Arbeitsauslastung auf einer geringeren Anzahl von Kernen zu erzwingen, was möglicherweise zu einer Verbesserung der Prozessor Cache-Trefferquoten führt.

Wenn Sie nur die CPU-Frequenzen auf mittlerer Auslastung erhöhen möchten (d. h. keine leichten workloadebenen), können Sie die Schwellenwerte für die Erhöhung/Verringerung der Prozessorleistung so anpassen, dass Sie nicht reagieren, bis bestimmte Aktivitätsstufen beobachtet werden.

### <a name="understand-periodic-behaviors"></a>Grundlegendes zum periodischen Verhalten

Es gibt möglicherweise unterschiedliche Leistungsanforderungen für den Tag und die Nacht oder über das Wochenende, oder es gibt verschiedene Workloads, die zu unterschiedlichen Zeiten ausgeführt werden. In diesem Fall ist ein Satz von ppm-Parametern für alle Zeiträume möglicherweise nicht optimal. Da mehrere benutzerdefinierte Energie Sparpläne entwickelt werden können, ist es möglich, sogar für verschiedene Zeiträume zu optimieren und zwischen Energie Sparplänen mithilfe von Skripts oder anderen Methoden der dynamischen Systemkonfiguration zu wechseln.

Dies erhöht wiederum die Komplexität des Optimierungsprozesses, sodass es eine Frage ist, wie viel Wert aus dieser Art von Optimierung erzielt wird. Dies wird wahrscheinlich bei signifikanten Hardware Upgrades oder Änderungen an der Arbeitsauslastung wiederholt.

Aus diesem Grund bietet Windows einen **ausgeglichenen** Energie Sparplan an erster Stelle, denn in vielen Fällen ist es wahrscheinlich nicht sinnvoll, eine manuelle Optimierung für eine bestimmte Arbeitsauslastung auf einem bestimmten Server durchzuführen.

## <a name="see-also"></a>Weitere Informationen
- [Überlegungen zur Leistung von Serverhardware](../index.md)
- [Server Hardware Power Considerations](../power.md) (Überlegungen zum Energiebedarf von Serverhardware)
- [Power and Performance Tuning](power-performance-tuning.md) (Leistungs- und Energieoptimierung)
- [Processor Power Management (PPM) Tuning for the Windows Server Balanced Power Plan](processor-power-management-tuning.md) (Optimieren der Prozessorenergieverwaltung (Processor Power Management (PPM)) für den ausgewogenen Energiesparplan von Windows Server)
- [Recommended Balanced Power Plan Parameters for Workloads Requiring Quick Response Times](recommended-balanced-plan-parameters.md) (Empfohlene Parameter für den ausgewogenen Energiesparplan für Workloads, die kurze Antwortzeiten erfordern)