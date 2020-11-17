---
title: Verbesserungen bei der Zeitgenauigkeit für Windows Server 2016
description: Windows Server 2016 hat die Algorithmen verbessert, die verwendet werden, um die Uhrzeit zu korrigieren und die lokale Uhrzeit auf die Synchronisierung mit UTC einzustellen.
author: dahavey
ms.author: dahavey
ms.date: 10/17/2018
ms.topic: article
ms.openlocfilehash: a09022cf1ad2929dfdffa244b86c211970b53aae
ms.sourcegitcommit: a7fb96c0b1d186baeb29349befbbd6bd3b955813
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/11/2020
ms.locfileid: "94522523"
---
# <a name="time-accuracy-improvements-for-windows-server-2016"></a>Verbesserungen bei der Zeitgenauigkeit für Windows Server 2016

Windows Server 2016 hat die Algorithmen verbessert, die verwendet werden, um die Uhrzeit zu korrigieren und die lokale Uhrzeit auf die Synchronisierung mit UTC einzustellen. NTP verwendet vier Werte, um die Zeitdifferenz zu berechnen, basierend auf den Zeitstempeln der Clientanforderung/-antwort und der Serveranforderung/-antwort. Allerdings sind Netzwerke mit Störungen behaftet, und es kann aufgrund von Netzwerküberlastung und anderen Faktoren, die sich auf die Netzwerkwartezeiten auswirken, zu Lastspitzen bei den von NTP eingehenden Daten kommen. Windows 2016-Algorithmen normalisieren diese Störungen auf ein Mittelmaß durch eine Reihe verschiedener Verfahren, die zu einer stabilen und präzisen Uhrzeit führen. Darüber hinaus referenziert die Quelle, die wir für die genaue Zeit verwenden, auf eine verbesserte API, die uns eine bessere Lösung bietet. Mit diesen Verbesserungen können wir eine Genauigkeit von 1 ms in Bezug auf die UTC in einer Domäne erzielen.

## <a name="hyper-v"></a>Hyper-V

Windows 2016 hat den Hyper-V-TimeSync-Dienst verbessert. Zu den Verbesserungen gehören eine genauere Anfangszeit beim Start oder der Wiederherstellung einer VM sowie eine Korrektur der Interruptwartezeit bei Stichproben, die für w32time bereitgestellt werden. Diese Verbesserung ermöglicht es uns, innerhalb von 10 μs des Hosts mit einer Standardabweichung (RMS, Root Mean Squared, ein Indikator für die Varianz) von 50 μs zu bleiben, selbst wenn ein Computer eine Auslastung von 75 % aufweist. Weitere Informationen findest du unter [Hyper-V-Architektur](https://msdn.microsoft.com/library/cc768520.aspx).

> [!NOTE]
> Die Auslastung wurde mit dem prime95-Benchmark mithilfe eines ausgeglichenen Profils erstellt.

Darüber hinaus ist die Stratum-Ebene, die der Host dem Gast meldet, transparenter. Zuvor hätte der Host unabhängig von seiner Genauigkeit ein festes Stratum von 2 angegeben. Mit den Änderungen in Windows Server 2016 meldet der Host ein Stratum, das ein Stratum höher als das des Hosts ist, was zu einer besseren Zeit für virtuelle Gäste führt. Das Stratum des Host wird von w32time mit Bordmitteln bestimmt, basierend auf seiner Quellzeit. Einer Domäne beigetretene Windows 2016-Gäste suchen die genaueste Uhr, anstatt den Host als Standard zu akzeptieren. Genau aus diesem Grund haben wir empfohlen, die Einstellung für den Hyper-V-Zeitanbieter für Computer manuell zu deaktivieren, die Teil einer Domäne in Windows 2012R2 und niedriger sind.

## <a name="monitoring"></a>Überwachung

Leistungsindikatoren wurden hinzugefügt. Diese ermöglichen Ihnen, für die Genauigkeit der Zeit eine Baseline zu entwickeln, sie zu überwachen und Probleme zu behandeln. Zu den Leistungsindikatoren gehören:

|Leistungsindikator|Beschreibung|
|----- | ----- |
|Berechnete Zeitdifferenz| Die absolute Zeitdifferenz zwischen Systemuhr und ausgewählter Zeitquelle, wie vom W32Time-Dienst in Mikrosekunden berechnet. Wenn eine neue gültige Stichprobe verfügbar ist, wird die berechnete Zeit anhand der von der Stichprobe angegebenen Zeitdifferenz aktualisiert. Dies entspricht der tatsächlichen Zeitdifferenz der lokalen Uhr. W32Time initiiert die Zeitanpassung anhand dieser Differenz und aktualisiert die berechnete Zeit zwischen Stichproben mit der verbleibenden Zeitdifferenz, die auf die lokale Uhr angewendet werden muss. Durch diesen Leistungsindikator kann die Zeitgenauigkeit mit einem niedrigen Abrufintervall (z. B. 256 Sekunden oder weniger) überwacht werden. Dabei sollte der Leistungsindikatorwert kleiner als der gewünschte Grenzwert für die Zeitgenauigkeit sein.|
|Anpassung der Taktfrequenz| Die Anpassung der absoluten Taktfrequenz, die von W32Time am lokalen System vorgenommen wird (Anzahl pro Milliarde Einheiten). Dieser Leistungsindikator hilft, die von W32Time vorgenommenen Aktionen zu visualisieren.|
|NTP-Roundtripverzögerung| Die aktuelle Roundtripverzögerung des NTP-Clients beim Empfang einer Antwort vom Server in Mikrosekunden. Dies ist die Zeit, die auf dem NTP-Client zwischen der Übertragung einer Anforderung an den NTP-Server und dem Empfang einer gültigen Antwort vom Server verstrichen ist. Mithilfe dieses Leistungsindikators werden die auf dem NTP-Client aufgetretenen Verzögerungen klassifiziert. Längere oder variierende Roundtrips können zu ungenaueren NTP-Zeitberechnungen führen, was sich wiederum auf die Genauigkeit bei der Zeitsynchronisierung durch NTP auswirken kann.|
|Anzahl von Zeitquellen des NTP-Clients| Die aktive Anzahl der NTP-Zeitquellen, die vom NTP-Client verwendet werden. Dies ist die Anzahl aktiver eindeutiger IP-Adressen von Zeitservern, die auf Anforderungen dieses Clients antworten. Die Anzahl kann größer oder kleiner sein als die Anzahl der konfigurierten Peers. Dies richtet sich nach der DNS-Auflösung von Peernamen und der aktuellen Erreichbarkeit.|
|Eingehende Anforderungen des NTP-Servers| Die Anzahl der vom NTP-Server empfangenen Anforderungen (Anforderungen/Sek.).|
|Ausgehende Antworten des NTP-Servers| Die Anzahl der vom NTP-Server beantworteten Anforderungen (Anforderungen/Sek.).|

Die ersten drei Leistungsindikatoren sind für Szenarien zur Behandlung von Problemen mit der Genauigkeit gedacht. Weitere Details hierzu findest du unten im Abschnitt „Problembehandlung von Zeitgenauigkeit und NTP“ unter „Bewährte Methoden“.
Die letzten drei Leistungsindikatoren decken NTP-Serverszenarien ab und sind hilfreich, wenn es um die Ermittlung der Auslastung und das Aufstellen einer Baseline für deine aktuelle Leistung geht.

## <a name="configuration-updates-per-environment"></a>Konfigurationsaktualisierungen nach Umgebung

Im Folgenden werden die Änderungen an der Standardkonfiguration zwischen Windows 2016 und früheren Versionen für jede Rolle beschrieben. Die Einstellungen für Windows Server 2016 und Windows 10 Anniversary Update (Build 14393) sind nun eindeutig, weshalb diese als separate Spalten angezeigt werden.

|Role-Eigenschaft|Einstellung|Windows Server 2016|Windows 10|Windows Server 2012 R2<br>Windows Server 2008 R2<br>Windows 10|
|---|---|---|---|---|
|**Eigenständig/Nano Server**||||
| |Zeitserver|time.windows.com|–|time.windows.com|
| |Abrufhäufigkeit|64 bis 1024 Sekunden|–|Einmal pro Woche|
| |Aktualisierungsrate der Uhr|Einmal pro Sekunde|–|Einmal pro Stunde|
|**Eigenständiger Client**||||
| |*Zeitserver*|–|time.windows.com|time.windows.com|
| |*Abrufhäufigkeit*|–|Einmal pro Tag|Einmal pro Woche|
| |*Aktualisierungsrate der Uhr*|–|Einmal pro Tag|Einmal pro Stunde|
|**Domänencontroller**||||
| |*Zeitserver*|PDC/GTIMESERV|–|PDC/GTIMESERV|
| |*Abrufhäufigkeit*|64 bis 1024 Sekunden|–|1024 bis 32768 Sekunden|
| |*Aktualisierungsrate der Uhr*|Einmal pro Sekunde|–|Einmal pro Stunde|
|**Domänenmitgliedsserver**||||
| |Zeitserver|DC|–|DC|
| |Abrufhäufigkeit|64 bis 1024 Sekunden|–|1024 bis 32768 Sekunden|
| |Aktualisierungsrate der Uhr|Einmal pro Sekunde|–|Einmal alle 5 Minuten|
|**Domänenmitgliedsclient**||||
| |Zeitserver|–|DC|DC|
| |Abrufhäufigkeit|–|1204 bis 32768 Sekunden|1024 bis 32768 Sekunden|
| |Aktualisierungshäufigkeit der Uhr|–|Einmal alle 5 Minuten|Einmal alle 5 Minuten|
|**Hyper-V-Gast**||||
| |Zeitserver|Wählt die beste Option aus, basierend auf dem Stratum des Hosts und des Zeitservers.|Wählt die beste Option aus, basierend auf dem Stratum des Hosts und des Zeitservers.|Standardeinstellung ist Host|
| |Abrufhäufigkeit|Basierend auf der oben genannten Rolle|Basierend auf der oben genannten Rolle|Basierend auf der oben genannten Rolle|
| |Aktualisierungshäufigkeit der Uhr|Basierend auf der oben genannten Rolle|Basierend auf der oben genannten Rolle|Basierend auf der oben genannten Rolle|

>[!NOTE]
>Informationen zu Linux in Hyper-V findest du unten im Abschnitt „Linux die Verwendung der Hyper-V-Hostzeit gestatten“.

## <a name="impact-of-increased-polling-and-clock-update-frequency"></a>Auswirkungen von erhöhter Abruf- und Aktualisierungshäufigkeit der Uhr

Um eine genauere Zeit bereitzustellen, werden die Standardwerte für die Abrufhäufigkeiten und Aktualisierungen der Uhr erhöht, was es uns gestattet, häufiger kleinere Anpassungen vorzunehmen. Dies führt zu erhöhtem UDP/NTP-Datenverkehr. Diese Pakete sind jedoch klein, weshalb dies nur sehr geringe oder gar keine Auswirkungen auf Breitbandverbindungen haben sollte. Der Vorteil besteht jedoch darin, dass die Zeit für eine größere Vielfalt von Hardware und Umgebungen besser sein sollte.

Bei Geräten mit Akku kann das Erhöhen der Abrufhäufigkeit zu Problemen führen. Geräte mit Akku speichern die Zeit nicht, während sie ausgeschaltet sind. Wenn sie wieder eingeschaltet werden, kann es sein, dass die Uhr häufig korrigiert werden muss. Eine Erhöhung der Abfragehäufigkeit führt dazu, dass die Uhr instabil wird und auch mehr Strom verbrauchen könnte. Microsoft empfiehlt, dass du die Standardeinstellungen des Clients nicht änderst.

Auswirkungen auf Domänencontroller sollten minimal sein, selbst wenn man den vervielfachten Effekt durch die erhöhten Aktualisierungen von NTP-Clients in einer AD-Domäne berücksichtigt. NTP weist im Vergleich zu anderen Protokollen einen wesentlich geringeren Ressourcenverbrauch auf und besitzt nur einen geringfügigen Effekt. Es ist wahrscheinlicher, dass du Grenzwerte für andere Domänenfunktionen erreichst, bevor sich die erweiterten Einstellungen für Windows Server 2016 auf dich auswirken können. Active Directory verwendet sicheres NTP, das tendenziell dazu neigt, die Zeit weniger genau zu synchronisieren als Simple NTP, aber wir haben verifiziert, dass es sich bis zu Clients hochskalieren lässt, die zwei Strata vom PDC entfernt sind.

Als konservativen Plan solltest du 100 NTP-Anforderungen pro Sekunde pro Kern reservieren. Beispielsweise solltest du bei einer Domäne, die aus vier DCs mit jeweils 4 Kernen bestehen, in der Lage sein, 1600 NTP-Anforderungen pro Sekunde zu bedienen. Wenn du 10.000 Clients so konfiguriert hast, dass sie alle 64 Sekunden die Zeit synchronisieren, und die Anforderungen im Laufe der Zeit gleichmäßig empfangen werden, wirst du feststellen, dass 10.000/64 Sekunden oder ungefähr 160 Anforderungen/Sekunde auf alle DCs verteilt werden. Dies liegt bequem innerhalb unserer 1600 NTP-Anforderungen/Sek. basierend auf diesem Beispiel. Hierbei handelt es sich um konservative Planungsempfehlungen, die natürlich auch in hohem Maße von deinem Netzwerk, den Prozessorgeschwindigkeiten und Auslastungen abhängig sind. Führe also wie immer in deinen Umgebungen Tests durch und richte eine Baseline ein.

Es ist auch wichtig zu beachten, dass, wenn deine DCs mit einer beträchtlichen CPU-Auslastung von mehr als 40 % laufen, dies mit ziemlicher Sicherheit zu Störungen in den NTP-Antworten führen und die Zeitgenauigkeit in deiner Domäne beeinträchtigen wird. Auch hier musst du in deiner Umgebung Tests durchführen, um die tatsächlichen Ergebnisse zu verstehen.

## <a name="time-accuracy-measurements"></a>Messungen der Zeitgenauigkeit

### <a name="methodology"></a>Methodik

Zum Messen der Zeitgenauigkeit für Windows Server 2016 haben wir eine Vielzahl von Tools, Methoden und Umgebungen verwendet. Du kannst diese Methoden verwenden, um deine Umgebung zu messen und zu optimieren und zu bestimmen, ob die Genauigkeitsergebnisse deinen Anforderungen entsprechen.

Die Quelluhr unserer Domäne bestand aus zwei hochpräzisen NTP-Servern mit GPS-Hardware. Wir haben ferner einen separaten Referenztestcomputer für Messungen verwendet, der ebenfalls über hochpräzise GPS-Hardware von einem anderen Hersteller verfügte. Für einige der Tests benötigst du eine exakte und zuverlässige Uhrenquelle, die zusätzlich zur Uhrenquelle deiner Domäne als Referenz verwendet werden kann.

Wir haben vier verschiedene Methoden verwendet, um die Genauigkeit mit beiden physischen und virtuellen Computern zu messen. Mehrere Methoden boten unabhängige Möglichkeiten zur Validierung der Ergebnisse.

1. Messen der lokalen Uhr, die von w32tm gesteuert wird, gegen unseren Referenztestcomputer, der über separate GPS-Hardware verfügt.

2. Messen von NTP-Pings vom NTP-Server an Clients mittels „stripchart“ von W32tm.

3. Messen von NTP-Pings vom Client an den NTP-Server mittels „stripchart“ von W32tm.

4. Messen von Hyper-V-Ergebnissen vom Host an den Gast mithilfe des Zeitstempelindikators (Time Stamp Counter, TSC). Dieser Leistungsindikator wird von beiden Partitionen und der Systemzeit in beiden Partitionen gemeinsam genutzt. Wir haben die Differenz zwischen der Hostzeit und der Clientzeit auf dem virtuellen Computer berechnet. Dann haben wir die TSC-Uhr verwendet, um die Hostzeit über den Gast zu interpolieren, da die Messungen nicht gleichzeitig stattfinden. Außerdem haben wir die TSC-Uhr verwendet, um Verzögerungen und Wartezeiten in der API auszuklammern.

W32tm ist integriert, aber die anderen Tools, die wir bei unseren Tests verwendet haben, sind für das Microsoft-Repository auf GitHub als Open Source für deine Tests und zu deiner Verwendung verfügbar. Weitere Informationen über die Verwendung der Tools zur Durchführung von Messungen finden Sie unter [Windows Time Calibration Tools Wiki](https://github.com/Microsoft/Windows-Time-Calibration-Tools).

Die unten gezeigten Testergebnisse sind eine Teilmenge der Messungen, die wir in einer der Testumgebungen vorgenommen haben. Sie veranschaulichen die Genauigkeit, die am Anfang der Zeithierarchie aufrechterhalten wird, sowie beim untergeordneten Domänenclient am Ende der Zeithierarchie. Dies wird zur Veranschaulichung mit denselben Computern in einer 2012-basierten Topologie verglichen.

### <a name="topology"></a>Topologie

Zum Vergleich haben wir sowohl eine Windows Server 2012R2- als auch eine Windows Server 2016-basierte Topologie getestet. Beide Topologien bestehen aus zwei physischen Hyper-V-Hostcomputern, die einen Windows Server 2016-Computer referenzieren, auf dem GPS-Uhrenhardware installiert ist. Auf jedem Host werden 3 der Domäne beigetretene Windows-Gäste ausgeführt, die entsprechend der folgenden Topologie angeordnet sind. Die Zeilen stellen die Zeithierarchie sowie das verwendete Protokoll bzw. den Transport dar.

![Windows-Zeitdienst-Topologiediagramm](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology1.png)

![Windows-Zeitdienst-Topologiediagramm](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology2.png)

### <a name="graphical-results-overview"></a>Grafische Übersicht der Ergebnisse

Die beiden folgenden Diagramme stellen die Zeitgenauigkeit für zwei bestimmte Mitglieder in einer Domäne auf der Grundlage der oben dargestellten Topologie dar. Jedes Diagramm zeigt eine Überlagerung der Ergebnisse von Windows Server 2012R2 und von 2016, wodurch sich die Verbesserungen visuell veranschaulichen lassen. Die Genauigkeit wurde auf dem Gastcomputer im Vergleich zum Host gemessen. Die grafischen Daten repräsentieren eine Teilmenge des gesamten Testumfangs, den wir durchgeführt haben, und zeigen die Best-Case- und Worst-Case-Szenarien.

![Windows-Zeitdienst-Topologiediagramm](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology3.png)

### <a name="performance-of-the-root-domain-pdc"></a>Leistung des PDC der Stammdomäne

Der Stamm-PDC wird mit dem Hyper-V-Host (mittels VMIC) synchronisiert, wobei es sich um einen Windows Server 2016 mit GPS-Hardware handelt, die nachweislich genau und stabil ist. Dies ist eine kritische Anforderung für eine Genauigkeit von 1 ms, die als grün schattierter Bereich dargestellt wird.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart1.png)

### <a name="performance-of-the-child-domain-client"></a>Leistung des Clients der untergeordneten Domäne

Der Client der untergeordneten Domäne ist mit einen untergeordneten Domänen-PDC verbunden, der mit dem Stamm-PDC kommuniziert. Seine Zeit liegt auch innerhalb der Anforderung von 1 ms.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart2.png)

### <a name="long-distance-test"></a>Langstreckentest

Im folgenden Diagramm wird 1 virtueller Netzwerk-Hop mit 6 physischen Netzwerk-Hops mit Windows Server 2016 verglichen. Zwei Diagramme sind transparent überlagert, um überlappende Daten darzustellen. Das Erhöhen der Netzwerkhops bedeutet eine höhere Wartezeit und stärkere Zeitabweichungen. Das Diagramm ist vergrößert, sodass die durch den grünen Bereich dargestellten 1-ms-Grenzen größer sind. Wie du sehen kannst, liegt die Zeit bei mehreren Hops immer noch innerhalb von 1 ms. Es ist negativ verschoben, was eine Netzwerkasymmetrie veranschaulicht. Natürlich sind alle Netzwerke anders, und die Messungen hängen von einer Vielzahl von Umgebungsfaktoren ab.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart3.png)

## <a name="best-practices-for-accurate-timekeeping"></a>Bewährte Methoden für exakte Zeitmessungen

### <a name="solid-source-clock"></a>Stabile Quellenuhr

Eine Computerzeit ist nur so gut wie die Quellenuhr, mit der sie synchronisiert wird. Um eine Genauigkeit von 1 ms zu erreichen, benötigst du GPS-Hardware oder ein Zeitgerät in deinem Netzwerk, das du als Masterquellenuhr referenzieren kannst. Wenn du den Standard „time.windows.com“ verwendest, liefert dieser möglicherweise keine stabile und lokale Zeitquelle. Darüber hinaus wirkt sich, je weiter du dich von der Quellenuhr entfernst, das Netzwerk auf die Genauigkeit aus. Für eine optimale Genauigkeit ist es erforderlich, in jedem Rechenzentrum eine Masterquellenuhr zu haben.

### <a name="hardware-gps-options"></a>Hardware-GPS-Optionen

Es gibt verschiedene Hardwarelösungen, die eine genaue Zeit bieten können. Im Allgemeinen basieren Lösungen heute auf GPS-Antennen. Es gibt auch Funk- und DFÜ-Modemlösungen, die dedizierte Leitungen verwenden. Sie werden entweder als Gerät mit deinem Netzwerk verbunden oder an einen PC angeschlossen, z. B. Windows über ein PCIe- oder USB-Gerät. Verschiedene Optionen bieten unterschiedliche Genauigkeitsstufen, und wie immer hängen die Ergebnisse von deiner Umgebung ab. Zu den Variablen, die die Genauigkeit beeinflussen, zählen GPS-Verfügbarkeit, Netzwerkstabilität und -auslastung sowie die PC-Hardware. Dies sind alles wichtige Faktoren bei der Auswahl einer Quellenuhr, die, wie bereits erwähnt, eine Voraussetzung für eine stabile und genaue Zeit ist.

### <a name="domain-and-synchronizing-time"></a>Domäne und Synchronisierung der Zeit

Domänenmitglieder verwenden die Domänenhierarchie, um zu bestimmen, welchen Computer sie als Quelle für die Synchronisierung der Zeit verwenden. Jedes Domänenmitglied findet einen anderen Computer, mit dem es sich synchronisiert, und speichert diesen als Uhrenquelle. Jeder Typ von Domänenmitglied folgt einem anderen Satz von Regeln, um eine Quellenuhr für die Zeitsynchronisierung zu finden. Der PDC im Gesamtstrukturstamm ist die Standarduhrenquelle für alle Domänen. Im Folgenden sind verschiedene Rollen und allgemeine Beschreibungen für die Weise aufgeführt, wie sie eine Quelle finden:

- **Domänencontroller mit PDC-Rolle**: Dieser Computer ist die maßgebliche Zeitquelle für eine Domäne. Er besitzt die präziseste in der Domäne verfügbare Zeit und muss sich mit einem Domänencontroller in der übergeordneten Domäne synchronisieren, außer wenn die GTIMESERV-Rolle aktiviert ist.
- **Jeder andere Domänencontroller**: Dieser Computer fungiert als Zeitquelle für Clients und Mitgliedsserver in der Domäne. Ein DC kann sich mit dem PDC seiner eigenen Domäne oder mit einem beliebigen Domänencontroller in seiner übergeordneten Domäne synchronisieren.
- **Clients/Mitgliedsserver**: Dieser Computer kann sich mit einem beliebigen DC oder PDC seiner eigenen Domäne oder mit einem DC oder PDC in der übergeordneten Domäne synchronisieren.

Abhängig von den verfügbaren Kandidaten wird ein Bewertungssystem verwendet, um die beste Zeitquelle zu ermitteln. Dieses System berücksichtigt die Zuverlässigkeit der Zeitquelle und ihren relativen Standort. Dies geschieht einmalig, wenn der Zeitdienst gestartet wird. Wenn du eine präzisere Kontrolle über die Art der Zeitsynchronisierung benötigst, kannst du gute Zeitserver an bestimmten Standorten oder Redundanz hinzufügen. Weitere Informationen findest du im Abschnitt „Angeben eines lokalen zuverlässigen Zeitdiensts mithilfe von GTIMESERV“.

#### <a name="mixed-os-environments-win2012r2-and-win2008r2"></a>Gemischte Betriebssystemumgebungen (Win2012R2 und Win2008R2)

Zwar ist für optimale Genauigkeit eine reine Windows Server 2016-Domänenumgebung erforderlich, dennoch gibt es aber Vorteile in einer gemischten Umgebung. Von der Bereitstellung von Windows Server 2016 Hyper-V in einer Windows 2012-Domäne profitieren die Gäste aufgrund der oben genannten Verbesserungen, aber nur, wenn es sich bei den Gästen ebenfalls um Windows Server 2016 handelt. Ein Windows Server 2016 PDC kann eine genauere Zeit bereitstellen und ist aufgrund der verbesserten Algorithmen eine stabilere Quelle. Da das Ersetzen deines PDC möglicherweise keine Option ist, kannst du stattdessen einen Windows Server 2016 DC mit der GTIMESERV-Rollengruppe hinzufügen, wobei es sich um ein Upgrade hinsichtlich der Genauigkeit für deine Domäne handeln würde. Ein Windows Server 2016-Domänencontroller kann Downstream-Zeitclients eine bessere Zeit bereitstellen, ist aber nur so gut, wie seine Quell-NTP-Zeit.

Wie oben bereits erwähnt, wurden auch die Abruf- und Aktualisierungshäufigkeiten der Uhr mit Windows Server 2016 geändert. Diese können manuell für deine DCs mit älteren Versionen geändert oder per Gruppenrichtlinie angewendet werden. Obwohl wir diese Konfigurationen noch nicht getestet haben, sollten sie sich in Win2008R2 und Win2012R2 gut verhalten und einige Vorteile bieten.

Altere Versionen als Windows Server 2016 hatten mehrere Probleme beim Aufrechterhalten genauer Zeitmessungen, was dazu führte, dass sich die Systemzeit sofort nach Vornahme einer Anpassung verschob. Aus diesem Grund führt das häufige Abrufen von Zeitstichproben von einer exakten NTP-Quelle und das Konfigurieren der lokalen Uhr mit den Daten zu einer geringeren Abweichung der Systemuhren im Zeitraum zwischen den Stichprobennahmen, was wiederum zu besseren Zeitmessungen bei BS-Vorgängerversionen führt. Die beste beobachtete Genauigkeit lag bei ungefähr 5 ms, wenn ein Windows Server 2012R2-NTP-Client, der mit Einstellungen für hohe Genauigkeit konfiguriert war, seine Zeit von einem präzisen Windows 2016-NTP-Server synchronisierte.

In einigen Szenarien mit Gastdomänencontrollern können Hyper-V-TimeSync-Stichproben die Zeitsynchronisierung der Domänen stören. Dies sollte bei Server 2016-Gästen, die auf Hyper-V-Hosts mit Server 2016 ausgeführt werden, kein Problem mehr sein.

Legen Sie den folgenden Gastregistrierungsschlüssel fest, um zu deaktivieren, dass der Hyper-V-TimeSync-Dienst Stichproben für W32Time bereitstellt: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider
 "Enabled"=dword:00000000`

#### <a name="allowing-linux-to-use-hyper-v-host-time"></a>Linux die Verwendung der Hyper-V-Hostzeit gestatten

Für Linux-Gäste, die in Hyper-V ausgeführt werden, werden Clients in der Regel so konfiguriert, dass sie den NTP-Daemon für die Zeitsynchronisierung mit NTP-Servern verwenden. Wenn die Linux-Distribution das TimeSync-Protokoll, Version 4, unterstützt und auf dem Linux-Gast der TimeSync-Integrationsdienst aktiviert ist, wird er mit der Hostzeit synchronisiert. Dies könnte zu inkonsistenten Zeitmessungen führen, wenn beide Methoden aktiviert sind.

Um exklusiv mit der Hostzeit zu synchronisieren, wird empfohlen, die NTP-Zeitsynchronisierung mit einer der folgenden Optionen zu deaktivieren:

- Deaktivieren aller NTP-Server in der Datei „ntp.conf“ oder

- Deaktivieren des NTP-Daemons

In dieser Konfiguration ist der Zeitserverparameter dieser Host. Seine Abrufhäufigkeit beträgt 5 Sekunden, und die Aktualisierungshäufigkeit der Uhr beträgt ebenfalls 5 Sekunden.

Um ausschließlich über NTP zu synchronisieren, wird empfohlen, den TimeSync-Integrationsdienst auf dem Gast zu deaktivieren.

> [!NOTE]
> Hinweis: Die Unterstützung einer exakten Zeit bei Linux-Gästen erfordert eine Funktion, die nur in den neuesten Linux-Upstreamkernels unterstützt wird und somit noch nicht in allen Linux-Distributionen allgemein verfügbar ist. Details zu unterstützten Distributionen findest du unter [Unterstützte virtuelle Linux- und FreeBSD-Computer für Hyper-V unter Windows](../../virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md).

#### <a name="specify-a-local-reliable-time-service-using-gtimeserv"></a>Angeben eines lokalen zuverlässigen Zeitdiensts mithilfe von GTIMESERV

Du kannst einen oder mehrere Domänencontroller als exakte Quellenuhren angeben, indem du die GTIMESERV-Kennzeichen (guter Zeitserver) verwendest. Beispielsweise können bestimmte Domänencontroller, die mit GPS-Hardware ausgestattet sind, als GTIMESERV gekennzeichnet werden. Dadurch wird sichergestellt, dass deine Domäne eine Uhr basierend auf der GPS-Hardware auf referenziert.

> [!NOTE]
> Weitere Informationen zu Domänenkennzeichen findest du in der [MS-ADTS-Protokolldokumentation](/openspecs/windows_protocols/ms-winerrata/fe563333-6e4f-4198-9bf5-741a523cd0d7).

TIMESERV ist ein weiteres verwandtes Domänendienstekennzeichen, das anzeigt, ob ein Computer zurzeit maßgeblich ist, was sich ändern kann, wenn ein DC die Verbindung verliert. Ein DC in diesem Zustand gibt „Unbekanntes Stratum“ zurück, wenn er über NTP abgefragt wird. Nach mehreren Versuchen protokolliert der Domänencontroller das Systemereignis „Zeitdienstereignis 36“.

Wenn du einen DC als GTIMESERV konfigurieren möchtest, kannst du ihn mithilfe des folgenden Befehls manuell konfigurieren. In diesem Fall verwendet der DC einen anderen Computer (oder mehrere) als Masteruhr. Dabei kann es sich um ein Gerät oder einen dedizierten Computer handeln.

```
w32tm /config /manualpeerlist:"master_clock1,0x8 master_clock2,0x8" /syncfromflags:manual /reliable:yes /update
```

> [!NOTE]
> Weitere Informationen findest du unter [Konfigurieren des Windows-Zeitdiensts](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191(v=ws.10)).

Wenn auf dem DC die GPS-Hardware installiert ist, musst du diese Schritte ausführen, um den NTP-Client zu deaktivieren und den NTP-Server zu aktivieren.

Beginne damit, dass du den NTP-Client deaktivierst und den NTP-Server aktivierst, indem du diese Registrierungsschlüsseländerungen verwendest.

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpClient /v Enabled /t REG_DWORD /d 0 /f

reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpServer /v Enabled /t REG_DWORD /d 1 /f
```

Als Nächstes startest du den Windows-Zeitdienst erneut.

```
net stop w32time && net start w32time
```

Gib zum Schluss an, dass dieser Computer eine zuverlässige Zeitquelle besitzt.

```
w32tm /config /reliable:yes /update
```

Um zu überprüfen, ob die Änderungen ordnungsgemäß durchgeführt wurden, kannst du die folgenden Befehle ausführen, die die unten gezeigten Ergebnisse liefern sollten.

```
w32tm /query /configuration

Value|Expected Setting|
----- | ----- |
AnnounceFlags| 5 (Local)|
NtpServer |(Local)|
DllName |C:\WINDOWS\SYSTEM32\w32time.DLL (Local)|
Enabled |1 (Local)|
NtpClient| (Local)|

w32tm /query /status /verbose

Value| Expected Setting|
----- | ----- |
Stratum| 1 (primary reference - syncd by radio clock)|
ReferenceId| 0x4C4F434C (source name: "LOCAL")|
Source| Local CMOS Clock|
Phase Offset| 0.0000000s|
Server Role| 576 (Reliable Time Service)|
```

#### <a name="windows-server-2016-on-3rd-party-virtual-platforms"></a>Windows Server 2016 auf virtuellen Drittanbieterplattformen

Wenn Windows virtualisiert ist, ist standardmäßig der Hypervisor für die Bereitstellung der Zeit verantwortlich. Der Domäne beigetretene Mitglieder müssen jedoch mit dem Domänencontroller synchronisiert werden, damit Active Directory ordnungsgemäß funktioniert. Es empfiehlt sich, jegliche Zeitvirtualisierung zwischen dem Gast und dem Host von jeglicher Drittanbieterplattform zu deaktivieren.

#### <a name="discovering-the-hierarchy"></a>Ermitteln der Hierarchie

Da die Verkettung der Zeithierarchie mit der Masterzeitquelle in einer Domäne dynamisch ist und ausgehandelt wird, muss du den Status eines bestimmten Computers abfragen, um seine Zeitquelle und die Verkettung mit der Masterquellenuhr zu verstehen. Dies kann bei der Diagnose von Zeitsynchronisierungsprobleme helfen.

Wenn du Probleme mit einem bestimmten Client behandeln möchtest, besteht der erste Schritt darin, seine Zeitquelle zu verstehen, indem du den „w32tm“-Befehl verwendest.

```
w32tm /query /status
```

Die Ergebnisse zeigen unter anderem die Quelle an. Die Quelle zeigt an, mit wem du die Zeit in der Domäne synchronisierst. Dies ist der erste Schritt in der Zeithierarchie dieses Computers.
Verwende als Nächstes den zuvor genannten Quelleneintrag sowie den „/StripChart“-Parameter, um die nächste Zeitquelle in der Kette zu finden.

```
w32tm /stripchart /computer:MySourceEntry /packetinfo /samples:1
```

Ebenfalls nützlich, listet der folgende Befehl alle Domänencontroller auf, die in der angegebenen Domäne gefunden werden können, und gibt ein Ergebnis aus, mit dem du jeden Partner bestimmen kannst. Dieser Befehl umfasst Computer, die manuell konfiguriert wurden.

 w32tm /monitor /domain:my_domain

Mithilfe der Liste kannst du die Ergebnisse durch die Domäne verfolgen und die Hierarchie sowie die Zeitdifferenz bei jedem Schritt verstehen. Indem du den Punkt auffindest, an dem die Zeitdifferenz signifikant schlechter wird, kannst du die Ursache für die fehlerhafte Zeit festmachen. Von dort aus kannst du versuchen, zu verstehen, warum diese Zeit falsch ist, indem du die w32tm-Protokollierung aktivierst.

#### <a name="using-group-policy"></a>Verwenden von Gruppenrichtlinien
Du kannst Gruppenrichtlinien verwenden, um eine strengere Genauigkeit zu erreichen, indem du beispielsweise Clients zur Verwendung bestimmter NTP-Server zuweist oder kontrollierst, wie Vorgängerversions-Betriebssysteme bei der Virtualisierung konfiguriert werden.
Im Folgenden findest du eine Liste möglicher Szenarien und relevanter Gruppenrichtlinieneinstellungen:

**Virtualisierte Domänen**: Zum Steuern virtualisierter Domänencontroller in Windows 2012R2, damit sie ihre Zeit mit ihrer Domäne synchronisieren, anstatt mit dem Hyper-V-Host. Du kannst diesen Registrierungseintrag deaktivieren.  Für den PDC solltest du den Eintrag nicht deaktivieren, da der Hyper-V-Host die stabilste Zeitquelle bereitstellt. Der Registrierungseintrag erfordert, dass du den w32time-Dienst neu startest, nachdem er geändert wurde.

 [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider] "Enabled"=dword:00000000

**Genauigkeitsabhängige Lasten**: Bei Workloads, die von der Genauigkeit der Zeit abhängig sind, kannst du Gruppen von Computern so konfigurieren, dass die NTP-Server und alle verwandten Zeiteinstellungen, z. B. Abruf- und Uhraktualisierungshäufigkeit, festgelegt werden. Dies wird normalerweise von der Domäne gehandhabt, aber um stärkere Kontrolle zu erhalten, könntest du bestimmte Computer festlegen, die direkt auf die Masteruhr verweisen sollen.

Gruppenrichtlinieneinstellung| Neuer Wert|
----- | ----- |
NtpServer| ClockMasterName,0x8|
MinPollInterval| 6 bis 64 Sekunden|
MaxPollInterval| 6|
UpdateInterval| 100 – Einmal pro Sekunde|
EventLogFlags| 3 – Sämtliche spezifische Zeitprotokollierung|

> [!NOTE]
> Die NtpServer- und EventLogFlags-Einstellungen befinden sich unter „System\Windows Time Service\Time Providers“ unter Verwendung der Einstellungen zum Konfigurieren des Windows-NTP-Clients. Die anderen 3 befinden sich unter „System\Windows Time Service“ unter Verwendung der Einstellungen für „Globale Konfiguration“.

**Remote-Genauigkeitsabhängige Lasten Remote**: Für Systeme in verzweigten Domänen wie „Einzelhandel“ oder „Kreditunternehmen“ verwendet Windows die aktuellen Standortinformationen und den Domänencontrollerlocator, um einen lokalen DC zu finden, sofern keine manuelle NTP-Zeitquelle konfiguriert ist. Diese Umgebung erfordert eine Genauigkeit von 1 Sekunde, was die Konvergenz zur richtigen Zeit beschleunigt. Diese Option gestattet dem w32time-Dienst, die Uhr zurückzustellen. Wenn dies akzeptabel ist und deine Anforderungen erfüllt, kannst du die folgende Richtlinie erstellen.  Stelle wie bei jeder Umgebung sicher, dass du das Netzwerk testet und eine Baseline entwickelst.

Gruppenrichtlinieneinstellung| Neuer Wert|
----- | ----- |
MaxAllowedPhaseOffset| 1, wenn länger als eine Sekunde, die Uhr stellen, um die Zeit zu korrigieren.|

Die Einstellung „MaxAllowedPhaseOffset“ befindet sich unter „System\Windows Time Service“ unter Verwendung der Einstellungen für „Globale Konfiguration“.

> [!NOTE]
> Weitere Informationen zu Gruppenrichtlinien und verwandten Einträgen findest du im TechNet-Artikel [Windows-Zeitdiensttools und -einstellungen](windows-time-service-tools-and-settings.md).

## <a name="azure-and-windows-iaas-considerations"></a>IaaS-Überlegungen für Azure und Windows

### <a name="azure-virtual-machine-active-directory-domain-services"></a>Virtueller Azure-Computer: Active Directory-Domänendienste (AD DS)
Wenn die Azure-VM, auf der Active Directory Domain Services ausgeführt wird, Teil einer vorhandenen lokalen Active Directory-Gesamtstruktur ist, sollte TimeSync (VMIC) deaktiviert werden. Auf diese Weise können alle DCs in der Gesamtstruktur, sowohl physische als auch virtuelle, eine einzige Synchronisierungshierarchie verwenden. Informationen findest du im Whitepaper zu bewährten Methoden mit dem Titel [Ausführen von Domänencontrollern in Hyper-V](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd363553(v=ws.10)).

### <a name="azure-virtual-machine-domain-joined-machine"></a>Virtueller Azure-Computer: Einer Domäne beigetretener Computer
Wenn du einen Computer hostest, der einer Domäne einer vorhandenen Active Directory-Gesamtstruktur (virtuell oder physisch) beigetreten ist, besteht die bewährte Methode darin, TimeSync für den Gast zu deaktivieren und sicherzustellen, dass W32Time für die Synchronisierung mit seinem Domänencontroller konfiguriert ist, indem du die Zeit auf „Type=NTP5“ konfigurierst.

### <a name="azure-virtual-machine-standalone-workgroup-machine"></a>Virtueller Azure-Computer: Eigenständiger Arbeitsgruppencomputer
Wenn der virtuelle Azure-Computer keiner Domäne beigetreten und auch kein Domänencontroller ist, wird empfohlen, die Standardzeitkonfiguration beizubehalten und die VM sich mit dem Host synchronisieren zu lassen.

## <a name="windows-application-requiring-accurate-time"></a>Windows-Anwendung, die exakte Zeit erfordert
### <a name="time-stamp-api"></a>Zeitstempel-API
Programme, die hinsichtlich UTC eine höchstmögliche Genauigkeit benötigen, und nicht bezüglich der Zeitspanne, sollten die [GetSystemTimePreciseAsFileTime-API](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getsystemtimepreciseasfiletime) verwenden. Dadurch wird sichergestellt, dass deine Anwendung die Systemzeit abruft, die vom Windows-Zeitdienst abhängig ist.

### <a name="udp-performance"></a>UDP-Leistung
Wenn du über eine Anwendung verfügst, die UDP-Kommunikation für Transaktionen verwendet, und es dabei wichtig ist, die Wartezeit zu minimieren, gibt es einige verwandte Registrierungseinträge, die du verwende kannst, um einen Bereich von Ports zu konfigurieren, der von der Basisfilter-Engine ausgeschlossen wird. Dadurch wird die Wartezeit verbessert und der Durchsatz erhöht. Änderungen an der Registrierung sollten jedoch erfahrenen Administratoren vorbehalten sein. Darüber hinaus schließt diese Problemumgehung Ports vom Schutz durch die Firewall aus. Weitere Informationen findest du weiter unten in der Artikelreferenz.

Für Windows Server 2012 und Windows Server 2008 musst du zuerst einen Hotfix installieren. Informationen findest du in diesem KB-Artikel: [Datagrammverlust beim Ausführen einer Multicastempfänger-Anwendung in Windows 8 und Windows Server 2012](https://support.microsoft.com/kb/2808584)

### <a name="update-network-drivers"></a>Aktualisieren von Netzwerktreibern
Einige Netzwerkhersteller verfügen über Treiberupdates, die die Leistung im Hinblick auf Treiberwartezeiten und Pufferung von UDP-Paketen verbessern. Wende dich an deinen Netzwerkhersteller, um zu ermitteln, ob Updates vorhanden sind, die beim UDP-Durchsatz helfen können.

## <a name="logging-for-auditing-purposes"></a>Protokollierung zu Überwachungszwecken
Zur Einhaltung von Bestimmungen für die Zeitablaufverfolgung kannst du w32tm-Protokolle, Ereignisprotokolle und Systemmonitorinformationen manuell archivieren. Später können die archivierten Informationen verwendet werden, um die Compliance zu einem bestimmten Zeitpunkt in der Vergangenheit nachzuweisen. Die folgenden Faktoren werden verwendet, um die Genauigkeit anzuzeigen.

1. Uhrgenauigkeit mithilfe des Leistungsindikators „Berechnete Zeitdifferenz“. Dadurch wird die Uhr mit der gewünschten Genauigkeit angezeigt.
2. Uhrenquelle durch Suchen nach „Peerantwort von“ in den w32tm-Protokollen.  Im Anschluss an den Meldungstext findest du die IP-Adresse oder VMIC, die die Zeitquelle sowie die nächste in der Kette der Referenzuhren zu validierende beschreibt.
3. Uhrenbedingungsstatus unter Verwendung der w32tm-Protokolle zur Validierung dass „ClockDispl Discipline: \*SKEW\*TIME\*“ auftreten. Dies zeigt an, dass w32tm zu dem Zeitpunkt aktiv ist.

### <a name="event-logging"></a>Ereignisprotokollierung
Um das volle Bild zu erhalten, benötigst du auch Ereignisprotokollinformationen. Durch das Erfassen des Systemereignisprotokolls und Filtern nach „Time-Server“, „Microsoft-Windows-Kernel-Boot“, „Microsoft-Windows-Kernel-General“ kannst du eventuell ermitteln, ob andere Einflüsse vorliegen, die die Zeit geändert haben, z. B. Drittanbieter. Diese Protokolle sind möglicherweise erforderlich, um externe Störungen auszuschließen. Eine Gruppenrichtlinie kann Einfluss darauf haben, welche Ereignisprotokolle in das Protokoll geschrieben werden. Weitere Informationen findest du oben im Abschnitt unter „Verwenden von Gruppenrichtlinien“.

### <a name="w32time-debug-logging"></a><a name="W32Logging"></a>W32time-Protokollierung
Um w32tm zu Überwachungszwecken zu aktivieren, aktiviert der folgende Befehl die Protokollierung, die die regelmäßigen Aktualisierungen der Uhr sowie die Quellenuhr anzeigt. Starte den Dienst neu, um die neue Protokollierung zu aktivieren.

Weitere Informationen findest du unter [Aktivieren der Debugprotokollierung im Windows-Zeitdienst](https://support.microsoft.com/kb/816043).

 w32tm /debug /enable /file:C:\Windows\Temp\w32time-test.log /size:10000000 /entries:0-73,103,107,110

### <a name="performance-monitor"></a>Systemmonitor
Der Windows-Zeitdienst von Windows Server 2016 stellt Leistungsindikatoren zur Verfügung, die zum Erfassen der Protokollierung für die Überwachung verwendet werden können. Sie können lokal oder remote protokolliert werden. Du kannst die Leistungsindikatoren „Computerzeitdifferenz“ und „Roundtripverzögerung“ aufzeichnen.
Wie bei jedem Leistungsindikator kannst du diese remote überwachen und Benachrichtigungen mithilfe von System Center Operations Manager erstellen. So kannst du beispielsweise eine Warnung verwenden, um dich alarmieren zu lassen, wenn die Zeitdifferenz von der gewünschten Genauigkeit abweicht. Das [System Center-Management Pack](https://www.microsoft.com/download/details.aspx?id=44231) enthält weitere Informationen.

### <a name="windows-traceability-example"></a>Beispiel für die Windows-Nachverfolgbarkeit
In w32tm-Protokolldateien solltest du zwei Informationen überprüfen. Die erste ist ein Hinweis darauf, dass die Protokolldatei zurzeit „Uhr festlegen“ aufweist. Dadurch wird nachgewiesen, dass deine Uhr zum strittigen Zeitpunkt vom Windows-Zeitdienst festgelegt wurde.

 151802 20:18:32.9821765s - ClockDispln Discipline: *SKEW* TIME* - PhCRR:223 CR:156250 UI:100 phcT:65 KPhO:14307 151802 20:18:33.9898460s - ClockDispln Discipline: *SKEW* TIME* - PhCRR:1 CR:156250 UI:100 phcT:64 KPhO:41 151802 20:18:44.1090410s - ClockDispln Discipline: *SKEW* TIME* - PhCRR:1 CR:156250 UI:100 phcT:65 KPhO:38

Die Hauptsache ist, dass du Meldungen mit dem Präfix „ClockDispln Discipline“ siehst, was beweist, dass w32time mit deiner Systemuhr interagiert.

Als Nächstes musst du die letzte Meldung im Protokoll vor dem strittigen Zeitpunkt finden, die den Quellcomputer meldet, der zurzeit als Referenzuhr verwendet wird. Dabei kann es sich um eine IP-Adresse, einen Computernamen oder den VMIC-Anbieter handeln, was anzeigt, dass die Synchronisierung mit dem Host für Hyper-V stattfindet. Im folgenden Beispiel wird die IPv4-Adresse „10.197.216.105“ bereitgestellt.

 151802 20:18:54.6531515s - Response from peer 10.197.216.105,0x8 (ntp.m|0x8|0.0.0.0:123->10.197.216.105:123), ofs: +00.0012218s

Nachdem du nun das erste System in der Referenzzeitkette überprüft hast, musst du die Protokolldatei auf die Referenzzeitquelle untersuchen und dieselben Schritte wiederholen. Dies setzt sich so lange fort, bis du zu einer physischen Uhr wie GPS oder einer bekannten Zeitquelle wie NIST gelangst. Wenn es sich bei der Referenzuhr um GPS-Hardware handelt, sind möglicherweise auch Protokolle des Herstellers erforderlich.

## <a name="network-considerations"></a>Überlegungen zum Netzwerk
Die NTP-Protokollalgorithmen sind von der Symmetrie deines Netzwerks abhängig. Wenn du die Anzahl der Netzwerkhops erhöhst, steigt die Wahrscheinlichkeit für eine Asymmetrie. Daher ist es schwierig, vorherzusagen, welche Arten von Genauigkeiten in deinen spezifischen Umgebungen angezeigt werden.

Die Leistungsüberwachung und die neuen Windows-Zeitleistungsindikatoren in Windows Server 2016 können verwendet werden, um die Genauigkeit deiner Umgebungen zu bewerten und Baselines zu erstellen. Zusätzlich kannst du eine Problembehandlung durchführen, um die aktuelle Differenz aller Computer in deinem Netzwerk zu ermitteln.

Es gibt zwei allgemeine Standards für genaue Zeit über das Netzwerk. PTP ([Precision Time Protocol – IEEE 1588](https://www.nist.gov/el/intelligent-systems-division-73500/introduction-ieee-1588)) enthält strengere Anforderungen an die Netzwerkinfrastruktur, kann aber häufig eine höhere Genauigkeit als Mikrosekunden bereitstellen. NTP ([Network Time Protocol – RFC 1305](https://tools.ietf.org/html/rfc1305)) funktioniert in einer größeren Vielzahl von Netzwerken und Umgebungen, was die Verwaltung erleichtert.

Windows unterstützt für Computer, die keiner Domäne beigetreten sind, standardmäßig Simple NTP (RFC2030). Für Computer, die einer Domäne beigetreten sind, verwenden wir ein sicheres NTP namens [MS-SNTP](/openspecs/windows_protocols/ms-sntp/8106cb73-ab3a-4542-8bc8-784dd32031cc), das von der Domäne aushandelte geheime Schlüssel nutzt, die einen Verwaltungsvorteil gegenüber dem in RFC1305 und RFC5905 beschriebenen authentifizierten NTP bieten.

Sowohl einer Domäne beigetretene als auch nicht beigetretene Protokolle erfordern UDP-Port 123. Weitere Informationen zu den bewährten Methoden für NTP findest du im [Network Time Protocol Best Current Practices IETF Draft](https://tools.ietf.org/html/draft-ietf-ntp-bcp-00).

### <a name="reliable-hardware-clock-rtc"></a>Zuverlässige Hardwareuhr (RTC)

Windows nimmt nur dann eine schrittweise Anpassung der Uhr vor, wenn bestimmte Grenzen überschritten werden, und kontrolliert sonst eher die Uhr. Dies bedeutet, dass w32tm die Aktualisierungshäufigkeit der Uhr in regelmäßigen Abständen mit der Einstellung „Aktualisierungshäufigkeit der Uhr“ anpasst, wofür der Standardwert bei Windows Server 2016 einmal pro Sekunde ist. Wenn die Uhr nachgeht, wird die Häufigkeit erhöht, und wenn sie vorgeht, wird die Häufigkeit verringert. Während der Zeiträume zwischen Anpassungen der Aktualisierungshäufigkeit der Uhr übernimmt die Hardwareuhr die Kontrolle. Wenn ein Problem mit der Firmware oder der Hardwareuhr vorliegt, kann die Zeit auf dem Computer ungenauer werden.

Dies ist ein weiterer Grund, warum du in deiner Umgebung Tests durchführen und Baselines einrichten musst. Wenn sich der Leistungsindikator „Berechnete Zeitdifferenz“ nicht bei der Genauigkeit stabilisiert, die du anstrebst, solltest due überprüfen, ob deine Firmware auf dem neuesten Stand ist. Als weiteren Test kannst du feststellen, ob sich dasselbe Problem auf duplizierter Hardware reproduzieren lässt.

### <a name="troubleshooting-time-accuracy-and-ntp"></a>Problembehandlung von Zeitgenauigkeit und NTP

Du kannst den oben stehenden Abschnitt „Ermitteln der Hierarchie“ verwenden, um die Quelle der ungenauen Zeit herauszufinden. Wenn du dir die Zeitdifferenz ansiehst, finde den Punkt in der Hierarchie, an dem die Zeit am meisten von ihrer NTP-Quelle abweicht. Nachdem du die Hierarchie verstanden hast, solltest du zu verstehen versuchen, warum diese spezielle Zeitquelle keine genaue Zeit erhält.

Wenn du dich auf das System mit der abweichenden Zeit konzentrierst, kannst du mithilfe dieser unten stehenden Tools weitere Informationen sammeln, um das Problem zu bestimmen und eine Lösung zu finden. Die unten stehende „UpstreamClockSource“-Referenz ist die mittels „w32tm /config /status“ ermittelte Uhr.

- Systemereignisprotokolle
- Aktiviere die Protokollierung mittels: w32tm logs - w32tm /debug /enable /file:C:\Windows\Temp\w32time-test.log /size:10000000 /entries:0-300
- w32Time-Registrierungsschlüssel „HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time“
- Lokale Netzwerkablaufverfolgungen
- Leistungsindikatoren (vom lokalen Computer oder der UpstreamClockSource)
- W32tm /stripchart /computer:UpstreamClockSource
- PING UpstreamClockSourc, um die Wartezeit und die Anzahl der Hops zur Quelle zu verstehen
- Tracert UpstreamClockSource

Problem| Symptome| Lösung|
----- | ----- | ----- |
| Die lokale TSC-Uhr ist nicht stabil.| Verwenden von Perfmon – Physischer Computer – Synchronisierungsuhr, stabile Uhr, doch dies tritt weiterhin alle 1 bis 2 Minuten von mehreren 100 µs auf. | Aktualisiere die Firmware, oder überprüfe, ob dasselbe Problem mit anderer Hardware vielleicht nicht auftritt.|
| Netzwerklatenz| „w32tm /stripchart“ zeigt eine RoundTripDelay von mehr als 10 ms an. Schwankungen bei der Verzögerung führen zu Störungen in einer Größenordnung von der Hälfte der Roundtripzeit, beispielsweise eine Verzögerung, die nur in eine Richtung wirksam ist.<br><br>UpstreamClockSource ist mehrere Hops, wie von PING angegeben. TTL sollte nahe bei 128 liegen.<br><br>Verwende Tracert, um die Wartezeit bei jedem Hop zu ermitteln.  | Suche eine näher liegende Uhrenquelle für die Zeit. Eine Lösung besteht darin, eine Quellenuhr im selben Segment zu installieren oder die geografisch näher liegende Quellenuhr manuell zu referenzieren. Füge in einem Domänenszenario einen Computer mit der GTimeServ-Rolle hinzu. |
Die NTP-Quelle kann nicht zuverlässig erreicht werden.| „W32tm /stripchart“ gibt zeitweise „Timeout bei Anforderung“ zurück. |NTP-Quelle reagiert nicht.|
NTP-Quelle reagiert nicht.| Überprüfe die Perfmon-Leistungsindikatoren „Anzahl von Zeitquellen des NTP-Clients“, „Eingehende NTP-Serveranforderungen“, „Ausgehende NTP-Serverantworten“, und bestimme deine Verwendung im Vergleich zu deinen Baselines.| Bestimme mithilfe von Serverleistungsindikatoren, ob sich die Last in Bezug auf deine Baselines geändert hat.<br><br>Liegen Netzwerküberlastungsprobleme vor?|
Der Domänencontroller verwendet nicht die genaueste Uhr.| Änderungen in der Topologie oder kürzlich hinzugefügte Masterzeituhr.| w32tm /resync /rediscover|
Clientuhren weisen Abweichungen auf.| Das „Zeitdienstereignis 36“ im Systemereignisprotokoll und/oder Text in der Protokolldatei, der Folgendes beschreibt: Der Indikator „Anzahl von Zeitquellen des NTP-Clients“ wechselt von 1 zu 0.|Behandle Probleme der Upstreamquelle, und finde heraus, ob dort Leistungsprobleme auftreten.|

### <a name="baselining-time"></a>Einrichten von Baselines für die Zeit

„Baselining“ ist wichtig, damit du zunächst die Leistung und Genauigkeit deines Netzwerks verstehen und in Zukunft bei Auftreten von Problemen mit der Baseline vergleichen kannst. Du solltest Baselines für den Stamm-PDC oder alle mit GTIMESRV markierten Computer einrichten. Außerdem empfiehlt es sich, für den PDC in jeder Gesamtstruktur Baselines zu entwickeln. Wähle schließlich alle kritischen DCs oder Computer aus, die interessante Merkmale aufweisen, wie z. B. Entfernung oder hohe Auslastung, und erstelle Baselines für sie.

Es ist ferner nützlich, Baselines für Windows Server 2016 im Vergleich zu 2012 R2 einzurichten. Dir steht jedoch nur „w32tm /stripchart“ als Tool zur Verfügung, mit dem du Vergleiche durchführen kannst, da Windows Server 2012R2 keine Leistungsindikatoren aufweist. Du solltest zwei Computer mit denselben Merkmalen auswählen, oder einen Computer upgraden und die Ergebnisse nach dem Upgrade vergleichen. Der Nachtrag zu Windows-Zeitmessungen bietet weitere Informationen zum Ausführen detaillierter Vergleichsmessungen zwischen 2016 und 2012.

Sammle unter Verwendung aller w32time-Leistungsindikatoren mindestens eine Woche lang Daten. Dadurch wird sichergestellt, dass du über eine ausreichend große Referenz verfügst, um die verschiedensten Dinge im Netzwerk im zeitlichen Verlauf berücksichtigen zu können, sowie über genügend Daten einer Ausführung, die die Gewissheit bieten, dass deine Zeitgenauigkeit stabil ist.

### <a name="ntp-server-redundancy"></a>NTP-Serverredundanz

Bei einer manuellen NTP-Serverkonfiguration, die für Computer verwendet wird, die keiner Domäne beigetreten sind, oder für den PDC, ist die Verwendung mehrerer Server eine gute Redundanzmaßnahme hinsichtlich der Verfügbarkeit. Dies kann auch eine bessere Genauigkeit bieten, wenn man davon ausgeht, dass alle Quellen genau und stabil sind. Wenn die Topologie jedoch nicht gut entworfen wurde, oder die Zeitquellen nicht stabil sind, könnte die resultierende Genauigkeit möglicherweise schlechter sein, weshalb Vorsicht geboten ist. Der Grenzwert für unterstützte Zeitserver, die w32Time manuell referenzieren kann, ist 10.

## <a name="leap-seconds"></a>Schaltsekunden

Die Erdumdrehungsdauer schwankt im zeitlichen Verlauf, was von klimatischen und geologischen Ereignissen verursacht wird. In der Regel liegt diese Schwankung bei ungefähr einer Sekunde alle paar Jahre. Immer, wenn die Abweichung gegenüber der Atomuhrzeit zu groß wird, wird eine Korrektur von einer Sekunde (nach oben oder unten) eingefügt, die als Schaltsekunde bezeichnet wird. Dies erfolgt so, dass der Unterschied niemals 0,9 Sekunden überschreitet. Diese Korrektur wird sechs Monate vor der tatsächlichen Korrektur angekündigt. Vor Windows Server 2016 hat der Microsoft-Zeitdienst Schaltsekunden nicht berücksichtigt, sondern hat sich darauf verlassen, dass der externe Zeitdienst dies berücksichtigt. Mit der zunehmenden Zeitgenauigkeit von Windows Server 2016 arbeitet Microsoft an einer geeigneteren Lösung für das Problem der Schaltsekunde.

## <a name="secure-time-seeding"></a>Sicheres Zeitseeding

W32Time in Server 2016 enthält die Funktion für sicheres Zeitseeding. Diese Funktion bestimmt die ungefähre aktuelle Zeit von ausgehenden SSL-Verbindungen. Dieser Zeitwert wird verwendet, um die lokale Systemuhr zu überwachen und grobe Fehler zu korrigieren. Weitere Informationen zu dieser Funktion findest du in [diesem Blogbeitrag](/archive/blogs/w32time/secure-time-seeding-improving-time-keeping-in-windows). Bei Bereitstellungen mit zuverlässigen Zeitquellen und gut überwachten Computern, was eine Überwachung auf Zeitdifferenzen beinhaltet, kannst du dich entscheiden, nicht die Funktion für sicheres Zeitseeding nicht zu verwenden und dich stattdessen auf deine vorhandene Infrastruktur verlassen.

Du kannst die Funktion mit folgenden Schritten deaktivieren:

1. Lege den Wert der Registrierungskonfiguration von UtilizeSSLTimeData auf einem bestimmten Computer auf 0 fest:

    ```
    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\Config /v UtilizeSslTimeData /t REG_DWORD /d 0 /f
    ```

2. Wenn du den Computer aus irgendeinem Grund nicht sofort neu starten kannst, kannst du den W32time-Dienst über die Konfigurationsaktualisierung benachrichtigen. Dadurch wird die Zeitüberwachung und -erzwingung, basierend auf den von SSL-Verbindungen gesammelten Zeitdaten, beendet.

    ```
    W32tm.exe /config /update
    ```

3. Durch einen Neustart des Computers wird die Einstellung sofort wirksam und bewirkt ferner die Beendigung der Erfassung von Zeitdaten von SSL-Verbindungen. Letzteres verursacht nur einen sehr geringen Aufwand und sollte kein Leistungsproblem darstellen.

4. Um diese Einstellung in einer ganzen Domäne anzuwenden, lege den Wert von UtilizeSSLTimeData in der W32time-Gruppenrichtlinieneinstellung auf 0 fest, und veröffentliche diese Einstellung. Wenn die Einstellung von einem Gruppenrichtlinienclient abgerufen wird, wird der W32time-Dienst benachrichtigt, und dieser beendet die Zeitüberwachung und -erzwingung mithilfe von SSL-Zeitdaten. Die Erfassung von SSL-Zeitdaten wird bei jedem Neustart eines Computers beendet. Wenn Ihre Domäne über tragbare schlanke Laptops/Tablets und andere Geräte verfügt, sollten Sie diese Computer von dieser Richtlinienänderung ausschließen. Bei diesen Geräte kommt es letztendlich zu einer Erschöpfung des Akkus, und bei ihnen muss die Funktion für sicheres Zeitseeding ihre Zeit bootstrappen.