---
ms.assetid: 72a90d00-56ee-48a9-9fae-64cbad29556c
title: Windows2016 – genaue Uhrzeit
description: ''
author: shortpatti
ms.author: pashort
manager: brianlic
ms.date: 3/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: f4b61dbf07fbc21820dd7b9326bbc990e4db3602
ms.sourcegitcommit: fb4e2ace2e0a29e0f6b028f1cb945cab6aa6ee2c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="windows-server-2016-accurate-time"></a>Windows Server2016 genaue Uhrzeit

>Gilt für: Windows Server 2016

Synchronisierung zeitgenauigkeit in Windows Server2016 wurde deutlich, Beibehaltung uneingeschränkter NTP-Kompatibilität mit älteren Windows-Versionen verbessert. Unter angemessenen Betriebsbedingungen können Sie verwalten, eine 1 ms Genauigkeit in Bezug auf UTC oder besser für Windows Server2016 und Windows10 Anniversary Update Mitglieder der Domäne.

Windows-Zeitdienst ist eine Komponente, die ein Plug-In-Modell für Client und Server-Synchronisierung Zeitanbieter verwendet wird.  Es gibt zwei integrierten Client-Anbieter für Windows und Drittanbieter-Plug-Ins sind verfügbar. Ein Anbieter verwendet [NTP (RFC 1305)](https://tools.ietf.org/html/rfc1305) oder [MS-NTP](https://msdn.microsoft.com/en-us/library/cc246877.aspx) die lokalen Systemzeit zu einem NTP und/oder MS-NTP-kompatible Referenz-Server zu synchronisieren. Der anderen Anbieter für Hyper-V und virtuellen Maschinen (VM) auf den Hyper-V-Host synchronisiert.  Wenn mehrere Anbieter vorhanden sind, Windows auswählen den besten Anbieter Schicht Ebene zuerst mit gefolgt von Verzögerung, Stamm-Verbreitung und schließlich Zeit Offset.

>[!NOTE]
>Für eine kurze Übersicht über Windows-Zeitdienst, sehen Sie sich diese [grobe Übersicht über Video](https://aka.ms/WS2016TimeVideo).

<!-- Not sure what to do with the following -->
In diesem Thema wird beschrieben, wir... in diesen Themen deren Beziehung genaue Uhrzeit aktivieren: 

- Verbesserungen
- Messungen
- Bewährte Methoden

>[!IMPORTANT]
> Ein Zusatz verwiesen wird, durch den Windows-Zeitdienst ab 2016 genau Artikel heruntergeladen werden [hier](http://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf).  Dieses Dokument enthält ausführliche Informationen zu unseren Tests und Messung Methoden.



> [!NOTE] 
> Das Windows Zeit Anbieter-Plug-In-Modell ist [in TechNet dokumentiert](https://msdn.microsoft.com/en-us/library/windows/desktop/ms725475%28v=vs.85%29.aspx).
<!-- -->





## <a name="domain-hierarchy"></a>Domänenhierarchie
Domänen- und eigenständige funktionieren anders.

- Mitglieder der Domäne verwenden Sie ein sicheres NTP-Protokoll, das Authentifizierung verwendet, um sicherzustellen, dass die Sicherheit und die Authentizität des Zeitreferenz.  Mitglieder der Domäne mit einer master Uhr hängt von der Domänenhierarchie und ein Bewertungssystem synchronisieren.  In einer Domäne besteht eine hierarchische Ebene der Zeit Stratums, wobei jeder Domänencontroller für ein übergeordnetes Element DC mit einer möglichst genauen Zeitpunkt Schicht verweist.  Die Hierarchie wird in der primäre Domänencontroller oder ein Domänencontroller in der Gesamtstruktur Stamm oder eines Domänencontrollers mit dem GTIMESERV Domäne-Kennzeichen, die eine gute Zeitserver für die Domäne bezeichnet.  Weitere Informationen finden Sie unter der [Geben Sie einen lokalen zuverlässige Zeit Dienst mithilfe von GTIMESERV](#GTIMESERV) weiter unten.

- Eigenständige Computer sind time.windows.com verwenden standardmäßig konfiguriert.  Dieser Name wird von Ihrem Internetdienstanbieter aufgelöst, die auf eine von Microsoft stammen Ressource verweisen soll.  Wie alle Remote-Standorten Zeit Verweise, Netzwerkausfälle, kann die Synchronisierung verhindern.  Netzwerkverkehr lädt, und asymmetrische Netzwerkpfade können die Genauigkeit der zeitsynchronisierung reduziert werden.  Sie können nicht bei einer Genauigkeit von 1 ms eine Remote-Zeitquellen abhängen.

Da Hyper-V-Gäste aus mindestens zwei Windows-Zeitdienst-Anbieter verfügen, kann die Host-Zeit und NTP, unterschiedliche Verhaltensweisen mit der Domäne oder eigenständige angezeigt, wenn als Gast ausgeführt.

> [!NOTE] 
> Weitere Informationen über die Domänenhierarchie und Karten finden Sie unter der ["Was ist Windows-Zeitdienst?"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) Blogbeitrag.

> [!NOTE]
> Ist ein Konzept, das in der NTP und die Hyper-V-Anbietern verwendet und der Wert gibt die Uhren Position in der Hierarchie.  Schicht 1 ist für die höchsten Uhr reserviert und Schicht 0 ist für die Hardware als genaue reserviert und hat wenig oder keine Verzögerung zugeordnet.  Schicht 2 wenden Sie sich an Schicht 1-Servern, Schicht 3 auf Schicht 2 und so weiter.  Während eine untere Schicht häufig eine genauere Uhr angegeben wird, ist es möglich, Diskrepanzen zu finden.  Außerdem akzeptiert W32time nur Zeit von Schicht 15 oder unten.  Verwenden Sie zum Anzeigen einer Schicht eines Clients *w32tm /query / Status*.

## <a name="critical-factors-for-accurate-time"></a>Wichtige Faktoren für die genaue Uhrzeit
In jedem Fall für die genaue Uhrzeit gibt es drei wichtige Faktoren:

1. **Solid Quelle Uhr** -Quelle Uhr in die Domäne muss stabil und präzise sein. Dies bedeutet normalerweise ein GPS-Gerät installieren oder verweist auf eine Schicht-1-Quelle, 3 berücksichtigen. Die Analogie wechselt, wenn Sie zwei Boote auf das Wasser, und Sie haben die Höhe einer im Vergleich zu anderen messen möchten, empfiehlt sich die Genauigkeit der Quelle Boat ist sehr stabil und nicht verschieben. Dasselbe gilt für Zeit und ist Ihre Quelle Uhr stabil, klicken Sie dann die gesamte Kette der synchronisierte Uhrzeit ist betroffen und in jeder Phase vergrößert. Es muss auch zugänglich sein, da Unterbrechungen bei der Verbindung die zeitsynchronisierung beeinträchtigt. Und schließlich müssen sie sicher sein. Verwaltet das Mal Verweis nicht richtig ist, oder von einer möglicherweise schädlichen Party betrieben wird, können Sie die Domäne für das zeitbasierte Angriffe verfügbar machen.
2. **Uhr stabil Client** -eine stabile Client Uhren wird sichergestellt, dass die natürliche Bewegung von dem an einschränkbaren ist.  NTP-Server mehrere Beispiele aus möglicherweise mehrere NTP-Server Bedingung und discipline die Uhr des lokalen Computers verwendet.  Ist es die Zeit geändert wird, wird kein Einzelschritt jedoch eher verlangsamt oder beschleunigt die lokalen Uhr, die, dass Sie die genaue Ansatz schnell Zeit und präzise bleiben zwischen NTP-Anforderungen.  Allerdings ist die Computeruhr Client an nicht stabil, klicken Sie dann weitere Fluktuationen zwischen Anpassungen können auftreten, und die Algorithmen, die um die Uhr Bedingung verwendet, nicht korrekt funktionieren.  In einigen Fällen können die Firmware-Updates für die genaue Uhrzeit erforderlich sein.
3. **Symmetrische NTP-Kommunikation** – es ist wichtig, dass die Verbindung für die Kommunikation NTP symmetrisch ist.  NTP verwendet Berechnungen, um die Zeit, die davon ausgehen, dass die Netzwerk-Patch symmetrisch ist anpassen.  Wenn der Pfad der NTP-Paket verwendet auf dem Server einen anderen Zeitraum zurückgeben, wird die Genauigkeit ist betroffen.  Beispielsweise könnte der Pfad ändern, aufgrund von Änderungen der Netzwerktopologie oder Pakete über Geräte, die Geschwindigkeiten der anderen Schnittstelle geleitet wird.


Bei Akkubetrieb Geräten müssen Mobil- und tragbaren, unterschiedliche Strategien berücksichtigt werden.  Gemäß der Empfehlung muss genaue Uhrzeit die Uhr einmal pro Sekunde disziplinierte werden die in der Update-Taktfrequenz entspricht. Diese Einstellungen werden Akku stärker als erwartet ist, und können sich störend auf Modi verfügbar in Windows für diese Geräte Energiesparmodi verbraucht. Akkubetrieb Geräte können auch bestimmte Energiesparmodi, die W32time Möglichkeit, die Uhr discipline und verwalten genaue Uhrzeit stören alle Anwendungen ausgeführt wird, nicht mehr. Darüber hinaus Uhren auf mobilen Geräten sehr genau zunächst möglicherweise nicht.  Umgebungslichtsensor Umweltbedingungen Einfluss auf die Genauigkeit der Uhr und ein mobiles Gerät kann von der Bedingung verschieben, auf die nächste die durch die Funktion der Zeit genau zu beeinträchtigen könnten.  Microsoft empfiehlt daher nicht, dass Sie Akkubetrieb tragbare Geräte mit hoher Genauigkeit Einstellungen einrichten. 

## <a name="why-is-time-important"></a>Warum ist die Uhrzeit wichtig?  


## <a name="windows-server-2016-improvements"></a>Windows Server2016-Verbesserungen
### <a name="windows-time-service-and-ntp"></a>Windows-Zeitdienst und NTP
Windows Server2016 wurde die Algorithmen verbessert so korrigieren Sie Zeit und der lokalen Zeit zum Synchronisieren mit UTC-Bedingung verwendet.  NTP 4 Werte verwendet, um den Zeitversatz zu berechnen basierend auf den Zeitstempel der Anforderung/Antwort-Client und Server Anforderung/Antwort.  Netzwerke sind allerdings lauten, und Spitzen in der Daten von NTP wegen Überlastung des Netzwerks und anderen Faktoren, die sich die Netzwerklatenz auswirken kann.  Windows2016 Algorithmen Durchschnitt dieser Auffälligkeiten mit einer Reihe von Techniken, was zu einer Uhr stabil und präzise führt.  Zusätzlich werden mithilfe der Quelle für die genaue Uhrzeit Verweise eine verbesserte API ermöglicht eine höhere Auflösung.  Diese Verbesserungen erzielen wir 1 ms Genauigkeit 1ms für UTC in einer Domäne.

### <a name="hyper-v"></a>Hyper-V
Windows2016 wurde die Hyper-V-TimeSync Dienst verbessert. Verbesserungen gehören genauer Anfangszeit auf VM-Start oder VM-Wiederherstellung und Interrupt Latenz Korrektur finden Sie Beispiele für w32time bereitgestellt.  Diese Verbesserung ermöglicht uns, innerhalb 10µs des Hosts mit einem RMS (Root bedeuten quadriert, der Abweichung angegeben), bleiben von 50µs, sogar auf einem Computer mit 75% Last.

> [!NOTE]
> Weitere Informationen finden Sie in diesem Artikel auf [Hyper-V-Architektur](https://msdn.microsoft.com/library/cc768520.aspx) Weitere Informationen.

> [!NOTE]
> Laden wurde mithilfe von prime95 Benchmark mit Lastenausgleich Profil erstellt.

Darüber hinaus ist die Schicht-Ebene, die der Host für den Gast meldet transparenter.  Zuvor würde der Host eine feste Schicht 2, unabhängig von der Genauigkeit darstellen.  Mit den Änderungen in Windows Server2016 meldet der Host eine Schicht größer als die Host-Schicht, die beste Zeitpunkt für virtuelle Gäste führt.  Der Host-Schicht wird durch w32time auf normale Weise basierend auf dessen Quellzeit bestimmt.  Mit einer Domäne zugeordnete Windows2016 Gäste findet die genauesten Uhr, anstatt auf den Host durchführen.  Es wurde aus diesem Grund, die wir empfohlene Zeitanbieter Hyper-V-Einstellung für Ihre Teilnahme an einer Domäne in der Windows-2012R2 und unter Computer manuell deaktivieren.

### <a name="monitoring"></a>Überwachung
Leistungsindikatoren wurden hinzugefügt.  Diese können Sie geplante, Überwachung und Problembehandlung zeitgenauigkeit.  Zu diesen Zählern gehören:

Leistungsindikator|Beschreibung|
----- | ----- |
Berechnet Zeitversatz|   Die absolute Zeit zwischen der Systemuhr und die gewählte Zeitquelle versetzt wird, wie vom W32Time-Dienst in Mikrosekunden berechnet. Wenn ein neues gültiges Beispiel verfügbar ist, wird die berechnete Zeit mit der Zeitoffset angegeben im Beispiel aktualisiert. Dies ist die tatsächliche Uhrzeit Offset der lokalen Uhr. W32Time Uhr Korrektur mithilfe dieser Information initiiert und aktualisiert die berechnete Zeit zwischen Beispiele mit den Offset der verbleibenden, der auf die lokale Uhr angewendet werden soll. Uhr Genauigkeit ein wenig Abrufintervall mit dieser Leistungsindikator verfolgt werden (z.B.: 256Sekunden oder weniger), und suchen Sie nach der Zählerwert kleiner als der gewünschte Uhr Genauigkeit Grenzwert.|
Anpassung der Uhr Häufigkeit| Absolute Uhr Häufigkeit Anpassung der auf der lokalen Systemzeit durch W32Time in ppb. Dieser Leistungsindikator können Sie die Aktionen durch W32time visualisieren.|
NTP Übersetzungsdateien Verzögerung|    Aktuelle Roundtrip Verzögerung der NTP-Client eine Antwort vom Server empfangen, in Mikrosekunden aufgetreten sind. Dies ist die Zeit abgelaufen, auf dem Client NTP zwischen eine Anforderung mit dem NTP-Server übertragen und eine gültige Antwort vom Server empfangen. Dieser Leistungsindikator wird die Verzögerungen, den der NTP-Client zu kennzeichnen. Größer oder veränderliche Roundtrips können Störungen NTP Zeit Berechnungen, hinzufügen, die wiederum die Genauigkeit der Synchronisierung über NTP beeinträchtigen können.|
NTP-Client-Quell-Anzahl|    Aktive Anzahl NTP-Zeitquellen von der NTP-Client verwendet wird. Dies ist die Anzahl der aktiven, unterschiedliche IP-Adressen der Zeitserver, die auf diesem Client-Anforderungen reagieren. Diese Zahl kann größer oder kleiner als der konfigurierte Peers, abhängig von DNS-Auflösung Peernamen und aktuelle Reichweite-Möglichkeit sein.|
NTP-Server eingehende Anforderungen|   Anzahl der Anfragen, die vom NTP-Server (Anfragen/s).|
Ausgehende NTP-Serverantworten|  Anzahl der Anfragen von NTP-Server (Antworten/s), die beantwortet wird.|

Die ersten 3 Leistungsindikatoren Ziel Szenarien für die Problembehandlung bei der Genauigkeit.  Die Problembehandlung bei Zeitgenauigkeit und NTP Abschnittunten unter [Best Practices](#BestPractices), hat mehr Detail.
Die letzten 3 Leistungsindikatoren NTP-Server-Szenarien behandelt und sind hilfreich bei bestimmen die Last und Baseline für die Leistung Ihrer aktuellen.

### <a name="configuration-updates-per-environment"></a>Aktualisieren der Konfiguration pro Umgebung
Im folgenden wird beschrieben, die Änderungen in der Standardkonfiguration zwischen Windows2016 und früheren Versionen für jede Rolle.  Die Einstellungen für Windows Server2016 und Windows10 Anniversary Update(Build 14393) sind jetzt eindeutig ist, warum es als separate Spalten angezeigt werden. 

|Rolle|Einstellung|Windows Server 2016|Windows10, Version 1607|Windows Server2012 R2</br>Windows Server2008 R2</br>Windows10|
|---|---|---|---|---|
|**Eigenständige/Nano Server**||||
| |*Zeitserver*|time.windows.com|NA|time.windows.com|
| |*Abrufintervall*|64 - 1024Sekunden|NA|Einmal pro Woche|
| |*Update-Taktfrequenz*|Einmal pro Sekunde|NA|Nach einer Stunde|
|**Eigenständiger Client**||||
| |*Zeitserver*|NA|time.windows.com|time.windows.com|
| |*Abrufintervall*|NA|Einmal pro Tag|Einmal pro Woche|
| |*Update-Taktfrequenz*|NA|Einmal pro Tag|Einmal pro Woche|
|**Domänencontroller**||||
| |*Zeitserver*|PDC/GTIMESERV|NA|PDC/GTIMESERV|
| |*Abrufintervall*|64-1024Sekunden|NA|1024 - 32768Sekunden|
| |*Update-Taktfrequenz*|Einmal pro Tag|NA|Einmal pro Woche|
|**Domänenmitgliedsserver**||||
| |*Zeitserver*|DC|NA|DC|
| |*Abrufintervall*|64-1024Sekunden|NA|1024 - 32768Sekunden|
| |*Update-Taktfrequenz*|Einmal pro Sekunde|NA|Alle 5Minuten|
|**Domain Member Client**||||
| |*Zeitserver*|NA|DC|DC|
| |*Abrufintervall*|NA|1204 - 32768Sekunden|1024 - 32768Sekunden|
| |*Update-Taktfrequenz*|NA|Alle 5Minuten|Alle 5Minuten|
|**Hyper-V-Gastcomputers**||||
| |*Zeitserver*|Wählt die besten basierend auf Schicht von Host und die Uhrzeit Server|Wählt die besten basierend auf Schicht von Host und die Uhrzeit Server|Die Standardeinstellung ist Host|
| |*Abrufintervall*|Basierend auf Ihrer Rolle oben|Basierend auf Ihrer Rolle oben|Basierend auf Ihrer Rolle oben|
| |*Update-Taktfrequenz*|Basierend auf Ihrer Rolle oben|Basierend auf Ihrer Rolle oben|Basierend auf Ihrer Rolle oben|

>[!NOTE]
>Linux in Hyper-V, finden Sie unter der [zulassen Linux, Hyper-V-Host verwenden](#AllowingLinux) weiter unten.

### <a name="impact-of-increased-polling-and-clock-update-frequency"></a>Auswirkungen der erhöhtes und Update-Taktfrequenz
Um mehr genaue Uhrzeit bieten die Standardeinstellungen für das Abrufen von Frequenzen und Uhr Updates sind verbessert, die wir häufiger kleine Anpassungen vornehmen können.  Dadurch wird mehr UDP/NTP-Datenverkehr, diese Pakete sind jedoch klein, damit es sollte nur sehr wenig oder gar nicht über eine Breitband-Verbindung. Der Vorteil ist jedoch, die Zeit, wird eine größere Vielfalt von Hardware und Umgebungen eine höhere.

Für Geräte mit Akku gesichert kann das Abrufintervall erhöhen Probleme verursachen.  Batteriegeräte speichern nicht die Zeit während deaktiviert.  Wenn sie fortsetzen, kann es häufig Korrekturen vor, um die Uhr erforderlich.  Erhöhen das Abrufintervall bewirkt, dass die Uhr instabil werden und können auch mehr Energie.  Microsoft empfiehlt, dass die Standardeinstellungen des Clients nicht zu ändern.

Domänencontroller sollten auch mit dem multipliziert Effekt der erhöhte Updates von NTP-Clients in einer AD-Domäne nur minimal beeinträchtigt werden.  NTP verfügt über eine viel kleinere-Ressourcenverbrauch im Vergleich zu anderen Protokolle und einen unbedeutenden Einfluss.  Sie sind eher Grenzwerte für andere Domänenfunktionalität zu erreichen, bevor Sie durch die verbesserte Einstellungen für Windows Server2016 beeinträchtigt wird.  Active Directory verwendet sichere NTP, wodurch Zeit weniger präzise als einfache NTP synchronisieren, aber Sie haben sichergestellt, dass es auf Clients zwei Schicht Weg der PDC skaliert werden kann.

Reservieren Sie als konservative Plan 100 NTP-Anforderungen pro Sekunde pro Kern.  Beispielsweise sollte eine Domäne bestehend aus 4 Domänencontroller mit 4 Kerne, Sie 1600 NTP-Anforderungen pro Sekunde verarbeiten können.  Wenn Sie 10 KB-Clients so konfiguriert, dass die Synchronisierungszeit 64Sekunden, und die Anforderungen gleichmäßig über eine Zeit empfangen wurden, sehen Sie 10.000/64 oder CA. 160 Anforderungen pro Sekunde, auf allen Domänencontrollern verteilt.  Dies fällt problemlos in unserer 1600 NTP-Anforderungen/s basierend auf diesem Beispiel.  Diese konservative Planen der Empfehlungen sind und natürlich verfügen über eine große Abhängigkeit in Ihrem Netzwerk, Prozessor Geschwindigkeiten und geladen wird, daher wie immer geplanten und Test in Ihrer Umgebung.

Es ist auch wichtig zu beachten, dass Ihre Domänencontroller mit eine beträchtliche CPU-Auslastung, die mehr als 40%, ausgeführt wird, dies wird mit großer Wahrscheinlichkeit Rauschen NTP-Antworten hinzufügen und Einfluss auf Ihre zeitgenauigkeit in Ihrer Domäne.  In diesem Fall müssen Sie in Ihrer Umgebung zu verstehen, die tatsächlichen Ergebnisse zu testen.

## <a name="time-accuracy-measurements"></a>Die Genauigkeit der Messungen Zeit
### <a name="methodology"></a>Methodik
Um die zeitgenauigkeit für Windows Server2016 zu messen, haben wir eine Vielzahl von Tools, Methoden und Umgebungen verwendet werden.  Diese Verfahren können Sie messen und optimieren Ihre Umgebung und bestimmen, ob die Genauigkeit der Ergebnisse Ihren Anforderungen entsprechen. 

Unsere Domäne Quelle Uhr Bestand aus zwei NTP-Server mit hoher Genauigkeit mit GPS-Hardware.  Wir verwendet auch einen separaten Verweis Testcomputer für Messungen, die auch eine hohe Genauigkeit GPS-Hardware, die von einem anderen Hersteller installiert wurde.  Für einige der Tests benötigen Sie eine genaue und zuverlässige Taktquelle als Referenz zusätzlich zu Ihrer Domäne Uhr Quelle verwenden.

Vier verschiedene Methoden verwendet zum Messen der Genauigkeit mit physischen und virtuellen Maschinen. Mehrere Methoden bereitgestellt, unabhängige bedeutet, dass die Ergebnisse überprüfen.


1. Messen Sie die lokale Uhr, die durch w32tm lagern ist, gegen unsere Verweis Testcomputer mit separaten GPS-Hardware.  
2.  Measure NTP-Pings vom NTP-Server von Clients mittels W32tm "Stripchart"
3.  Measure NTP-Pings vom Client mit dem NTP-Server mit W32tm "Stripchart"
4.  Measure Hyper-V ergibt sich aus dem Host, Gast mithilfe der Zeit Zeitstempel Leistungsindikator (TSC).  Dieser Leistungsindikator Partitionen und die Systemzeit in beiden Partitionen gemeinsam verwendet.  Den Unterschied von dem Host und der Client in der virtuellen Maschine berechnet.  Anschließend wir die Uhr TSC zum Interpolieren der Host-Zeit vom Gast verwenden, da die Messungen zur gleichen Zeit auftreten nicht.  Darüber hinaus verwenden wir die TSV Uhr Faktor Verzögerungen und Latenz in der API.

W32tm ist integriert, aber die anderen Tools, mit denen wir bei unseren Tests sind als open-Source für das Testen und die Nutzung für das Microsoft-Repository auf GitHub verfügbar.  Im WIKI im Repository enthält weitere Informationen, die beschreibt, wie Sie die Tools verwenden, um die Messungen führen.

> [https://github.com/Microsoft/Windows-Time-Calibration-Tools](https://github.com/Microsoft/Windows-Time-Calibration-Tools)

Die nachfolgend aufgeführten Testergebnisse sind eine Teilmenge der Messungen, die wir in einem von der Testumgebungen vorgenommen haben.  Sie erläutern die Genauigkeit, die am Anfang der Zeithierarchie und der untergeordneten Domänenclient am Ende der Zeithierarchie beibehalten.  Dies wird mit den gleichen Computern in einer Topologie 2012-basierte zum Vergleich verglichen.

### <a name="topology"></a>Topologie
Zum Vergleich haben wir einen Windows Server-2012R2 und die Windows Server2016-basierte Topologie getestet.  Beide Topologien bestehen aus zwei physischen Hyper-V-Hostcomputer, die auf einen Windows Server2016-Computer mit GPS-Uhr Hardwarekomponenten verweisen.  Jeder Host führt 3 Domäne Windows-Gäste, die gemäß der folgenden Topologie angeordnet sind.  Die Zeilen stehen für die Zeithierarchie und Protokoll/Transport verwendet wird.

![Windows-Zeitdienst](media/Windows-2016-Accurate-Time/topology1.png)

![Windows-Zeitdienst](media/Windows-2016-Accurate-Time/topology2.png)

### <a name="graphical-results-overview"></a>Ergebnisse (Übersicht)
Die folgenden zwei Diagramme stellen die zeitgenauigkeit für zwei bestimmte Elemente in einer Domäne, die basierend auf der oben genannten Topologie dar.  Jedes Diagramm zeigt Windows Server-2012R2 und 2016 überlagert, Ergebnisse an die Verbesserungen visuell veranschaulicht.  Die Genauigkeit wurde dem Gastcomputer im Vergleich zu dem Host, in mit-messen.  Die Daten grafischen steht für eine Teilmenge der gesamte Satz von Tests, die wir fertig sind und die besten Fall und ungünstigsten Fall.  

![Windows-Zeitdienst](media/Windows-2016-Accurate-Time/topology3.png)

### <a name="performance-of-the-root-domain-pdc"></a>Leistung der PDC-Stammdomäne
Der Stamm-PDC ist auf den Hyper-V-Host (mit VMIC) synchronisiert wird Windows Server2016 mit GPS-Hardware, die nachweislich genauer und stabiler werden.  Dies ist eine wichtige Voraussetzung für die 1 ms Genauigkeit, die als grünen schattierten Bereich angezeigt wird.

![Windows-Zeitdienst](media/Windows-2016-Accurate-Time/chart1.png)

### <a name="performance-of-the-child-domain-client"></a>Leistung des Clients untergeordneten Domäne
Der untergeordneten Domänenclient ist die kommuniziert, zu der PDC Stamm einer untergeordneten Domäne PDC zugeordnet.  Es Zeit ist auch innerhalb der 1 ms-Anforderung.

![Windows-Zeitdienst](media/Windows-2016-Accurate-Time/chart2.png)


### <a name="long-distance-test"></a>Test für große Entfernung
Das folgende Diagramm vergleicht 1 virtuelles Netzwerkhop auf 6 physischen Netzwerkhops mit Windows Server2016.  Zwei Diagramme sind voneinander mit Transparenz überlappende Daten anzeigen überlagert.  Zunehmende Netzwerkhops bedeuten höhere Latenz und größere Zeit Abweichung.  Das Diagramm ist die vergrößerten und so die 1 ms Grenzen, dargestellt durch die grünen Bereich zu groß ist.  Wie Sie sehen können, ist die Zeit noch innerhalb von 1 ms mit mehreren Hops.  Es ist negativ verschoben, die gezeigt ein Netzwerk Asymmetrie.  Natürlich jedes Netzwerk ist anders, und Messungen, die auf einer Vielzahl von Umweltfaktoren abhängig sind.

![Windows-Zeitdienst](media/Windows-2016-Accurate-Time/chart3.png)

## <a name="BestPractices"></a>Bewährte Methoden für die genaue Zeitbestimmung
### <a name="solid-source-clock"></a>Solid Quelle Uhr
Ein Computer dauert nur so gut wie die Quelle Uhr, die mit den synchronisiert.  Zur Erreichung 1 ms Genauigkeit, Sie benötigen GPS-Hardware oder eine Uhrzeit Anwendung in Ihrem Netzwerk, die Sie als die Uhr master Quelle verweisen.  Verwenden den Standardwert von time.windows.com, möglicherweise kein stabil und lokalen Zeitquelle bereit.  Darüber, wie Sie von der Quelle Uhr Weitere, wirkt sich auf das Netzwerk die Genauigkeit.  Mit einer Master-Quelle Uhr in jedes Center für die beste Genauigkeit erforderlich ist.

### <a name="hardware-gps-options"></a>Hardware-GPS-Optionen
Es gibt verschiedene hardwarelösungen, die genaue Uhrzeit anbieten können.  Im Allgemeinen basieren Lösungen heute auf GPS-Antenne.  Es gibt auch Radio und DFÜ-Modem-Lösungen, die mithilfe von dedizierter Zeilen.  Sie fügen mit Ihrem Netzwerk entweder als eine Einheit oder an einen PC, z.B. Windows über ein PCIe oder USB-Gerät anschließen.  Verschiedene Optionen werden verschiedene Ebenen der Genauigkeit bieten, und wie gewohnt Ergebnisse hängen von Ihrer Umgebung.  Variablen, die Genauigkeit beeinflussen enthalten GPS-Verfügbarkeit, Netzwerkstabilität und laden und PC-Hardware.  Diese sind wichtige Faktoren, wenn eine Uhr Quelle wie erwähnt, eine Voraussetzung für die Stabilität und genaue Uhrzeit ist auswählen.

### <a name="domain-and-synchronizing-time"></a>Domäne und die Zeit synchronisieren
Mitglieder der Domäne mithilfe die Domänenhierarchie um zu bestimmen, welche Computer sie als Quelle verwenden, um Zeit zu synchronisieren.  Jedes Mitglied der Domäne findet sich auf einem anderen Computer mit und speichern Sie sie als Uhr Quelle synchronisieren.  Jede Art von Domänenmitglied folgt einen anderen Satz von Regeln, um eine Taktquelle für die zeitsynchronisierung finden.  Der primäre Domänencontroller im Stamm Gesamtstruktur ist die Uhr Standardquelle für alle Domänen.  Unten finden Sie verschiedene Rollen und übergreifende Beschreibung wie sie eine Quelle suchen:


- **Domänencontroller mit der Rolle PDC** – dieser Computer ist die zeitverwaltungsquelle für eine Domäne. Sie müssen in der Domäne möglichst genaue Zeit zur Verfügung und müssen eine Synchronisierung mit einem Domänencontroller in der übergeordneten Domäne, außer in Fällen, in denen [GTIMESERV](#GTIMESERV) -Rolle ist aktiviert. 
- **Alle anderen Domänencontroller** – dieser Computer fungiert als Zeitquelle für Clients und Server in der Domäne. Domänencontroller kann mit dem PDC ihrer eigenen Domäne oder einem beliebigen Domänencontroller in der übergeordneten Domäne synchronisiert werden.
- **Clients/Mitgliedsserver** – dieses Computers mit einem beliebigen Domänencontroller oder PDC ihrer eigenen Domäne oder ein Domänencontroller oder für den primären Domänencontroller in der übergeordneten Domäne synchronisieren kann.

Auf Grundlage der verfügbaren Kandidaten, wird ein Bewertungssystem verwendet, um die beste Zeit Ursache zu ermitteln.  Dieses System berücksichtigt die Zuverlässigkeit der Zeitquelle und die relative Position.  Dies geschieht, wenn die Zeit-Dienst gestartet wird.  Wenn Sie eine genauere Steuerung benötigen des wie Uhrzeit synchronisiert wird, können Sie rechtzeitig Server an bestimmten Speicherorten hinzugefügt oder Redundanz.  Weitere Informationen finden Sie unter der [Geben Sie einen lokalen zuverlässige Zeit Dienst mithilfe von GTIMESERV](#GTIMESERV) Abschnitt, um weitere Informationen.

#### <a name="mixed-os-environments-win2012r2-and-win2008r2"></a>Gemischte OS-Umgebungen (Win2012R2 und Win2008R2)
Eine reine Windows Server2016-Domäne-Umgebung für die beste Genauigkeit erforderlich ist, gibt es jedoch immer noch Vorteile in einer gemischten Umgebung.  Bereitstellen von Windows Server2016 Hyper-V in Windows2012-Domäne profitieren Gäste aufgrund der Verbesserungen, die wir erwähnt, jedoch die Gäste auch Windows Server2016.  Ein Windows Server2016-PDC werden bieten mehr genaue Uhrzeit aufgrund der verbesserten Algorithmen, er kann, eine stabile Quelle.  Als Ersatz für die PDC kann möglicherweise eine Option, können Sie stattdessen einen Windows Server2016-Domänencontroller mit Hinzufügen der [GTIMESERV](#GTIMESERV) Aufnahmen festlegen, die ein Upgrade Genauigkeit für Ihre Domäne.  Ein Windows Server2016-Domänencontroller können beste Zeitpunkt für Downstreamserver zeitclients übermitteln, es ist jedoch nur so gut wie die Quelle NTP-Zeit.

Abrufen und Aktualisieren der Taktfrequenzen wurden geändert, wie bereits erwähnt, auch mit Windows Server2016.  Diese können manuell geändert werden, um die älteren DCs oder über die Gruppenrichtlinie angewendet werden.  Während wir diese Konfigurationen noch nicht getestet, sollten sie auch in Win2008R2 und Win2012R2 Verhalten und bieten einige Vorteile.

Versionen vor Windows Server2016 musste ein mehrere Probleme, halten die genaue Zeit für die führte dazu, dass das System Zeit fliegende sofort, nachdem eine Änderung vorgenommen wurde.  Aus diesem Grund führt häufig Abrufen von Stichproben aus einer genauen NTP-Quelle und Vorbereitung der lokalen Zeit mit den Daten um kleinere Drift in ihrer Systemuhren innerhalb der übermitteln sampling, was eine bessere Zeit auf älteren Betriebssystemversionen. Beobachtete Genauigkeit war ca. 5 ms, wenn Sie einen Windows Server 2012R2 NTP-Client mit den Einstellungen präzise konfiguriert die Zeit von einem genaue Windows2016 NTP-Server synchronisiert.

In einigen Szenarien im Zusammenhang mit Gast-Domänencontroller können Hyper-V-TimeSync Beispiele Domäne Synchronisierung unterbrochen werden.  Dies sollte nicht mehr Problem für Server2016-Gäste auf Server2016 Hyper-V-Hosts ausgeführt werden.

Um den Hyper-V-TimeSync-Dienst von der Bereitstellung von Beispielen w32time zu deaktivieren, legen Sie den folgenden Registrierungsschlüssel für den Gast:

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider 
    "Enabled"=dword:00000000

#### <a name="AllowingLinux"></a>Zulassen von Linux, Hyper-V-Host verwenden
Für Linux-Gäste in Hyper-V ausgeführt wird werden Clients in der Regel die Verwendung den NTP-Daemon für zeitsynchronisierung NTP-Server konfiguriert.  Wenn die Linux-Distribution das Protokoll der Version 4 TimeSync unterstützt und Linux-Gastbetriebssysteme den TimeSync Integrationsdienst aktiviert, wird es mit dem Zeitpunkt der Host synchronisieren. Dies kann zu inkonsistenten Zeit, wenn beide Methoden aktiviert sind führen.

Um ausschließlich mit dem Zeitpunkt der Host zu synchronisieren, empfiehlt es sich zum Deaktivieren der zeitsynchronisierung NTP entweder durch:

- Deaktivieren alle NTP-Server in der Datei ntp.conf
- Oder den NTP-Daemon deaktivieren

In dieser Konfiguration ist der Zeitserver-Parameter dieser Host.  Die Polling Frequency ist 5Sekunden und der Update-Taktfrequenz 5Sekunden.

Um ausschließlich über NTP zu synchronisieren, wird empfohlen, den TimeSync Integration-Dienst auf dem Gast zu deaktivieren.

> [!NOTE]
> Hinweis: Unterstützung für die genaue Uhrzeit mit Linux-Gastbetriebssystemen erfordert ein Feature, das nur in der neuesten upstream Linux-Kernel unterstützt wird, und es ist etwas, das weit verbreitet über alle Linux-Distributionen noch ist nicht. Finden Sie [unterstützt Linux und FreeBSD virtuellen Maschinen für Hyper-V unter Windows](https://technet.microsoft.com/en-us/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows) ausführliche Informationen zum Support Verteilungen.

#### <a name="GTIMESERV"></a>Geben Sie einen lokalen zuverlässigen Zeitdienst mit GTIMESERV
Können Sie einen oder mehrere Domänencontroller als Quelle korrekt Uhren angeben mithilfe der GTIMESERV gute Zeitserver, kennzeichnet.  Beispielsweise können mit GPS-Hardware ausgestattet sind bestimmte Domänencontroller als ein GTIMESERV gekennzeichnet.  Dadurch wird sichergestellt, dass die Domäne eine Uhr, die auf der Grundlage der GPS-Hardware verweist.

> [!NOTE]
> Weitere Informationen zu Domäne Flags finden Sie der [MS-ADTS Protokoll Dokumentation](https://msdn.microsoft.com/library/mt226583.aspx).

TIMESERV ist einem anderen verwandten Domäne Dienste Flag gibt an, ob ein Computer aktuell autorisierend ist, das ändern können, wenn der Domänencontroller die Verbindung unterbrochen.  Ein Domänencontroller in diesem Zustand wird "Unbekannt Schicht" bei der Abfrage über NTP zurückgegeben.  Nach dem Versuch mehrmals, protokolliert der Domänencontroller System Ereignis Zeitdienst Ereignis 36.

Wenn Sie einen Domänencontroller als ein GTIMESERV konfigurieren möchten, kann dies mithilfe des folgenden Befehls manuell konfiguriert werden.  In diesem Fall wird der Domänencontroller einen anderen Computer als die Master-Uhrzeit verwendet.  Dies kann eine Anwendung oder einen dedizierten Computer sein.

    w32tm /config /manualpeerlist:”master_clock1,0x8 master_clock2,0x8” /syncfromflags:manual /reliable:yes /update

> [!NOTE]
> Weitere Informationen finden Sie unter [Konfigurieren der Windows-Zeitdienst](https://technet.microsoft.com/library/cc731191.aspx)

Wenn der Domänencontroller die GPS-Hardware installiert wurde, müssen Sie diese gehen Sie zum Deaktivieren des NTP-Clients und den NTP-Server aktivieren.

Durch das Deaktivieren der NTP-Client starten Sie, und aktivieren Sie verwenden diesen Schlüssel registrierungsänderungen NTP-Server.

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpClient /v Enabled /t REG_DWORD /d 0 /f

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpServer /v Enabled /t REG_DWORD /d 1 /f

Als Nächstes Starten der Windows-Zeitdienst

    net stop w32time && net start w32time

Abschließend geben Sie an, dass dieser Computer mit einer zuverlässigen hat.
   
    w32tm /config /reliable:yes /update

Um zu überprüfen, dass die Änderungen richtig ausgeführt wurden, können Sie die folgenden Befehle ausführen, die die nachfolgend aufgeführten Ergebnisse beeinflussen. 

    w32tm /query /configuration

Wert|Erwartet festlegen|
----- | ----- |
AnnounceFlags|  5 (lokal)|
NtpServer   |(Lokal)|
DLL-Name |C:\WINDOWS\SYSTEM32\w32time.DLL (lokal)|
Aktiviert |1 (lokal)|
NtpClient|  (Lokal)|

    w32tm /query /status /verbose

Wert|  Erwartet festlegen|
----- | ----- |
Schicht|    1 (primäre Referenz - Syncd Radio-Uhr)|
ReferenceId|    0x4C4F434C (Name der Quelle: "LOCAL")|
Quelle| Lokale CMOS-Uhr|
Phase Offset|   0.0000000s|
Server-Rolle|    576 (zuverlässigen Zeitdienst)|

#### <a name="windows-server-2016-on-3rd-party-virtual-platforms"></a>Windows Server 2016 auf 3rd Party virtuelle Plattformen
Windows virtualisiert ist, wird der Hypervisor standardmäßig für die Bereitstellung Zeit.  Jedoch einer Domäne Mitglieder müssen mit dem Domänencontroller in der Reihenfolge für die Active Directory ordnungsgemäß synchronisiert werden.  Es wird empfohlen, Virtualisierung Zeit zwischen dem Gast und Host von 3rd Party virtuelle Plattformen deaktivieren.

#### <a name="discovering-the-hierarchy"></a>Ermittlung der Hierarchie
Da die Kette der Zeithierarchie der Master-Uhrzeit Quelle in einer Domäne dynamisch ist und ausgehandelt, müssen Sie den Status eines bestimmten Computers zu verstehen, dass er Zeitquelle und die Kette der Uhr master Quelle ist abzufragen.  Dies kann helfen, Probleme bei der Synchronisierung von Zeit zu diagnostizieren.

Wenn Sie einen bestimmten Client; beheben möchten der erste Schrittist, dessen Zeitquelle mit diesem Befehl w32tm zu verstehen.

    w32tm /query /status

Die Ergebnisse werden unter anderem Quelle.  Die Quelle Gibt an, mit denen Sie Zeit in der Domäne zu synchronisieren.  Dies ist der erste Schrittdieser Computer Zeit Hierarchie.
Als Nächstes verwenden Sie Eintrag von oben Quelle und den /StripChart Parameter, um die nächsten Zeitquelle finden Sie in der Kette.

    w32tm /stripchart /computer:MySourceEntry /packetinfo /samples:1

Auch hilfreich, der folgende Befehl listet jedem Domänencontroller, um es in der angegebenen Domäne zu finden und druckt Ergebnis, das Sie jeden Partner ermitteln kann.  Mit diesem Befehl werden Computer enthalten, die manuell konfiguriert wurden.
    
    w32tm /monitor /domain:my_domain

Mithilfe der Liste, können Sie verfolgen die Ergebnisse über die Domäne und Verstehen der Hierarchie als auch der Zeitoffset in jedem Schritt.  Suchen Sie den Punkt, in denen das Zeitoffset erheblich schlimmer wird, können Sie im Stammverzeichnis der falsche Uhrzeit festlegen.  Von dort aus können Sie versuchen, zu verstehen, warum diese Zeit falsch ist, durch Aktivieren der [w32tm Protokollierung](#W32Logging). 

#### <a name="using-group-policy"></a>Mithilfe von Gruppenrichtlinien
Gruppenrichtlinien können strengere Genauigkeit, die mit erreichen z.B. Verwendung bestimmter NTP-Server oder Steuerelement wie kompatiblen Betriebssystem konfiguriert sind, wenn virtualisierte Clients zuweisen.  
Im folgenden finden Sie eine Liste der möglichen Szenarien und entsprechenden Gruppenrichtlinien:

**Virtualisierte Domänen** – um virtualisierte Domänencontroller in Windows 2012R2 steuern, sodass sie Zeit mit ihrer Domäne synchronisieren, anstatt mit dem Hyper-V-Host können Sie dieses Registrierungseintrags deaktivieren.   Für den PDC möchten Sie nicht den Eintrag zu deaktivieren, wie Hyper-V-Hosts die stabile Zeitquelle übermittelt werden.  Der Registrierungseintrag erfordert, dass Sie den w32time-Dienst neu starten, nachdem es geändert wurde.

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider]
    "Enabled"=dword:00000000

**Genauigkeit sensible Lasten** – für Zeit Genauigkeit sensible Arbeitslasten, konnte Sie Gruppen von Computern festlegen NTP-Server konfigurieren und alle zugehörigen Uhrzeiteinstellungen, z.B. Abruf und Uhr Häufigkeit aktualisieren.  Dies erfolgt normalerweise von der Domäne, jedoch mehr Kontrolle können Sie bestimmte Computer direkt auf die Master-Uhrzeit Ziel.

Gruppenrichtlinieneinstellung|   Neuer Wert|
----- | ----- |
NtpServer|  ClockMasterName, 0 x 8|
MinPollInterval|    6 – 64Sekunden|
MaxPollInterval|    6|
UpdateInterval| 100 – einmal pro Sekunde|
EventLogFlags|  3 – alle spezielle Anmeldung|

> [!NOTE]
> Die Einstellungen für NtpServer und EventLogFlags befinden sich unter System\Widows Service\Time Zeitanbieter mit den Einstellungen Windows NTP-Client konfigurieren.  Die anderen 3 befinden sich unter Serverbasisbetriebssystem\Windows Zeitdienst mit den Einstellungen für die globale Konfiguration.

**Remote Genauigkeit sensible Lasten Remote** – für Systeme in Filialen Domänen für Einzelhandels-Instanz und die Zahlung einer Industry (PCI), verwendet Windows die aktuellen Standortinformationen und Domänencontrollerlocator Suche nach einem lokalen Domänencontroller, es sei denn, es eine manuelle NTP ist Zeitquelle konfiguriert.  Diese Umgebung erfordert 1Sekunde Genauigkeit, die schneller Konvergenz auf die richtige Uhrzeit verwendet.  Mit dieser Option können den w32time-Dienst für die Uhr rückwärts bewegen.  Wenn dies zulässig ist und Ihre Anforderungen erfüllt, können Sie die folgende Richtlinie erstellen.   Wie bei jeder Umgebung stellt sicher zu Test- und geplante Netzwerk. 

Gruppenrichtlinieneinstellung|   Neuer Wert|
----- | ----- |
Max. zugelassener Phasenoffset|  1, stellen Sie am zweiten, wenn mehr als Uhr zum richtigen Zeitpunkt.|

Die Einstellung Max. zugelassener Phasenoffset befindet sich unter Serverbasisbetriebssystem\Windows Zeitdienst mit den Einstellungen für die globale Konfiguration.

> [!NOTE]
> Weitere Informationen zu Gruppenrichtlinien und verwandten Einträgen finden Sie unter [Windows-Zeitdienst: Tools](windows-time-service-tools-and-settings.md) und Einstellungen Artikel im TechNet.

#### <a name="azure-and-windows-iaas-considerations"></a>Azure und Windows IaaS-Überlegungen

##### <a name="azure-virtual-machine-active-directory-domain-services"></a>Virtuellen Azure-Computer: Active Directory-Domänendienste
Wenn der Azure-VM mit Active Directory-Domänendienste Teil einer vorhandenen lokalen ist sollte Active Directory-Gesamtstruktur, klicken Sie dann TimeSync(VMIC), deaktiviert werden. Dadurch werden alle Domänencontroller in der Gesamtstruktur, die physische und virtuelle, eine einzelne Uhrzeit Sync-Hierarchie verwenden zu können. Weitere Informationen finden Sie in der best Practice-Whitepaper ["ausgeführten Domain Controller in Hyper-V"](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx)

##### <a name="azure-virtual-machine-domain-joined-machine"></a>Virtuellen Azure-Computer: Domäne beigetretenen Computer
Wenn Sie einen Computer die Domäne zu einer vorhandenen Active Directory-Gesamtstruktur beigetreten ist hosten, virtuell oder physisch, wird daher empfohlen TimeSync für den Gast deaktivieren und sicherstellen, W32Time ist so konfiguriert, dass die Synchronisierung mit der Domänencontroller über das Konfigurieren der Zeit für ein = NTP5

##### <a name="azure-virtual-machine-standalone-workgroup-machine"></a>Virtuellen Azure-Computer: Eigenständige-Arbeitsgruppencomputer
Wenn der Azure-VM keiner Domäne Mitglied noch ein Domänencontroller ist, empfiehlt es sich, halten die Standardkonfiguration für die Zeit und die virtuelle Maschine, die Synchronisierung mit dem Host haben.

### <a name="windows-application-requiring-accurate-time"></a>Windows-Anwendung, die erfordern genaue Uhrzeit
#### <a name="time-stamp-api"></a>Zeitstempel API
Programme, die die größte Genauigkeit im Hinblick auf UTC und nicht im Zeitablauf, erfordern verwenden, sollte die [GetSystemTimePreciseAsFileTime API](https://msdn.microsoft.com/library/windows/desktop/Hh706895.aspx).  Dadurch wird sichergestellt, dass die Anwendung Systemzeit, wird die von der Windows-Zeitdienst lagern ist.

#### <a name="udp-performance"></a>UDP-Leistung
Wenn Sie eine Anwendung, verwendet UDP-Kommunikation in der für Transaktionen und es ist wichtig, dass die Wartezeit, minimieren vorhanden sind einige Einträge in der Registrierung können Sie konfigurieren Sie einen Portbereich aus ausgeschlossen werden im Zusammenhang mit die Filter-Engine Base portiert haben.  Dies verbessert die sowohl die Latenz und den Durchsatz erhöhen.  Allerdings sollten Änderungen an der Registrierung auf erfahrene Administratoren beschränkt werden.  Diese Lösung schließt darüber hinaus Ports von der Sicherung durch die Firewall.  Finden Sie im Artikel unten für Weitere Informationen.

Für Windows Server2012 und Windows Server2008 müssen Sie zunächst ein Hotfix installiert werden.  Sie können diesem KB-Artikel verweisen: [datagrammverlust beim Ausführen einer Anwendung Multicast Empfänger in Windows8 und Windows Server2012](https://support.microsoft.com/en-us/kb/2808584)

#### <a name="update-network-drivers"></a>Aktualisieren von Netzwerktreibern
Einige Netzwerk-Anbieter haben Treiberupdates für die Verbesserung der Leistung im Hinblick auf Treiber Latenz und Puffern von UDP-Pakete.  Wenden Sie sich an den Netzwerk-Anbieter, um festzustellen, ob Updates für Hilfe mit UDP-Durchsatz vorhanden sind.

### <a name="logging-for-auditing-purposes"></a>Die Protokollierung für Überwachungszwecke
Um Zeit Tracing Vorschriften zu erfüllen, können Sie w32tm Protokolle, Ereignisprotokolle und Performance Monitor-Informationen manuell archivieren.  Die archivierte Informationen kann später verwendet werden, auf Kompatibilität zu einem bestimmten Zeitpunkt in der Vergangenheit nachzuweisen.  Die folgenden Faktoren werden verwendet, um die Genauigkeit anzugeben.


1. Uhr Genauigkeit, die mit den Leistungsindikator Zeitversatz berechnet.  Hier wird die Uhr in die gewünschte Genauigkeit angezeigt.
2.  Suchen Sie nach "Antwort vom Peer" in den Protokollen w32tm Taktquelle.   Den Meldungstext folgt die IP-Adresse oder VMIC, das beschreibt die Zeitquelle und den Nächsten in der Kette von Verweis Uhren überprüfen.
3.  Uhr Bedingung Status über die Protokolle w32tm überprüft, ob "ClockDispl Disziplin: \*SKEW\*TIME\*" auftreten.  Dies weist darauf hin, dass die w32tm Zeitpunkt aktiv ist.

#### <a name="event-logging"></a>Ereignisprotokollierung
Um die ganze Geschichte erhalten möchten, benötigen Sie außerdem das Ereignisprotokollinformationen.  Erfassen das Systemereignisprotokoll, und Filtern auf Zeitserver, Microsoft-Windows-Kernel-Boot-, Microsoft-Windows-Kernel-Allgemein, Sie möglicherweise ermitteln, ob es gibt andere Aspekte, die die Zeit, z.B. dritte geändert wurden.  Diese Protokolle möglicherweise erforderlich, externe Interferenzen auszuschließen.  Gruppenrichtlinien kann Auswirkungen auf die Ereignisprotokolle in das Ereignisprotokoll geschrieben werden.  Weitere Informationen finden Sie im oben stehenden Abschnittauf mithilfe von Gruppenrichtlinien.

#### <a name="W32Logging"></a>W32Time-Debugprotokollierung
Um w32tm Überwachungszwecken zu aktivieren, aktiviert der folgende Befehl die Protokollierung, der den regelmäßigen Updates der Uhr und gibt an, die Quelle Uhr.  Starten Sie den Dienst, um die neue Protokollierung aktivieren.  

Weitere Informationen finden Sie unter [zum Aktivieren der Debugprotokollierung in der Windows-Zeitdienst](https://support.microsoft.com/en-us/kb/816043).

    w32tm /debug /enable /file:C:\Windows\Temp\w32time-test.log /size:10000000 /entries:0-73,103,107,110

#### <a name="performance-monitor"></a>Systemmonitor
Windows-Zeitdienst für Windows Server2016 verfügbar macht, Leistungsindikatoren, die zum Sammeln der Protokollierung für die Überwachung verwendet werden können.  Diese können lokal oder Remote protokolliert werden.  Sie können die Computer Zeitversatz Roundtrip Verzögerung Indikatoren und aufzeichnen.  
Und wie einen beliebigen Leistungsindikator können Sie Remote zu überwachen und erstellen Sie mithilfe von System Center Operations Manager Warnungen.  Z.B. eine Warnung können Sie Alarm, wenn der Zeitversatz vom die gewünschte Genauigkeit abweicht.  Die [System Center Management Pack](https://social.technet.microsoft.com/wiki/contents/articles/15251.system-center-management-pack-authoring-guide.aspx) finden Sie weitere Informationen.

#### <a name="windows-traceability-example"></a>Windows-Weg-Beispiel
Aus den Protokolldateien w32tm möchten Sie zwei Informationselemente überprüfen.  Die erste ist ein Hinweis, dass die Protokolldatei Bedingung Uhr aktuell ist.  Dies nachweisen, dass die Uhr Umstrittenes Zeitpunkt von den Windows-Zeitdienst lagern wird wurde.

    151802 20:18:32.9821765s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:223 CR:156250 UI:100 phcT:65 KPhO:14307
    151802 20:18:33.9898460s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:64 KPhO:41
    151802 20:18:44.1090410s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:65 KPhO:38

Der wesentliche Punkt liegt darin, dass Nachrichten, die mit dem Präfix ClockDispln Disziplin Nachweis w32time wird mit der Systemuhr interagiert.
 
Als Nächstes müssen Sie den letzten Bericht das Protokoll vor dem Umstrittenes finden Sie in dem Quellcomputer meldet, die derzeit als Referenzuhr verwendet wird.  Dies ist möglicherweise eine IP-Adresse, Computernamen oder der Anbieter VMIC, das angibt, dass es mit dem Hyper-V-Host synchronisiert wird.  Das folgende Beispiel enthält eine IPv4-Adresse des 10.197.216.105.

    151802 20:18:54.6531515s - Response from peer 10.197.216.105,0x8 (ntp.m|0x8|0.0.0.0:123->10.197.216.105:123), ofs: +00.0012218s

Nun, dass Sie das erste System in der Referenz Zeit Kette überprüft haben, müssen Sie untersuchen die Protokolldatei auf dem Referenz-Zeitquelle, und wiederholen die gleichen Schritteaus.  Dies wird fortgesetzt, bis Sie auf eine physische Uhr, z.B. GPS oder eine bekannte Zeitquelle wie NIST zugreifen.  Ist die Verweis Uhr GPS-Hardware, können der hergestellten Protokolle auch erforderlich sein.

### <a name="network-considerations"></a>Netzwerküberlegungen
Die NTP-Protokoll-Algorithmen besitzen eine Abhängigkeit der Symmetrie Ihres Netzwerks.  Wird Sie als Ihre Vergrößern der Anzahl der Netzwerkhops die Wahrscheinlichkeit Asymmetrie erhöht.  Es ist es, schwer vorherzusagen, welche Arten von genauigkeiten zu testen Sie in Ihrer spezifischen Umgebung angezeigt werden. 

Performance Monitor und die neue Windows-Zeitdienst-Leistungsindikatoren in Windows Server2016 können verwendet werden, Ihre Genauigkeit Umgebungen zu bewerten und Erstellen von Basislinien. Darüber hinaus können Sie die Problembehandlung verwendet, um den aktuellen Offset für alle Computer in Ihrem Netzwerk ermitteln ausführen.

Es gibt zwei allgemeine Standards für die genaue Uhrzeit über das Netzwerk.  PTP ([Genauigkeit NTP - IEEE 1588](https://www.nist.gov/el/intelligent-systems-division-73500/introduction-ieee-1588)) hat eine strengere Anforderungen auf die Netzwerkinfrastruktur, aber untergeordnete Mikrosekunden Genauigkeit können oft bereitstellen.  NTP ([Network Time Protocol – RFC 1305](https://tools.ietf.org/html/rfc1305)) kann auf eine größere verschiedene Netzwerke und Umgebungen, dies es einfacher macht zu verwalten. 

Windows unterstützt einfache NTP (RFC2030) in der Standardeinstellung nicht der Domäne verbundenen Computer.  Für der Domäne Computer angehören, verwenden wir eine sichere NTP aufgerufen [MS-SNTP](https://msdn.microsoft.com/en-us/library/cc246877.aspx), die mithilfe von Domäne ausgehandelt Kennwörter verwendet, die eine Verwaltung gegenüber einem authentifizierten NTP in RFC1305 und RFC5905 beschrieben bereitstellen.   

Die Domäne und die nicht der Domäne verbundenen Protokolle ist UDP-Port 123 erforderlich.  Weitere Informationen zu bewährten Methoden für NTP finden Sie unter [Netzwerk Zeit Protokoll besten aktuellen Methoden IETF-Entwurf](https://tools.ietf.org/html/draft-ietf-ntp-bcp-00).

### <a name="reliable-hardware-clock-rtc"></a>Zuverlässige Hardware-Uhr (RTC)
Windows wird nicht SchrittZeit, es sei denn, bestimmte Grenzen überschritten werden, aber stattdessen die Uhr bestraft.  Das bedeutet, dass w32tm in regelmäßigen Abständen, mit der Update-Taktfrequenz festlegen, welche standardmäßig einmal pro Sekunde mit Windows Server2016 wird die Häufigkeit der Uhr angepasst.  Wenn die Uhr hinter befindet, wird beschleunigt, die Häufigkeit und ist er im Voraus, es verlangsamt die Häufigkeit.  Während dieser Zeit zwischen Uhr Häufigkeit Anpassungen ist die Hardware-Uhr Kontrolle.  Liegt ein Problem mit der Firmware oder Hardware-Uhr, können die auf dem Computer weniger präzise dar.

Dies ist ein weiterer Grund, den Sie testen müssen, und geplante in Ihrer Umgebung.  Wenn Sie der Leistungsindikator "Zeitversatz berechnet" nicht mit der Genauigkeit stabilisiert, die Sie verwenden möchten, empfiehlt es sich möglicherweise um sicherzustellen, dass die Firmware auf dem neuesten Stand ist.  Als ein weiterer Test können Sie sehen, ob doppelter Hardware dasselbe Problem ebenfalls auftritt.

### <a name="troubleshooting-time-accuracy-and-ntp"></a>Problembehandlung bei der Zeitgenauigkeit und NTP
Sie können das Ermitteln von der Hierarchie Abschnittoben, um die Quelle der zeiteinstellung zu verstehen.  Betrachten den Offset der, suchen Sie den Punkt in der Hierarchie, in denen Zeit zur optimalen Nutzung der NTP-Quelle gewissen Grad.  Wenn Sie die Hierarchie verstanden haben, sollten Sie testen und zu verstehen, warum die bestimmten Zeitquelle genaue Uhrzeit empfangen.  

Schwerpunkt auf dem System mit dem abweichenden Zeit, können diese folgenden Tools Sie zum Sammeln von Informationen können Sie das Problem ermitteln und eine Lösung finden.  Die folgenden UpstreamClockSource Verweis ist die Uhr ermittelt mithilfe von "w32tm /config /Status".


- System-Ereignisprotokolle
- Die Protokollierung unter: w32tm Protokolle - w32tm /debug /enable /file: C:\Windows\Temp\w32time-Test.log//size: 10000000 /entries: 0 bis 300
- w32Time-Registrierungsschlüssel HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time
- Lokale netzwerkablaufverfolgungen
- Leistungsindikatoren (aus dem lokalen Computer oder der UpstreamClockSource)
- W32tm /stripchart /Computer: UpstreamClockSource
- PING UpstreamClockSource Latenz und Anzahl der Hops Quelle zu verstehen
- Tracert UpstreamClockSource

Problem|    Symptome|   Auflösung|
----- | ----- | ----- |
Lokaler TSC Uhrzeit ist nicht zuverlässig.| Mithilfe von Perfmon - physischen Computer – synchronisieren Uhr stabil Uhr, jedoch weiterhin anzuzeigen, die alle 1 bis 2Minuten von mehreren 100us. |   Firmware zu aktualisieren oder Überprüfen anderer Hardware nicht das gleiche Problem angezeigt.|
Die Netzwerklatenz|    W32tm Stripchart zeigt eine RoundTripDelay von mehr als 10 ms.  Variante in der so groß wie ½ Verzögerung Ursache Störung der Roundtripzeit, z.B. eine Verzögerung, die nur in eine Richtung.</br></br>UpstreamClockSource entspricht, das mehrere Hops PING angegeben.  TTL-Wert sollte in der Nähe 128 sein.</br></br>Verwenden Sie Tracert, um die Wartezeit in jedem Abschnittzu suchen.    | Suchen nach einer näher Uhr Quelle für die Zeit ein.  Eine Lösung besteht darin, eine Quelle Uhr auf dem gleichen Segment zu installieren, oder zeigen Sie manuell auf Quelle Uhr, weit entfernt ist.  Fügen Sie einen Computer mit der Rolle GTimeServ für ein Szenario Domäne hinzu. |  
Kann nicht zuverlässig erreichen, die NTP-Quelle|    W32tm /stripchart zeitweise gibt "Anforderung Timeout"    |NTP-Quelle reagiert.|
NTP-Quelle reagiert.|    Perfmon-Leistungsindikatoren für NTP-Client Quell-Anzahl, NTP-Server eingehende Anforderungen, NTP-Server ausgehende Antworten überprüfen und Ihrer Verwendung im Vergleich zu Ihrer Grundwerte ermitteln.|    Mithilfe von Server-Leistungsindikatoren, bestimmen Sie, ob die Last in Bezug auf Ihre Konfigurationsbasislinien geändert hat.</br></br>Gibt es Netzwerk Überlastung Probleme?|
Domänencontroller, die nicht über die genauesten Uhr|    Änderungen in der Topologie oder vor kurzem master Zeit Uhr.|   w32tm /resync /rediscover|
Client Uhren fliegende sind| Zeitdienst Ereignis 36 im Systemprotokoll der Ereignisanzeige und/oder Text in der Protokolldatei, die beschreiben, die: "NTP-Client Zeit Quelle Count" Leistungsindikator für den Wechsel von 1 auf 0|Problembehandlung bei der upstream-Quelle und verstehen Sie, wenn sie in Leistungsprobleme ausgeführt wird.|

### <a name="baselining-time"></a>Baselining-Zeit
Baselining ist wichtig, damit Sie zuerst, die Leistung und Genauigkeit Ihres Netzwerks verstehen können, und vergleichen Sie mit der Basislinie in der Zukunft beim Auftreten von Problemen.  Möchten Sie Baseline den PDC des Stamms oder alle Computer mit der GTIMESRV gekennzeichnet.  Wir empfehlen Ihnen auch Basislinie der primäre Domänencontroller in jeder Gesamtstruktur.  Abschließend wählen Sie alle kritischen DCs oder Computer, auf denen interessante Eigenschaften, z.B. Abstand oder hoher Auslastung und geplante diese.

Außerdem ist es nützlich zum geplanten Windows Server2016 Vs 2012 R2, jedoch Sie nur w32tm müssen /stripchart als Tool können Sie vergleichen seit Windows Server-2012R2 Leistungsindikatoren aufweist.  Sie sollten zwei Computer mit den gleichen Eigenschaften auswählen oder aktualisieren ein Computers und vergleichen Sie die Ergebnisse nach dem Update.  Der Windows-Zeit-Messungen Zusatz enthält weitere Informationen zur Vorgehensweise finden Sie ausführliche Messungen zwischen 2016 und 2012.

Erfassen Sie Daten mithilfe von der alle w32time Leistungsindikatoren, mindestens eine Woche.  Dadurch wird sichergestellt, dass genügend ein Verweis auf das Konto für die verschiedenen im Laufe der Zeit Netzwerk sowie ausreichende Anzahl von einer Ausführung vertrauen bereit, Ihre zeitgenauigkeit stabil ist.

### <a name="ntp-server-redundancy"></a>Redundanz für NTP-Server
Für manuelle NTP-Server-Konfiguration, die mit keiner Domäne verbundenen Computer oder den primären Domänencontroller verwendet ist mehr als einen Server eine gute Redundanz Measure bei Verfügbarkeit.  Es kann auch eine höhere Genauigkeit, vorausgesetzt, dass die Quellen genauer und stabiler sind erhalten.  Jedoch konnte die Topologie dient nicht gut, oder die Zeitquellen sind nicht stabil, die resultierende Genauigkeit schlimmer sein, daher Vorsicht empfohlen wird.  Der Grenzwert von unterstützten Mal Servern w32time manuell verweisen können ist 10. 

## <a name="leap-seconds"></a>LEAP Sekunden
Die Erde Drehung Zeitraum unterscheidet sich im Laufe der Zeit durch Klima und geologischen Ereignisse verursacht. Die Variante wird in der Regel ca. eine Sekunde alle paar Jahre. Wenn die Abweichung von atomare Zeit zu groß wird, ist eine Korrektur von einer Sekunde (nach oben oder unten) eingefügt, eine aufgerufen. Dies erfolgt in einer Weise, dass die Differenz 0,9Sekunden nicht überschreitet. Diese Korrektur ist sechs Monate vor dem tatsächlichen Korrektur angekündigt. Vor Windows Server2016 der Microsoft-Zeitdienst war nicht bewusst Leap Sekunden, aber auf den externen Zeitdienst für dieses Achten Sie darauf verlassen. Microsoft arbeitet mit der eine erhöhte zeitgenauigkeit von Windows Server2016 auf eine geeignetere Lösung für das Problem Leap Sekunde.

## <a name="secure-time-seeding"></a>Sichern Sie die Zeit Seeding
W32Time in Server2016 enthält den sicheren Zeitpunkt Seeding-Feature. Dieses Feature bestimmt die ungefähre aktuelle Zeit von ausgehenden SSL-Verbindungen.  Dieser Zeitwert dient zum Überwachen der lokalen Systemzeit und grob fahrlässig Fehler korrigieren. Sie weitere Informationen zum Feature in [in diesem Blogbeitrag](https://blogs.msdn.microsoft.com/w32time/2016/09/28/secure-time-seeding-improving-time-keeping-in-windows/).  Bei Bereitstellungen mit einen zuverlässigen Zeitdienst Quellen und gut überwachten Computern, die Überwachung für Zeitoffsets enthalten, dürfen nicht das Secure Zeit Seeding-Feature und stattdessen abhängig von Ihrer vorhandenen Infrastruktur. 

Sie können das Feature mit den folgenden Schrittendeaktivieren:

1.  Setzen Sie den Registrierungswert Konfiguration UtilizeSSLTimeData auf 0 auf einem bestimmten Computer:

    REG HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\Config /v UtilizeSslTimeData /t REG_DWORD /d 0 /f hinzufügen


2.  Wenn Sie den Computer sofort aufgrund aus irgendeinem Grund neu starten nicht möglich, können Sie W32time-Dienst über die Aktualisierung der Konfiguration informieren. Dies beendet die Überwachung der Zeit und Erzwingung Zeitdaten anhand von SSL-Verbindungen gesammelt. 

    W32tm.exe /config /update

3.  Neustart des Computers die Einstellung wird sofort wirksam wird, und auch mehr Zeitdaten von SSL-Verbindungen gesammelt wird.  Das letzte Teil verfügt über einen sehr kleinen Mehraufwand und sollte kein Belang bezogen werden.

4.  Der UtilizeSSLTimeData-Wert im W32time-Gruppenrichtlinieneinstellung auf 0 festgelegt, und veröffentlichen Sie die Einstellung, um diese Einstellung in einer gesamten Domäne anzuwenden.  Wenn die Einstellung durch eine Gruppenrichtlinienclient gewählt wird, W32time-Dienst benachrichtigt, und Zeit Überwachung und Erzwingung mithilfe von SSL-Zeitdaten wird beendet. Die SSL-Zeit-Datensammlung beendet, wenn jeder Computer wird neu gestartet. Verfügt Ihre Domäne tragbaren schlanke Laptops /-Tablets und anderen Geräten, können Sie solche Computer von dieser Richtlinienänderung ausschließen möchten. Diese Geräte werden schließlich Akkuverbrauch konfrontiert und müssen Funktion der sicheren Zeitpunkt Seeding, um Zeit zu starten.














 













 




