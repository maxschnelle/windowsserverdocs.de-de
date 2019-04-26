---
title: Optimierung der Energiesparplan von Windows Server mit Lastenausgleich für die Energieverwaltung (PPM)
description: Optimierung der Energiesparplan von Windows Server mit Lastenausgleich für die Energieverwaltung (PPM)
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Qizha;TristanB
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 8a2ef4fd39554446aaac686e142ad24f53b4efaa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863051"
---
# <a name="processor-power-management-ppm-tuning-for-the-windows-server-balanced-power-plan"></a>Optimierung der Energiesparplan von Windows Server mit Lastenausgleich für die Energieverwaltung (PPM)

Ab Windows Server 2008 bietet Windows Server drei Energiesparpläne aus: **Mit Lastenausgleich**, **hohe Leistung**, und **Power Bildschirmschoner**. Die **ausgeglichen** Energiesparplan ist die Standardoption, die zielt darauf ab, die Energieeffizienz für eine Reihe von typischen Server-Workloads zu erhalten. In diesem Thema wird beschrieben, die arbeitsauslastungen, die verwendet wurden, um zu bestimmen, die Standardeinstellungen für die **ausgeglichen** -Schema für die letzten Versionen von Windows.

Wenn Sie ein Server-System, die andere workloadmerkmale oder Leistung und geringeren Energieverbrauch als für diese Workloads verfügt ausführen, möchten Sie möglicherweise optimieren Sie die Standardeinstellungen für die Power (d. h., einen benutzerdefinierten Energiesparplan erstellen). Ist eine Informationsquelle nützliche Optimierung der [Server Power Hardwareanforderungen](../power.md). Alternativ können Sie entscheiden, dass die **hohe Leistung** Energiesparplan ist die richtige Wahl für Ihre Umgebung erkennen, dass Sie wahrscheinlich eine erhebliche Energie, die im Austausch gegen gewisse erhöhte Reaktionsfähigkeit erreicht gelangen.

>[!Important]
> Nutzen Sie die Power-Richtlinien, die mit Windows Server enthalten sind, es sei denn, Sie eine spezifische Notwendigkeit haben, erstellen Sie eine benutzerdefinierte und sehr gute Kenntnisse, dass die Ergebnisse je nach den Eigenschaften Ihrer arbeitsauslastung variieren.

## <a name="windows-processor-power-tuning-methodology"></a>Windows-Prozessor Power Optimierung Methodik


### <a name="tested-workloads"></a>Getestete workloads

Workloads werden ausgewählt, auf einen Best-Effort-Prinzip "typische? Windows Server-Workloads. Dieser Satz ist offensichtlich nicht vorgesehen, für die ganze Bandbreite der echten serverumgebungen repräsentativ sein.

Die Optimierung in jeder Richtlinie Power sind Daten, die durch die folgenden fünf Workloads gesteuert:

-   **IIS-Webserver-workload**

    Eine interne Microsoft-Vergleichstest wird aufgerufen, Web-Grundlagen wird verwendet, zur Optimierung der Energieeffizienz von Plattformen, die IIS-Webserver ausführen. Das Setup enthält einen Webserver und mehrere Clients, die die Web Access-Datenverkehr zu simulieren. Die Verteilung von "Dynamic", "Static" heiß "(in-Memory) und statische Cold (Datenträgerzugriff erforderlich) Webseiten basieren auf statistische Untersuchungen der Produktionsserver. Um die CPU-Kerne des Servers auf vollständige Auslastung (ein Ende des Spektrums getestete) zu übertragen, benötigt die Einrichtung schnell genug Netzwerk- und Datenträger.

-   **SQL Server-Datenbank-arbeitsauslastung**

    Die [TPC-E-](http://www.tpc.org/tpce/default.asp) Benchmark ist eine beliebte Benchmark für Datenbank-Leistungsanalyse. Es wird verwendet, um eine OLTP-arbeitsauslastung für die Optimierung PPM-Optimierungen zu generieren. Diese Workload ist erheblich mehr Datenträger-e/a, und daher wurde eine hohe Leistung-Anforderung für die Speichergröße für System- und Arbeitsspeicher.

-   **Dateiserver-arbeitsauslastung**

    Wird aufgerufen, eine Benchmark von Microsoft entwickelt wurden [FSCT](http://www.snia.org/sites/default/files2/sdc_archives/2009_presentations/tuesday/BartoszNyczkowski-JianYan_FileServerCapacityTool.pdf) zum Generieren einer SMB-Dateiserver-arbeitsauslastung verwendet wird. Erstellt eine große Datei auf dem Server festgelegt und viele Clientsysteme (tatsächlichen oder virtualisierten) zum Generieren der Datei öffnen, schließen, Lese- und Schreibvorgänge verwendet. Die Vorgang Mischung basiert auf statistische Untersuchungen der Produktionsserver. Weiterhin wird unterstrichen, CPU-, Datenträger- und Netzwerkressourcen.

-   **SPECpower – JAVA-workload**

    [SPECpower\_ssj2008](http://spec.org/power_ssj2008/) ist der erste SPEC Industriestandard-Benchmark, der Leistungsfähigkeit Merkmale gemeinsam ausgewertet wird. Es ist ein serverseitiges Java-Workload mit unterschiedlichen Ebenen der CPU-Auslastung. Viele Datenträger- oder Netzwerk-Ressourcen muss nicht, aber sie hat bestimmte Anforderungen für die Speicherbandbreite. Fast alle die CPU-Aktivität wird ausgeführt, im Benutzermodus. Kernelmodus-Aktivität muss nicht viel Auswirkungen auf die Benchmarks' Power und Leistungsmerkmale, mit Ausnahme der Entscheidungen für die Verwaltung.

-   **Anwendungsserver-arbeitsauslastung**

    Die [SAP-SD-](http://global.sap.com/campaigns/benchmark/index.epx) Vergleichstest wird verwendet, um eine Anwendungsserver-arbeitsauslastung zu generieren. Ein zwei-Ebenen-Setup wird mit der Datenbank und dem Anwendungsserver, auf dem gleichen Serverhost verwendet. Diese Workload nutzt auch Antwortzeit als eine Leistungsmetrik, die von anderen getesteten Workloads unterscheidet. Daher wird sie verwendet, um die Auswirkungen der PPM-Parameter auf die Reaktionsfähigkeit zu überprüfen. Dennoch soll es nicht repräsentativ für alle produktionsworkloads für die Latenz von Bedeutung sein.

Alle die Benchmarks außer SPECpower wurden ursprünglich entworfen, für die Leistungsanalyse und daher für die Ausführung unter Last spitzenauslastung erstellt wurden. Allerdings Ebenen Medium zu geringer Auslastung, sind häufiger für Server mit der realen Welt und weitere interessante für **ausgeglichen** Planen von Optimierungen. Wir führen absichtlich die Benchmarks mit unterschiedlicher Last von 100 % auf 10 % (in Schritten von 10 %) über die Drosselung Methoden (z. B. durch das Reduzieren der Anzahl von aktiven Clients/Benutzer).

### <a name="hardware-configurations"></a>Hardwarekonfigurationen

Für jede Version von Windows werden die aktuellen Produktionsserver in den Power Plans Analyse und Optimierung verwendet. In einigen Fällen wurden die Tests auf Pre-Production-Systemen ausgeführt, deren releasezeitplan, die die nächste Windows-Version übereinstimmt.

Angesichts der Tatsache, dass die meisten Server mit 1 bis 4 prozessorsockets verkauft werden, und da hochskalieren Server weniger wahrscheinlich Energieeffizienz als eines der Hauptprobleme sind, sind die Power-Plan Optimierung in erster Linie auf Systemen mit 2-Socket und 4-Socket-Tests. Die Menge an Arbeitsspeicher, Datenträger und Netzwerk-Ressourcen für jeden Test werden ausgewählt, um jedes System auszuführende einprozessorenlösungen bis hinauf unter Berücksichtigung die Cost-Einschränkungen, die normalerweise zu echten serverumgebungen, z. B. unter Beibehaltung der vollen Kapazität ermöglichen die Konfigurationen, die sinnvoll.

>[!Important]
> Obwohl das System an die Spitzenlast ausführen kann, in der Regel Optimierung erfolgt für geringer Auslastung, da Server, die konsistent zu ihren Spitzenwert Auslastungsgrad ausgeführt klar empfohlen wäre, mit der **High Performance** Energiesparoption, es sei denn, Energie Effizienz ist eine hohe Priorität.

### <a name="metrics"></a>Metriken

Alle von den getesteten Benchmarks verwenden Durchsatz, als die Leistungsmetrik. Antwortzeit gilt als SLA-Anforderung für diese Workloads (mit Ausnahme von SAP, in denen es sich um eine primäre Metrik ist). Beispielsweise ist eine Benchmark, führen Sie "? gültig Wenn die Mittelwert- oder die maximale Antwortzeit kleiner als bestimmten Wert ist.

Aus diesem Grund verwendet der Optimierungsanalyse auch PPM Durchsatz als Leistungsmetrik.  Auf der höchsten Auslastung-Ebene (100 % der CPU-Auslastung) ist unser Ziel an, dass der Durchsatz mehr als ein paar Prozent aufgrund Power Management Optimierungen nicht verringert werden soll. Aber der wichtigste Aspekt ist, um die Energieeffizienz zu maximieren (wie unten definiert) auf mittlerer und geringer Auslastung.

![Formel für Power-Effizienz](../../media/serverperf-ppm-formula.jpg)

Die CPU-Kerne auf niedrigeren Häufigkeit ausgeführt wird Energieverbrauch reduziert. Niedriger Häufigkeit wird jedoch in der Regel Durchsatz verringern, und der Antwortzeit zu erhöhen. Für die **ausgeglichen** Energiesparplan, besteht eine absichtliche vor-und Nachteile des Reaktionsfähigkeit und Leistung Effizienz. Die SAP-Workload-Tests als auch die Antwortzeit SLAs für andere Workloads, stellen sicher, dass es sich bei der Antwort verlängern Schwellenwert (5 % als Beispiel) für diese speziellen Workloads nicht überschreitet.

>[!Note]
> Wenn die arbeitsauslastung Antwortzeit als die Leistungsmetrik verwendet, sollte das System entweder zum Wechseln der **hohe Leistung** Energiesparplan von Computern oder ändern Sie **ausgeglichen** Energiesparplan, wie im [ Ausgeglichene Power-Plan-Parameter für die schnelle Antwortzeit empfohlen](recommended-balanced-plan-parameters.md).

### <a name="tuning-results"></a>Optimierung der Ergebnisse

Ab Windows Server 2008, hat Microsoft mit Intel und AMD, um die PPM-Parameter für die aktuellen Serverprozessoren für jede Windows-Version zu optimieren. Eine große Anzahl von Seiten pro Minute Parameterkombinationen wurden in jeder der zuvor erläuterten arbeitsauslastungen finden Sie die beste Energieeffizienz auf andere Ebenen getestet. Als Software-Algorithmen wurden optimiert und als Hardware-Power-Architekturen hoch entwickelten, jede neue Windows-Server immer besser hatte oder gleich Energieeffizienz als die früheren Versionen über den Bereich der getesteten Workloads.

Die folgende Abbildung zeigt ein Beispiel der Energieeffizienz unter verschiedenen TPC-E-Auslastungsgrad auf einem 4-Socket-Produktionsserver, der mit Windows Server 2008 R2. Es zeigt eine 8 % Verbesserung im Vergleich zu Windows Server 2008 auf mittlerer Last.

![Vergleich der Power-Effizienz](../../media/serverperf-ppm-figure1.jpg)

## <a name="customized-tuning-suggestions"></a>Angepasste Optimierungsvorschläge

Wenn Ihre primären workloadmerkmale deutlich von den fünf Workloads verwendet werden, für den standardmäßigen unterscheiden **ausgeglichen** Energiesparplan PPM optimieren, Sie können experimentieren, durch Ändern der einem oder mehreren PPM-Parametern finden Sie die beste Lösung für Ihre Umgebung.

Aufgrund der Anzahl und Komplexität der Parameter Dies kann eine Herausforderung sein, aber wenn Sie den besten Kompromiss zwischen Energie Verbrauch und Workload-Effizienz für Ihre jeweilige Umgebung suchen, kann es sein, der Mühe Wert.

 Der vollständige Satz von verschiedene einstellbare PPM-Parameter finden Sie im [Processor Power Management-Optimierung](https://msdn.microsoft.com/windows/hardware/gg566941.aspx). Einige der einfachste Power-Parameter möglicherweise für den Einstieg:

-   **Prozessor Leistungsschwellenwert erhöhen und die Leistung erhöhen Prozessorzeit** – größere Werte langsam die Perf-Antwort auf eine Zunahme der Aktivität

-   **Prozessor-Leistungsschwellenwert verringern** – große Werte beschleunigen, die Power-Antwort, um die Zeiträume im Leerlauf

-   **Verringern der Zeit der Prozessor Leistung** – größere Werte verringern Perf eher allmählich während Leerlaufzeiten

-   **Prozessor-Leistungsrichtlinie Erhöhung** – der "Single? Richtlinie verlangsamt die Perf-Antwort auf zunehmende und nachhaltige Aktivität; die "Rocket? Richtlinie reagiert schnell auf eine Zunahme der Aktivität

-   **Prozessor-Leistungsrichtlinie verringern** – der "Single? Richtlinie verringert die Leistung eher allmählich über mehr Leerlaufzeiten; die "Rocket? Richtlinie löscht Power sehr schnell, wenn Sie eine Zeit im Leerlauf eingeben

>[!Important]
> Vor dem Starten alle Experimente, sollten Sie zuerst Ihre Workloads, verstehen, was das richtige PPM-Parameter aus und verringern den Aufwand, der Optimierung.

### <a name="understand-high-level-performance-and-power-requirements"></a>Allgemeine Leistung und Energieprofil zu verstehen

Wenn Ihre Workload "Echtzeit? (z. B. anfällig für Glitching oder andere durch den Endbenutzer sichtbar wirkt sich auf) oder sind sehr strenge Reaktionsfähigkeit erforderlich (z. B. eine Börsenmakler), und wenn Energieverbrauch keiner primären Kriterien für Ihre Umgebung ist, sollten Sie vielleicht stattdessen die **Hohe Leistung** Energiesparplan. Andernfalls sollten Sie verstehen der Anforderungen an Reaktionen auf-Zeit Ihrer Workloads, und klicken Sie dann optimieren die PPM-Parameter für die beste möglich Energieeffizienz, die immer noch diese Anforderungen erfüllt.

### <a name="understand-underlying-workload-characteristics"></a>Verstehen der zugrunde liegenden Merkmalen der arbeitsauslastung

Sie kennen Ihre Workloads und Entwerfen das Experiment Parametersätze für die Optimierung. Z. B. wenn die Häufigkeit der CPU-Kerne müssen sehr ramped werden erhöhen Fast (vielleicht haben Sie eine bursty arbeitsauslastung mit erheblichen Leerlaufzeiten, aber Sie benötigen sehr schnelle Reaktionsfähigkeit, wenn eine neue Transaktion, die dabei spielt), und klicken Sie dann auf die prozessorleistung Richtlinie Klicken Sie auf "Rocket? festgelegt werden müssen (die, wie der Name schon sagt, Schießen der CPU-Core-Häufigkeit als der maximale Wert, anstatt über eine bestimmte Zeitspanne intensivieren).

Wenn Ihre Workload sehr bursty ist, kann Intervall für die Seiten pro Minute reduziert werden, um die CPU-Frequenz, die schrittweise Ausführung beginnen sich früher nach dem Empfangen eines plötzlichen Ansturms zu machen. Wenn Ihre Workload mit hoher threadparallelität besitzt, und klicken Sie dann das Parken aktiviert werden kann, erzwingen Sie die Workload für eine kleinere Anzahl von Kernen, ausführen, wodurch die potenziell verbessern könnten Cachetreffer Prozessor Verhältnissen.

Wenn Sie nur die CPU-Frequenzen auf mittlerer Auslastung Ebenen (d. h. nicht geringer arbeitsauslastung Ebenen) erhöhen möchten, können Prozessor erhöhen oder verringern, Leistungsschwellenwerte angepasst werden, um nicht zu reagieren, bis bestimmte Verfügbarkeitsstufen für Aktivität festgestellt werden.

### <a name="understand-periodic-behaviors"></a>Verstehen Sie regelmäßige Verhalten

Möglicherweise gibt es verschiedene Anforderungen für Tages- und Nachtzeit oder über das Wochenende oder möglicherweise gibt es verschiedene Workloads, die zu unterschiedlichen Zeiten ausgeführt. In diesem Fall einen Satz von Seiten pro Minute Parameter optimal für alle Zeiträume möglicherweise nicht. Da mehrere Energiesparpläne entworfen werden können, ist es möglich, sogar für verschiedene Zeiträume zu optimieren, und wechseln Sie zwischen Energiesparpläne über Skripts oder anderen Methoden der dynamischen Konfiguration.

In diesem Fall addiert, um die Komplexität des Optimierungsprozesses, daher ist es eine Frage, wie viel Wert aus diese Art der Optimierung, erzielt werden, wird das wahrscheinlich muss wiederholt werden, wenn es signifikante Hardwareupgrades oder Änderungen der arbeitsauslastung.

Aus diesem Grund Windows bietet ist eine **ausgeglichen** – energiesparplanüberwachung im vornherein, da in vielen Fällen es wahrscheinlich nicht den Aufwand der manuellen Optimierung für eine bestimmte Arbeitslast auf einem bestimmten Server Wert ist.

## <a name="see-also"></a>Siehe auch
- [Überlegungen zur Leistung von Server-Hardware](../index.md)
- [Überlegungen zur Power von Server-Hardware](../power.md)
- [Leistung und Leistungsoptimierung](power-performance-tuning.md)
- [Processor Power Management-Optimierung](processor-power-management-tuning.md)
- [Ausgeglichene Parametern empfohlen](recommended-balanced-plan-parameters.md)
