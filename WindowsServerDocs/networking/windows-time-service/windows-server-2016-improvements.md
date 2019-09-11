---
title: Windows Server 2016-Verbesserungen
description: Windows Server 2016 hat die verwendeten Algorithmen verbessert, um die Uhrzeit zu korrigieren und die lokale Uhrzeit für die Synchronisierung mit UTC zu verwenden.
author: dcuomo
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 2b8c6148af21e94e4a56661402f36dcb2e636461
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871832"
---
## <a name="windows-server-2016-improvements"></a>Windows Server 2016-Verbesserungen

### <a name="windows-time-service-and-ntp"></a>Windows-Zeit Dienst und NTP
Windows Server 2016 hat die verwendeten Algorithmen verbessert, um die Uhrzeit zu korrigieren und die lokale Uhrzeit für die Synchronisierung mit UTC zu verwenden.  NTP verwendet vier Werte, um den Zeit Offset basierend auf den Zeitstempeln der Client Anforderung/-Antwort und der Server Anforderung/-Antwort zu berechnen.  Allerdings sind Netzwerke nicht verfügbar, und die Daten von NTP können aufgrund von Netzwerk Überlastung und anderen Faktoren, die sich auf die Netzwerk Latenz auswirken, Spitzen haben.  Windows 2016-Algorithmen Durchschnitt dieses Rauschen durch eine Reihe verschiedener Techniken, die zu einer stabilen und präzisen Uhr führen.  Außerdem verweist die Quelle, die wir für die genaue Zeit verwenden, auf eine verbesserte API, die uns eine bessere Lösung bietet.  Mit diesen Verbesserungen können wir eine Genauigkeit von 1 MS in Bezug auf die UTC in einer Domäne erzielen.

### <a name="hyper-v"></a>Hyper-V
Windows 2016 hat den Hyper-V-TimeSync-Dienst verbessert. Zu den Verbesserungen gehören eine genauere anfängliche Zeit beim VM-Start oder eine VM-Wiederherstellung und eine Interruptzeit-Korrektur für die w32time.  Diese Verbesserung ermöglicht es uns, in 10μs des Hosts mit einem RMS (Root Mean squared, was die Varianz anzeigt) von 50 μs, auch auf einem Computer mit einer Auslastung von 75%, zu bleiben. Weitere Informationen finden Sie unter [Hyper-V-Architektur](https://msdn.microsoft.com/library/cc768520.aspx).

> [!NOTE]
> Load wurde mithilfe von prime95 Benchmark mithilfe eines ausgeglichenen Profils erstellt.

Darüber hinaus ist die Stratum-Ebene, die der Host an den Gast meldet, transparenter.  Zuvor würde der Host unabhängig von seiner Genauigkeit eine Fixed-Stratum 2 darstellen.  Mit den Änderungen in Windows Server 2016 meldet der Host einen mehr als den Host-Stratum, was zu einer besseren Zeit für virtuelle Gäste führt.  Die Host-strateration wird von W32Time auf normale Weise basierend auf der Quell Zeit bestimmt.  In die Domäne eingebundener Windows 2016-Gäste finden Sie die genaueste Uhr, anstatt den Host zu überschreiten.  Aus diesem Grund wurde empfohlen, die Einstellung für den Hyper-V-Zeit Anbieter für Computer, die Teil einer Domäne in Windows 2012 2012r2 und niedriger sind, manuell zu deaktivieren.

### <a name="monitoring"></a>Überwachung
Leistungsindikatoren wurden hinzugefügt.  Diese ermöglichen Ihnen die Baseline, Überwachung und Problembehandlung der Zeit Genauigkeit.  Zu diesen Leistungsindikatoren gehören:

Indikator|Beschreibung|
----- | ----- |
Berechneter Zeit Offset|   Der absolute Zeit Offset zwischen der Systemuhr und der ausgewählten Zeit Quelle, wie von W32Time Service in Mikrosekunden berechnet. Wenn ein neues gültiges Beispiel verfügbar ist, wird die berechnete Zeit mit dem Zeit Offset aktualisiert, der im Beispiel angegeben ist. Dies ist der tatsächliche Zeit Offset der lokalen Uhr. W32Time initiiert die Takt Korrektur mithilfe dieses Offsets und aktualisiert die berechnete Zeit zwischen den Stichproben und dem verbleibenden Zeit Offset, das auf die lokale Uhr angewendet werden muss. Die Takt Genauigkeit kann mithilfe dieses Leistungs Zählers mit einem niedrigen Abruf Intervall (z. b. 256 Sekunden oder weniger) nachverfolgt werden, und es wird gesucht, dass der Wert des Leistungs Zählers kleiner als die gewünschte Takt Genauigkeit ist.|
Anpassung der Taktfrequenz| Die absolute Taktfrequenz Anpassung an der lokalen Systemuhr um W32Time in Teilen pro Milliarde. Mithilfe dieses Zählers können Sie die Aktionen visualisieren, die von W32Time ausgeführt werden.|
NTP-Roundtrip-Verzögerung|    Die letzte Roundtrip-Verzögerung wurde vom NTP-Client beim Empfangen einer Antwort vom Server in Mikrosekunden verzeichnet. Dies ist die Zeit, die auf dem NTP-Client zwischen dem übertragen einer Anforderung an den NTP-Server und dem Empfang einer gültigen Antwort vom Server verstrichen ist. Mithilfe dieses Zählers können die Verzögerungen des NTP-Clients charakterisiert werden. Größere oder abweichende Roundtrips können zu NTP-Zeit Berechnungen Rauschen hinzufügen, die sich wiederum auf die Genauigkeit der Zeitsynchronisierung über NTP auswirken können.|
NTP-Client Quellen Anzahl|    Die aktive Anzahl von NTP-Zeitquellen, die vom NTP-Client verwendet werden. Dies ist die Anzahl aktiver, unterschiedlicher IP-Adressen von Zeitservern, die auf die Anforderungen dieses Clients reagieren. Diese Zahl ist möglicherweise größer oder kleiner als die konfigurierten Peers, abhängig von der DNS-Auflösung von Peer Namen und der aktuellen REACH-Fähigkeit.|
Eingehende NTP-Server Anforderungen|   Anzahl der vom NTP-Server empfangenen Anforderungen (Anforderungen/Sek.).|
Ausgehende NTP-Server Antworten|  Anzahl von Anforderungen, die von NTP-Server (Antworten/Sek.) beantwortet wurden.|

Die ersten drei Leistungsindikatoren Zielen auf Szenarien zur Behebung von Genauigkeits Problemen ab  Im Abschnitt "Problembehandlung und NTP" unten unter [bewährte Methoden](#BestPractices)finden Sie weitere Details.
Die letzten 3 Leistungsindikatoren decken NTP-Server Szenarios ab und sind hilfreich, wenn Sie die Auslastung ermitteln und die Leistung Ihrer aktuellen Leistung ermitteln.

### <a name="configuration-updates-per-environment"></a>Konfigurations Updates pro Umgebung
Im folgenden werden die Änderungen der Standardkonfiguration zwischen Windows 2016 und früheren Versionen für jede Rolle beschrieben.  Die Einstellungen für Windows Server 2016 und Windows 10 Anniversary Update (Build 14393) sind nun eindeutig, weshalb es als separate Spalten angezeigt wird. 

|Rolle|Einstellung|Windows Server 2016|Windows 10|Windows Server 2012 R2</br>Windows Server 2008 R2</br>Windows 10|
|---|---|---|---|---|
|**Eigenständig/Nano Server**||||
| |*Zeit Server*|time.windows.com|Nicht verfügbar|time.windows.com|
| |*Abruf Häufigkeit*|64-1024 Sekunden|Nicht verfügbar|Einmal pro Woche|
| |*Takt Aktualisierungshäufigkeit*|Einmal pro Sekunde|Nicht verfügbar|Einmal pro Stunde|
|**Eigenständiger Client**||||
| |*Zeit Server*|Nicht verfügbar|time.windows.com|time.windows.com|
| |*Abruf Häufigkeit*|Nicht verfügbar|Einmal pro Tag|Einmal pro Woche|
| |*Takt Aktualisierungshäufigkeit*|Nicht verfügbar|Einmal pro Tag|Einmal pro Woche|
|**Domänen Controller**||||
| |*Zeit Server*|PDC/GTIMESERV|Nicht verfügbar|PDC/GTIMESERV|
| |*Abruf Häufigkeit*|64-1024 Sekunden|Nicht verfügbar|1024-32768 Sekunden|
| |*Takt Aktualisierungshäufigkeit*|Einmal pro Tag|Nicht verfügbar|Einmal pro Woche|
|**Domänen Mitglieds Server**||||
| |*Zeit Server*|DC|Nicht verfügbar|DC|
| |*Abruf Häufigkeit*|64-1024 Sekunden|Nicht verfügbar|1024-32768 Sekunden|
| |*Takt Aktualisierungshäufigkeit*|Einmal pro Sekunde|Nicht verfügbar|Alle 5 Minuten|
|**Domänen Mitglieds Client**||||
| |*Zeit Server*|Nicht verfügbar|DC|DC|
| |*Abruf Häufigkeit*|Nicht verfügbar|1204-32768 Sekunden|1024-32768 Sekunden|
| |*Takt Aktualisierungshäufigkeit*|Nicht verfügbar|Alle 5 Minuten|Alle 5 Minuten|
|**Hyper-V-Gast**||||
| |*Zeit Server*|Wählt die beste Option basierend auf dem Stratum des Host-und Zeit Servers|Wählt die beste Option basierend auf dem Stratum des Host-und Zeit Servers|Standardwert für Host|
| |*Abruf Häufigkeit*|Basierend auf der oben genannten Rolle|Basierend auf der oben genannten Rolle|Basierend auf der oben genannten Rolle|
| |*Takt Aktualisierungshäufigkeit*|Basierend auf der oben genannten Rolle|Basierend auf der oben genannten Rolle|Basierend auf der oben genannten Rolle|

>[!NOTE]
>Informationen zu Linux in Hyper-v finden Sie weiter unten im Abschnitt [erlauben der Verwendung des Hyper-v-Host Zeitraums durch Linux](#AllowingLinux) .

### <a name="impact-of-increased-polling-and-clock-update-frequency"></a>Auswirkung erhöhter Abruf-und uhrzeitaktualisierungs Häufigkeit
Um einen genaueren Zeitbedarf zu erzielen, werden die Standardwerte für Abruf Häufigkeiten und Uhr Updates vergrößert, sodass wir kleinere Anpassungen häufiger vornehmen können.  Dies führt zu mehr UDP/NTP-Datenverkehr. diese Pakete sind jedoch klein, sodass es nur sehr wenig oder gar keine Auswirkung auf Breitband Verknüpfungen gibt. Der Vorteil ist jedoch, dass die Zeit für eine größere Vielfalt an Hardware und Umgebungen besser sein sollte.

Bei Akku gestützten Geräten kann das Erhöhen der Abruf Häufigkeit Probleme verursachen.  Akku Geräte speichern die Zeit nicht, während Sie ausgeschaltet werden.  Wenn Sie fortgesetzt werden, sind möglicherweise häufige Korrekturen an der Uhr erforderlich.  Das Erhöhen der Abruf Häufigkeit bewirkt, dass die Uhr instabil wird und auch mehr Energie verbrauchen kann.  Microsoft empfiehlt, die Client Standardeinstellungen nicht zu ändern.

Domänen Controller sollten auch mit den multiplizierten Auswirkungen der verbesserten Updates von NTP-Clients in einer AD-Domäne minimal beeinträchtigt werden.  NTP weist im Vergleich zu anderen Protokollen und einer geringfügigen Auswirkung einen wesentlich geringeren Ressourcenverbrauch auf.  Es ist wahrscheinlicher, dass Sie Grenzwerte für andere Domänen Funktionen erreichen, bevor Sie von den erweiterten Einstellungen für Windows Server 2016 betroffen sind.  Active Directory verwendet Secure NTP, das tendenziell weniger Zeit als Simple NTP synchronisiert, aber wir haben überprüft, dass es auf Clients mit zwei stratums als dem PDC zentral hochskaliert werden kann.

Als konservativer Plan sollten Sie 100 NTP-Anforderungen pro Sekunde pro Kern reservieren.  Beispielsweise sollte eine Domäne aus vier DCS mit jeweils 4 Kernen bestehen, sodass Sie 1600 NTP-Anforderungen pro Sekunde bedienen können.  Wenn Sie über 10 Clients verfügen, die für die Synchronisierung der Zeit einmal alle 64 Sekunden konfiguriert sind, und die Anforderungen im Laufe der Zeit einheitlich empfangen werden, sehen Sie 10000/64 oder ungefähr 160 Anforderungen/Sekunde, die auf alle DCS verteilt sind.  Dies lässt sich problemlos innerhalb unserer 1600 NTP-Anforderungen/Sek. basierend auf diesem Beispiel erkennen.  Dabei handelt es sich um konservative Planungsempfehlungen, die natürlich eine große Abhängigkeit von Ihrem Netzwerk, Prozessor Geschwindigkeiten und-Auslastung haben, also in ihren Umgebungen immer Baseline und Test.

Es ist auch wichtig zu beachten, dass bei einer beträchtlichen CPU-Auslastung, die größer als 40% ist, bei der Ausführung von Domänen Controllern sehr wahrscheinlich Rauschen für NTP-Antworten hinzugefügt werden und ihre Zeit Genauigkeit in Ihrer Domäne beeinträchtigt wird.  Auch hier müssen Sie in Ihrer Umgebung testen, um die tatsächlichen Ergebnisse zu verstehen.

## <a name="time-accuracy-measurements"></a>Zeit Genauigkeits Messungen
### <a name="methodology"></a>Entwickelnde
Zum Messen der Zeit Genauigkeit für Windows Server 2016 haben wir eine Vielzahl von Tools, Methoden und Umgebungen verwendet.  Sie können diese Techniken verwenden, um Ihre Umgebung zu messen und zu optimieren und zu bestimmen, ob die Genauigkeits Ergebnisse Ihren Anforderungen entsprechen. 

Unsere Domänen quelluhr umfasste zwei NTP-Server mit hoher Genauigkeit und GPS-Hardware.  Wir haben auch einen separaten Referenz Testcomputer für Messungen verwendet, bei denen auch GPS-Hardware mit hoher Genauigkeit von einem anderen Hersteller installiert wurde.  Für einige der Tests benötigen Sie eine exakte und zuverlässige Clock-Quelle, die zusätzlich zu ihrer Domänen-Takt Quelle als Referenz verwendet werden kann.

Wir haben vier verschiedene Methoden zum Messen der Genauigkeit mit physischen und virtuellen Computern verwendet. Mehrere Methoden bieten unabhängige Möglichkeiten, um die Ergebnisse zu überprüfen.


1. Messen Sie die lokale Uhr, die durch W32tm bedingt ist, gegen den Referenz Testcomputer, der über separate GPS-Hardware verfügt.  
2.  Messen von NTP-Pings vom NTP-Server an Clients mit W32tm "stripchart"
3.  Messen von NTP-Pings vom Client an den NTP-Server mithilfe von W32tm "stripchart"
4.  Messen Sie die Hyper-V-Ergebnisse vom Host auf den Gast mithilfe des Zeitstempel Zählers (TSC).  Dieser Wert wird von beiden Partitionen und der Systemzeit in beiden Partitionen gemeinsam genutzt.  Wir haben den Unterschied zwischen der hostzeit und der Client Zeit auf dem virtuellen Computer berechnet.  Dann verwenden wir die TSC-Uhr, um die hostzeit vom Gast zu interpolieren, da die Messungen nicht gleichzeitig stattfinden.  Außerdem verwenden wir die Verzögerungen und Latenzzeiten der TSV-Takt Überschreitung in der API.

W32tm ist integriert, aber die anderen Tools, die wir bei unseren Tests verwendet haben, sind für das Microsoft-Repository auf GitHub als Open Source für Ihre Tests und Verwendungsmöglichkeiten verfügbar.  Das wiki im Repository enthält weitere Informationen, die beschreiben, wie die Tools zum Durchführen von Messungen verwendet werden.

> [https://github.com/Microsoft/Windows-Time-Calibration-Tools](https://github.com/Microsoft/Windows-Time-Calibration-Tools)

Die unten gezeigten Testergebnisse sind eine Teilmenge der Messungen, die wir in einer der Testumgebungen vorgenommen haben.  Sie veranschaulichen die Genauigkeit, die am Anfang der Zeit Hierarchie und den untergeordneten Domänen Client am Ende der Zeit Hierarchie beibehalten wird.  Dies wird im Vergleich zu den gleichen Computern in einer 2012-basierten Topologie verglichen.

### <a name="topology"></a>Topologie
Zum Vergleich haben wir sowohl eine Windows Server 2012r2-als auch eine Windows Server 2016-basierte Topologie getestet.  Beide Topologien bestehen aus zwei physischen Hyper-V-Host Computern, die auf einen Windows Server 2016-Computer verweisen, auf dem GPS-Takt Hardware installiert ist.  Jeder Host führt 3 in die Domäne eingebundener Windows-Gäste aus, die entsprechend der folgenden Topologie angeordnet werden.  Die Zeilen stellen die Zeit Hierarchie und das verwendete Protokoll/den Transport dar.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology1.png)

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology2.png)

### <a name="graphical-results-overview"></a>Übersicht über grafische Ergebnisse
Die beiden folgenden Diagramme stellen die Zeit Genauigkeit für zwei bestimmte Member in einer Domäne auf der Grundlage der oben dargestellten Topologie dar.  Jedes Diagramm zeigt die Ergebnisse von Windows Server 2012r2 und 2016, die die Verbesserungen visuell darstellen.  Die Genauigkeit war gemessen von mit-auf dem Gastcomputer im Vergleich zum Host.  Die grafischen Daten repräsentieren eine Teilmenge der gesamten Tests, die wir vorgenommen haben, und zeigen die Szenarien mit dem besten Fall und im schlimmsten Fall an.  

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology3.png)

### <a name="performance-of-the-root-domain-pdc"></a>Leistung des PDC der Stamm Domäne
Der Stamm-PDC wird mit dem Hyper-V-Host (mit VMIC) synchronisiert. dabei handelt es sich um eine Windows Server 2016 mit GPS-Hardware, die sich als genau und stabil erweist.  Dies ist eine wichtige Anforderung für eine Genauigkeit von 1 MS, die als grüner schattierter Bereich angezeigt wird.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart1.png)

### <a name="performance-of-the-child-domain-client"></a>Leistung des untergeordneten Domänen Clients
Der untergeordnete Domänen Client ist mit einem untergeordneten Domänen-PDC verbunden, der mit dem Stamm-PDC kommuniziert.  Die IT-Zeit liegt auch innerhalb der Anforderung von 1 ms.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart2.png)


### <a name="long-distance-test"></a>Langer Entfernungs Test
Im folgenden Diagramm werden 1 virtuelle Netzwerk Hops mit Windows Server 2016 verglichen.  Zwei Diagramme werden mit Transparenz überlagert, um überlappende Daten anzuzeigen.  Das Erhöhen der Netzwerkhops bedeutet eine höhere Latenz und größere Zeit Abweichungen.  Das Diagramm wird vergrößert, sodass die durch den grünen Bereich dargestellten Grenzen von 1 MS größer sind.  Wie Sie sehen können, liegt die Zeit immer noch innerhalb von 1 ms bei mehreren Hops.  Es wird negativ verlagert, was eine Netzwerk Asymmetrie der Netzwerkfunktion veranschaulicht.  Natürlich sind alle Netzwerke anders, und die Messungen hängen von einer Vielzahl von Umgebungsfaktoren ab.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart3.png)

## <a name="BestPractices"></a>Bewährte Methoden für die genaue Zeit Aufbewahrung
### <a name="solid-source-clock"></a>Vollbild-quelluhr
Eine Computerzeit ist nur so gut wie die quelluhr, mit der die Synchronisierung durchgeführt wird.  Um 1 MS Genauigkeit zu erreichen, benötigen Sie GPS-Hardware oder ein Zeit Gerät in Ihrem Netzwerk, auf das Sie als Master quelluhr verweisen.  Mit dem Standardwert von Time.Windows.com kann keine stabile und lokale Zeit Quelle bereitstellen.  Außerdem wirkt sich das Netzwerk auf die Genauigkeit aus, wenn Sie von der quelluhr entfernt werden.  Eine Master quelluhr in jedem Rechenzentrum ist erforderlich, um die beste Genauigkeit zu erzielen.

### <a name="hardware-gps-options"></a>Hardware-GPS-Optionen
Es gibt verschiedene Hardwarelösungen, die eine genaue Zeit bieten können.  Im allgemeinen basieren Lösungen heute auf GPS-Antennen.  Es gibt auch Funk-und DFÜ-Modem Lösungen, die dedizierte Zeilen verwenden.  Sie werden an Ihr Netzwerk entweder als Appliance oder als Plug-in an einen PC angeschlossen, beispielsweise über ein PCIe-oder USB-Gerät.  Verschiedene Optionen bieten unterschiedliche Genauigkeits Stufen, und wie immer sind die Ergebnisse von Ihrer Umgebung abhängig.  Zu den Variablen, die die Genauigkeit beeinflussen, zählen GPS-Verfügbarkeit, Netzwerk Stabilität und-Auslastung sowie PC-Hardware  Dies sind alle wichtigen Faktoren bei der Auswahl einer quelluhr, die wie bereits erwähnt ist, eine Voraussetzung für stabile und genaue Zeit.

### <a name="domain-and-synchronizing-time"></a>Domänen-und Synchronisierungs Zeit
Domänen Mitglieder verwenden die Domänen Hierarchie, um zu bestimmen, welcher Computer als Quelle für die Synchronisierung verwendet wird.  Jedes Mitglied der Domäne findet einen anderen Computer, mit dem synchronisiert werden soll, und speichert ihn als uhrquelle.  Jeder Typ des Domänen Members folgt einem anderen Satz von Regeln, um eine uhrquelle für die Zeitsynchronisierung zu finden.  Der PDC im Gesamtstruktur Stamm ist die Standard-Takt Quelle für alle Domänen.  Im folgenden sind verschiedene Rollen und eine allgemeine Beschreibung der Art und Weise aufgeführt, wie Sie eine Quelle finden:


- **Domänen Controller mit PDC-Rolle** – dieser Computer ist die autoritative Zeit Quelle für eine Domäne. Es ist die präzisere Zeit in der Domäne verfügbar und muss mit einem Domänen Controller in der übergeordneten Domäne synchronisiert werden, außer in Fällen, in denen die [gtimeserv](#GTIMESERV) -Rolle aktiviert ist. 
- **Alle anderen Domänen Controller** – dieser Computer fungiert als Zeit Quelle für Clients und Mitglieds Server in der Domäne. Ein DC kann mit dem PDC der eigenen Domäne oder mit einem beliebigen Domänen Controller in der übergeordneten Domäne synchronisiert werden.
- **Clients/Mitglieds Server** – dieser Computer kann mit einem beliebigen Domänen Controller oder PDC der eigenen Domäne oder mit einem DC oder PDC in der übergeordneten Domäne synchronisiert werden.

Basierend auf den verfügbaren Kandidaten wird ein Bewertungssystem verwendet, um die beste Zeit Quelle zu ermitteln.  Dieses System berücksichtigt die Zuverlässigkeit der Zeit Quelle und ihres relativen Standorts.  Dies geschieht einmal, wenn der Dienst gestartet wurde.  Wenn Sie eine präzisere Kontrolle über die Zeitsynchronisierung benötigen, können Sie einen guten Zeitserver an bestimmten Speicherorten hinzufügen oder Redundanz hinzufügen.  Weitere Informationen finden Sie im Abschnitt [Angeben eines lokalen zuverlässigen Zeit Dienstanbieter mit gtimeserv](#GTIMESERV) .

#### <a name="mixed-os-environments-win2012r2-and-win2008r2"></a>Gemischte Betriebssystemumgebungen (Win2012R2 und Win2008R2)
Eine reine Windows Server 2016-Domänen Umgebung ist für die beste Genauigkeit erforderlich, aber es gibt noch Vorteile in einer gemischten Umgebung.  Das Bereitstellen von Windows Server 2016 Hyper-V in einer Windows 2012-Domäne profitiert den Gästen aufgrund der oben genannten Verbesserungen, aber nur, wenn es sich bei den Gästen auch um Windows Server 2016 handelt.  Ein Windows Server 2016 PDC kann aufgrund der verbesserten Algorithmen eine genauere Zeit bereitstellen, da es sich um eine stabilere Quelle handelt.  Da das Ersetzen des PDC möglicherweise keine Option ist, können Sie stattdessen einen Windows Server 2016-DC mit dem [gtimeserv](#GTIMESERV) -rollset hinzufügen, bei dem es sich um ein Aktualisierungs Upgrade für Ihre Domäne handelt.  Ein Windows Server 2016-Domänen Controller kann einen besseren Zeit-bis downstreamzeit-Client bereitzustellen, aber er ist nur so gut wie seine Quell-NTP-Zeit.

Wie oben bereits erwähnt, wurden die Zeit Abruf-und Aktualisierungs Häufigkeits Angaben mit Windows Server 2016 geändert.  Diese können manuell in Ihre DCS auf der entsprechenden Ebene geändert oder über die Gruppenrichtlinie angewendet werden.  Obwohl wir diese Konfigurationen noch nicht getestet haben, sollten Sie sich in Win2008R2 und Win2012R2 gut Verhalten und einige Vorteile bieten.

Bei Versionen vor Windows Server 2016 gab es mehrere Probleme, die eine genaue Zeit Beibehaltung enthielten, was dazu führte, dass die Systemzeit sofort nach der Anpassung erfolgte.  Aus diesem Grund führt das Abrufen von Zeit Beispielen aus einer exakten NTP-Quelle häufig und das Anordnen der lokalen Uhr mit den Daten zu einer geringeren Abweichung der System Uhren im Zeitraum für die Abtastung, was zu einer besseren Zeit in Bezug auf Betriebssystemversionen führt. Die am besten beobachtete Genauigkeit lag bei ungefähr 5 ms, wenn ein Windows Server 2012r2-NTP-Client, der mit den Einstellungen für hohe Genauigkeit konfiguriert wurde, seine Zeit von einem präzisen Windows 2016 NTP-Server synchronisiert hat.

In einigen Szenarien mit Gast Domänen Controllern kann die Synchronisierung der Domänen Zeit durch Hyper-V-TimeSync-Beispiele beeinträchtigt werden  Dies sollte für Server 2016-Gäste, die auf 2016 Servern mit Hyper-V-Hosts ausgeführt werden, kein Problem mehr sein.

Legen Sie den folgenden Gast Registrierungsschlüssel fest, um den Hyper-V-TimeSync-Dienst zum Bereitstellen von Beispielen für W32Time zu deaktivieren:

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider 
    "Enabled"=dword:00000000

#### <a name="AllowingLinux"></a>Zulassen, dass die Hyper-V-hostzeit von Linux verwendet wird
Für Linux-Gäste, die in Hyper-V ausgeführt werden, sind Clients in der Regel so konfiguriert, dass Sie den NTP-Daemon für die Zeitsynchronisierung mit NTP  Wenn die Linux-Distribution das TimeSync-Protokoll, Version 4, unterstützt und der Linux-Gast den TimeSync-Integrations Dienst aktiviert hat, wird er mit der hostzeit synchronisiert. Dies kann zu inkonsistenter Zeit führen, wenn beide Methoden aktiviert sind.

Um exklusiv mit der hostzeit zu synchronisieren, wird empfohlen, die NTP-Zeitsynchronisierung mit folgenden Optionen zu deaktivieren:

- Deaktivieren von NTP-Servern in der Datei "NTP. conf"
- oder den NTP-Daemon deaktivieren

In dieser Konfiguration ist der Zeit Server Parameter dieser Host.  Die Abruf Häufigkeit beträgt 5 Sekunden, und die Uhrzeit Update Frequenz beträgt ebenfalls 5 Sekunden.

Um exklusiv über NTP zu synchronisieren, wird empfohlen, den TimeSync-Integrations Dienst im Gast-zu deaktivieren.

> [!NOTE]
> Hinweis:  Die Unterstützung der exakten Zeit mit Linux-Gästen erfordert ein Feature, das nur in den neuesten Linux-Upstream-Kernel unterstützt wird. es ist noch nicht in allen Linux-Distributionen allgemein verfügbar. Weitere Informationen zu unterstützten Distributionen finden Sie [unter Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows) .

#### <a name="GTIMESERV"></a>Angeben eines lokalen zuverlässigen Zeit Dienstanbieter mithilfe von gtimeserv
Sie können einen oder mehrere Domänen Controller als exakte Quell Uhren angeben, indem Sie den gtimeserv, den guten Zeit Server und die Flags verwenden.  Beispielsweise können bestimmte Domänen Controller, die mit GPS-Hardware ausgestattet sind, als gtimeserv gekennzeichnet werden.  Dadurch wird sichergestellt, dass Ihre Domäne basierend auf der GPS-Hardware auf eine Uhr verweist.

> [!NOTE]
> Weitere Informationen zu domänenflags finden Sie in der [MS-ADTs-protokolldokumentation](https://msdn.microsoft.com/library/mt226583.aspx).

TimeServ ist ein weiteres verwandtes Domänen Dienste-Flag, das angibt, ob ein Computer zurzeit autorisierend ist.  Ein Domänen Controller in diesem Status gibt "Unknown Stratum" zurück, wenn er über NTP abgefragt wird.  Nachdem der Domänen Controller mehrmals versucht hat, protokolliert er das System Ereignis Zeit-Dienst Ereignis 36.

Wenn Sie einen DC als gtimeserv konfigurieren möchten, können Sie ihn mithilfe des folgenden Befehls manuell konfigurieren.  In diesem Fall verwendet der DC einen anderen Computer als Masteruhr.  Dabei kann es sich um ein Gerät oder einen dedizierten Computer handeln.

    w32tm /config /manualpeerlist:”master_clock1,0x8 master_clock2,0x8” /syncfromflags:manual /reliable:yes /update

> [!NOTE]
> Weitere Informationen finden Sie unter [Konfigurieren des Windows-Zeit Dienstanbieter](https://technet.microsoft.com/library/cc731191.aspx) .

Wenn auf dem DC die GPS-Hardware installiert ist, müssen Sie diese Schritte ausführen, um den NTP-Client zu deaktivieren und den NTP-Server zu aktivieren.

Deaktivieren Sie zunächst den NTP-Client, und aktivieren Sie den NTP-Server mithilfe dieser Registrierungsschlüssel Änderungen.

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpClient /v Enabled /t REG_DWORD /d 0 /f

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpServer /v Enabled /t REG_DWORD /d 1 /f

Starten Sie anschließend den Windows-Zeit Dienst neu.

    net stop w32time && net start w32time

Zum Schluss geben Sie an, dass dieser Computer über eine zuverlässige Zeit Quelle verfügt.
   
    w32tm /config /reliable:yes /update

Um zu überprüfen, ob die Änderungen ordnungsgemäß durchgeführt wurden, können Sie die folgenden Befehle ausführen, die die unten gezeigten Ergebnisse beeinflussen. 

    w32tm /query /configuration

Wert|Erwartete Einstellung|
----- | ----- |
"Verkünceflags"|  5 (lokal)|
NtpServer   |Nah|
DllName |C:\windows\system32\w32time. DLL (lokal)|
Enabled |1 (lokal)|
NtpClient|  Nah|

    w32tm /query /status /verbose

Wert|  Erwartete Einstellung|
----- | ----- |
Stratum|    1 (primärer Verweis-syncd nach Radio-Uhr)|
ReferenceId|    0x4c4f 434c (Quellname:  "LOCAL")|
Source| Lokale CMOS-Uhr|
Phasen Offset|   0.0000000 s|
Serverrolle|    576 (zuverlässiger Zeit Dienst)|

#### <a name="windows-server-2016-on-3rd-party-virtual-platforms"></a>Windows Server 2016 auf virtuellen Drittanbieter Plattformen
Wenn Windows virtualisiert ist, ist der Hypervisor standardmäßig für die Bereitstellung von Zeit verantwortlich.  In die Domäne eingebundener Mitglieder müssen jedoch mit dem Domänen Controller sychronisiert werden, damit Active Directory ordnungsgemäß funktioniert.  Es empfiehlt sich, jede Zeit-Virtualisierung zwischen dem Gast und dem Host von virtuellen Drittanbieter Plattformen zu deaktivieren.

#### <a name="discovering-the-hierarchy"></a>Ermitteln der Hierarchie
Da die Hierarchie der Zeit Kette zur Master Zeit Quelle dynamisch in einer Domäne ist und ausgehandelt wird, müssen Sie den Status eines bestimmten Computers Abfragen, um die Zeit Quelle und die Kette der Master quelluhr zu verstehen.  Dies kann helfen, Zeit Synchronisierungs Probleme zu diagnostizieren.

Wenn Sie ein bestimmtes Client Problem beheben möchten, der erste Schritt ist das Verständnis der Zeit Quelle mit diesem W32tm-Befehl.

    w32tm /query /status

Die Ergebnisse zeigen unter anderem die Quelle an.  Die Quelle gibt an, mit wem Sie die Zeit in der Domäne synchronisieren.  Dies ist der erste Schritt dieser Computerzeit Hierarchie.
Verwenden Sie als nächstes den Quell Eintrag von oben, und verwenden Sie den/StripChart-Parameter, um die nächste Zeit Quelle in der Kette zu suchen.

    w32tm /stripchart /computer:MySourceEntry /packetinfo /samples:1

Der folgende Befehl bietet außerdem eine Liste aller Domänen Controller, die in der angegebenen Domäne gefunden werden können, und gibt ein Ergebnis aus, mit dem Sie jeden Partner bestimmen können.  Dieser Befehl schließt Computer ein, die manuell konfiguriert wurden.
    
    w32tm /monitor /domain:my_domain

Mithilfe der Liste können Sie die Ergebnisse über die Domäne verfolgen und die Hierarchie sowie den Zeit Offset bei jedem Schritt verstehen.  Durch Auffinden des Punkts, an dem der Zeit Offset erheblich schlechter wird, können Sie den Stamm der falschen Zeit ermitteln.  Von dort aus können Sie versuchen, zu verstehen, warum diese Zeit falsch ist, indem Sie die [W32tm-Protokollierung](#W32Logging)aktivieren. 

#### <a name="using-group-policy"></a>Verwenden von Gruppenrichtlinie
Mithilfe von Gruppenrichtlinie können Sie eine strengere Genauigkeit erreichen, indem Sie beispielsweise Clients zur Verwendung bestimmter NTP-Server zuweisen oder die Konfiguration von Betriebssystemen auf Betriebssystemen bei Virtualisierung steuern.  
Im folgenden finden Sie eine Liste möglicher Szenarien und relevanter Gruppenrichtlinie Einstellungen:

**Virtualisierte Domänen** : um virtualisierte Domänen Controller in Windows 2012r2 zu steuern, sodass Sie die Zeit mit Ihrer Domäne und nicht mit dem Hyper-V-Host synchronisieren, können Sie diesen Registrierungs Eintrag deaktivieren.   Für den PDC möchten Sie den Eintrag nicht deaktivieren, da der Hyper-V-Host die stabilste Zeit Quelle bereitstellt.  Der Registrierungs Eintrag erfordert, dass Sie den W32Time-Dienst neu starten, nachdem er geändert wurde.

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider]
    "Enabled"=dword:00000000

**Genauigkeits empfindliche Auslastung** : für Arbeits Auslastungen mit Zeit Genauigkeit können Sie Gruppen von Computern konfigurieren, um die NTP-Server und alle zugehörigen Zeit Einstellungen festzulegen, z. b. Abruf-und Uhrzeit Aktualisierungshäufigkeit.  Dies wird normalerweise von der Domäne gehandhabt, aber zur weiteren Kontrolle können Sie bestimmte Computer als Ziel festlegen, um direkt auf die Masteruhr zu verweisen.

Gruppenrichtlinieneinstellung|   Neuer Wert|
----- | ----- |
NtpServer|  Clockmastername, 0x8|
Minpollinterval|    6 – 64 Sekunden|
MaxPollInterval|    6|
Updateingeterval| 100 – einmal pro Sekunde|
Eventlogflags|  3 – alle speziellen Zeit Protokollierung|

> [!NOTE]
> Die NtpServer-und eventlogflags-Einstellungen befinden sich unter "system\windows Time Service \ Time Providers" unter Verwendung der Windows NTP-Client Einstellungen konfigurieren.  Die anderen drei befinden sich unter system\windows-Zeit Dienst mithilfe der globalen Konfigurationseinstellungen.

**Remote Genauigkeits sensitiv lädt Remote** – für Systeme in Verzweigungs Domänen für die Instanz Retail und die Payment Credit Industry (PCI), verwendet Windows die aktuellen Standortinformationen und den Domänencontrollerlocator, um einen lokalen Domänen Controller zu finden, es sei denn, es ist eine manuelle .  Diese Umgebung erfordert eine Genauigkeit von 1 Sekunde, was eine schnellere Konvergenz zur richtigen Zeit erfordert.  Diese Option ermöglicht es dem W32Time-Dienst, die Uhr rückwärts zu verschieben.  Wenn dies akzeptabel ist und Ihre Anforderungen erfüllt, können Sie die folgende Richtlinie erstellen.   Stellen Sie wie bei jeder Umgebung sicher, dass Sie das Netzwerk testen und eine Baseline durchgehen. 

Gruppenrichtlinieneinstellung|   Neuer Wert|
----- | ----- |
Maxzugewedphaseoffset|  1, wenn mehr als ein zweiter Wert ist, legen Sie die Uhrzeit auf die richtige Uhrzeit fest.|

Die Einstellung maxzugewiesenen wedphaseoffset befindet sich unter system\windows-Zeit Dienst mithilfe der globalen Konfigurationseinstellungen.

> [!NOTE]
> Weitere Informationen zu Gruppenrichtlinien und zugehörigen Einträgen finden Sie im TechNet-Artikel [Windows-Zeit Dienst Tools](windows-time-service-tools-and-settings.md) und-Einstellungen.

## <a name="azure-and-windows-iaas-considerations"></a>Überlegungen zu Azure und Windows IaaS

### <a name="azure-virtual-machine-active-directory-domain-services"></a>Virtueller Azure-Computer: Active Directory Domain Services
Wenn die Azure-VM, die Active Directory Domain Services ausgeführt wird, Teil einer vorhandenen lokalen Active Directory Gesamtstruktur ist, sollte TimeSync (VMIC) deaktiviert werden. Auf diese Weise können alle DCS in der Gesamtstruktur, sowohl physisch als auch virtuell, eine einmalige Synchronisierungs Hierarchie verwenden. Weitere Informationen finden Sie im Whitepaper ["Ausführen von Domänen Controllern in Hyper-V"](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx) .

### <a name="azure-virtual-machine-domain-joined-machine"></a>Virtueller Azure-Computer: In die Domäne eingebundener Computer
Wenn Sie einen Computer, der einer vorhandenen Active Directory-Gesamtstruktur (Virtual oder Physical) angehören, in eine Domäne eingehört, empfiehlt es sich, TimeSync für den Gast zu deaktivieren und sicherzustellen, dass W32Time für die Synchronisierung mit dem Domänen Controller konfiguriert ist, indem Sie die Zeit für Type = NTP5

### <a name="azure-virtual-machine-standalone-workgroup-machine"></a>Virtueller Azure-Computer: Eigenständiger Arbeitsgruppen Computer
Wenn der virtuelle Azure-Computer keiner Domäne hinzugefügt wird und es sich nicht um einen Domänen Controller handelt, wird empfohlen, die Standardzeit Konfiguration beizubehalten und die VM mit dem Host zu synchronisieren.

## <a name="windows-application-requiring-accurate-time"></a>Windows-Anwendung mit präziser Zeit
### <a name="time-stamp-api"></a>Zeitstempel-API
Programme, die in Bezug auf die UTC die höchste Genauigkeit erfordern, und nicht der Zeitverlauf, sollten die [getsystemtimepreciseasfiletime-API](https://msdn.microsoft.com/library/windows/desktop/Hh706895.aspx)verwenden.  Dadurch wird sichergestellt, dass Ihre Anwendung die System Zeit erhält, die vom Windows-Zeit Dienst abhängig ist.

### <a name="udp-performance"></a>UDP-Leistung
Wenn Sie über eine Anwendung verfügen, die UDP-Kommunikation für Transaktionen verwendet, und es wichtig ist, die Latenz zu minimieren, gibt es einige verwandte Registrierungseinträge, die Sie verwenden können, um einen Bereich von Ports zu konfigurieren, der vom Port der Basis Filter-Engine ausgeschlossen wird.  Dadurch wird die Latenzzeit verbessert und der Durchsatz erhöht.  Änderungen an der Registrierung sollten jedoch auf erfahrene Administratoren beschränkt sein.  Außerdem wird durch diese Problem Umgehung ausgeschlossen, dass die Ports nicht durch die Firewall geschützt werden.  Weitere Informationen finden Sie in der nachfolgenden Artikel Referenz.

Für Windows Server 2012 und Windows Server 2008 müssen Sie zuerst einen Hotfix installieren.  Sie können auf diesen KB-Artikel verweisen: [Datagrammverlust beim Ausführen einer Multicast-Empfänger Anwendung in Windows 8 und Windows Server 2012](https://support.microsoft.com/kb/2808584)

### <a name="update-network-drivers"></a>Aktualisieren von Netzwerk Treibern
Einige Netzwerkhersteller verfügen über Treiber Updates, die die Leistung im Hinblick auf die Treiber Latenz und die Pufferung von UDP-Paketen verbessern.  Wenden Sie sich an Ihren Netzwerkhersteller, um zu ermitteln, ob Updates für den UDP-Durchsatz vorhanden sind.

## <a name="logging-for-auditing-purposes"></a>Protokollierung zu Überwachungszwecken
Zur Einhaltung der Regeln für die Zeitablauf Verfolgung können Sie W32tm-Protokolle, Ereignisprotokolle und System Monitor Informationen manuell archivieren.  Später können die archivierten Informationen verwendet werden, um die Kompatibilität zu einem bestimmten Zeitpunkt in der Vergangenheit zu bestätigen.  Die folgenden Faktoren werden verwendet, um die Genauigkeit anzugeben.


1. Takt Genauigkeit mithilfe des Leistungs Monitors für den berechneten Zeit Offset.  Dadurch wird die Uhr mit in der gewünschten Genauigkeit angezeigt.
2.  Clock-Quelle, die in den W32tm-Protokollen nach "Peer Response from" sucht.   Nach dem Nachrichtentext handelt es sich um die IP-Adresse oder VMIC, die die Uhrzeit Quelle und die nächste in der Kette der zu validierenden Referenzuhren beschreibt.
3.  Status der Takt Bedingung mithilfe der W32tm-Protokolle zum Überprüfen der "clockdispl-Disziplin: \*Versatz\*Zeit.\*  Dies gibt an, dass W32tm zu diesem Zeitpunkt aktiv ist.

### <a name="event-logging"></a>Ereignisprotokollierung
Um die gesamte Story zu erhalten, benötigen Sie auch Ereignisprotokoll Informationen.  Durch das Erfassen des System Ereignis Protokolls und das Filtern nach "Time-Server", "Microsoft-Windows-Kernel-Boot", "Microsoft-Windows-Kernel-General" können Sie möglicherweise ermitteln, ob sich die Zeit geändert hat, z. b. von Drittanbietern.  Diese Protokolle sind möglicherweise erforderlich, um externe Störungen auszuschließen.  Die Gruppenrichtlinie kann Einfluss darauf haben, welche Ereignisprotokolle in das Protokoll geschrieben werden.  Weitere Informationen finden Sie im obigen Abschnitt unter Verwenden von Gruppenrichtlinie.

### <a name="W32Logging"></a>W32Time Debug-Protokollierung
Der folgende Befehl aktiviert die Protokollierung, die die regelmäßigen Updates der Uhr anzeigt und die quelluhr angibt, um W32tm zu Überwachungszwecken zu aktivieren.  Starten Sie den Dienst neu, um die neue Protokollierung zu aktivieren.  

Weitere Informationen finden Sie unter Aktivieren [der Debugprotokollierung im Windows-Zeit Dienst](https://support.microsoft.com/kb/816043).

    w32tm /debug /enable /file:C:\Windows\Temp\w32time-test.log /size:10000000 /entries:0-73,103,107,110

### <a name="performance-monitor"></a>Performance Monitor (Leistungsüberwachung)
Der Windows Server 2016 Windows-Zeit Dienst stellt Leistungsindikatoren zur Verfügung, die zum Erfassen der Protokollierung für die Überwachung verwendet werden können.  Diese können lokal oder Remote protokolliert werden.  Sie können den Computer Zeit Offset und die Roundtrip-Verzögerungs Zähler aufzeichnen.  
Wie bei jedem beliebigen Leistungsindikatoren können Sie diese Remote überwachen und Warnungen mithilfe System Center Operations Manager erstellen.  Sie können beispielsweise eine Warnung verwenden, um Sie zu warnen, wenn der Zeit Offset von der gewünschten Genauigkeit abweicht.  Weitere Informationen finden Sie im [System Center-Management Pack](https://social.technet.microsoft.com/wiki/contents/articles/15251.system-center-management-pack-authoring-guide.aspx) .

### <a name="windows-traceability-example"></a>Windows-nach Verfolgungs Beispiel
In W32tm-Protokolldateien sollten Sie zwei Informationen überprüfen.  Der erste ist ein Hinweis darauf, dass die Protokolldatei zurzeit eine Bedingungs-Uhr ist.  Dadurch wird nachgewiesen, dass die Uhr zum Zeitpunkt der umstrittenen Zeit vom Windows-Zeit Dienst festgestellt wurde.

    151802 20:18:32.9821765s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:223 CR:156250 UI:100 phcT:65 KPhO:14307
    151802 20:18:33.9898460s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:64 KPhO:41
    151802 20:18:44.1090410s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:65 KPhO:38

Der Hauptgrund ist, dass Sie Nachrichten mit dem Präfix clockdispln-Disziplin sehen, bei der es sich um eine Prüfpunkt-W32Time handelt.
 
Als nächstes müssen Sie den letzten Bericht im Protokoll vor dem umstrittenen Zeitpunkt finden, der den Quellcomputer meldet, der zurzeit als die Referenzuhr verwendet wird.  Dabei kann es sich um eine IP-Adresse, einen Computernamen oder den VMIC-Anbieter handeln, der angibt, dass die Synchronisierung mit dem Host für Hyper-V stattfindet.  Im folgenden Beispiel wird eine IPv4-Adresse von 10.197.216.105 bereitstellt.

    151802 20:18:54.6531515s - Response from peer 10.197.216.105,0x8 (ntp.m|0x8|0.0.0.0:123->10.197.216.105:123), ofs: +00.0012218s

Nachdem Sie nun das erste System in der Verweis Zeit Kette überprüft haben, müssen Sie die Protokolldatei auf der Verweis Zeit Quelle untersuchen und die gleichen Schritte wiederholen.  Dies wird so lange fortgesetzt, bis Sie zu einer physischen Uhr wie GPS oder einer bekannten Zeit Quelle wie NIST gelangen.  Wenn es sich bei der Referenzuhr um GPS-Hardware handelt, sind möglicherweise auch Protokolle aus dem hergestellten erforderlich.

## <a name="network-considerations"></a>Netzwerküberlegungen
Die NTP-Protokoll Algorithmen haben eine Abhängigkeit von der Symmetrie Ihres Netzwerks.  Wenn Sie die Anzahl der Netzwerkhops erhöhen, erhöht sich die Wahrscheinlichkeit der Asymmetrie.  Hier ist es schwierig, vorherzusagen, welche Arten von Genauigkeits Typen in ihren spezifischen Umgebungen angezeigt werden. 

Der System Monitor und die neuen Windows-Zeit Indikatoren in Windows Server 2016 können verwendet werden, um die Genauigkeit ihrer Umgebungen zu bewerten und Basis Linien zu erstellen. Außerdem können Sie die Problembehandlung durchführen, um den aktuellen Offset eines beliebigen Computers in Ihrem Netzwerk zu ermitteln.

Es gibt zwei allgemeine Standards für die genaue Zeit über das Netzwerk.  PTP ([Precision Time Protocol-IEEE 1588](https://www.nist.gov/el/intelligent-systems-division-73500/introduction-ieee-1588)) hat strengere Anforderungen an die Netzwerkinfrastruktur, kann aber häufig die Genauigkeit der untergeordneten Mikrosekunden bereitstellen.  NTP ([Network Time Protocol – RFC 1305](https://tools.ietf.org/html/rfc1305)) funktioniert in einer größeren Vielzahl von Netzwerken und Umgebungen, was die Verwaltung erleichtert. 

Windows unterstützt für Computer, die keiner Domäne beigetreten sind, standardmäßig Simple NTP (RFC2030).  Für in die Domäne eingebundenen Computern wird ein sicheres NTP namens [MS-SNTP](https://msdn.microsoft.com/library/cc246877.aspx)verwendet, das von der Domäne aushandelte geheime Schlüssel nutzt und einen Verwaltungs Vorteil gegenüber authentifizierten NTP bietet, der in RFC1305 und RFC5905 beschrieben wird.   

Sowohl die Domänen-als auch die nicht mit der Domäne verbundenen Protokolle erfordern den UDP-Port 123  Weitere Informationen zu den bewährten Methoden für NTP finden Sie unter [Network Time Protocol Best Current Practices IETF Draft](https://tools.ietf.org/html/draft-ietf-ntp-bcp-00).

### <a name="reliable-hardware-clock-rtc"></a>Zuverlässige Hardwareuhr (RTC)
Windows kann nicht schrittweise ausgeführt werden, es sei denn, es werden bestimmte Begrenzungen überschritten, sondern die Uhr.  Dies bedeutet, dass W32tm die Häufigkeit der Uhr in regelmäßigen Abständen mit der Einstellung Takt Update Frequency anpasst, bei der der Standardwert einmal pro Sekunde mit Windows Server 2016 verwendet wird.  Wenn die Uhr hinter der Uhr steht, wird die Häufigkeit beschleunigt, und wenn Sie im Voraus ist, wird die Häufigkeit verlangsamt.  Während dieser Zeit zwischen den Anpassungen der Taktfrequenz befindet sich die Hardwareuhr jedoch in der Kontrolle.  Wenn ein Problem mit der Firmware oder der Hardwareuhr vorliegt, kann die Zeit auf dem Computer weniger genau werden.

Dies ist ein weiterer Grund, den Sie in Ihrer Umgebung testen und Baseline testen müssen.  Wenn sich der Leistungswert "berechneter Zeit Offset" nicht mit der Genauigkeit stabilisiert, die Sie als Ziel haben, sollten Sie überprüfen, ob die Firmware auf dem neuesten Stand ist.  Als weiterer Test können Sie feststellen, ob die doppelte Hardware dasselbe Problem reproduziert.

### <a name="troubleshooting-time-accuracy-and-ntp"></a>Problembehandlung bei Zeit Genauigkeit und NTP
Sie können den obigen Abschnitt Ermitteln der Hierarchie verwenden, um die Quelle der ungenauen Zeit zu verstehen.  Wenn Sie sich den Zeit Offset ansehen, finden Sie den Punkt in der Hierarchie, an dem die Zeit am meisten von der NTP-Quelle abweicht.  Nachdem Sie die Hierarchie verstanden haben, sollten Sie wissen, warum eine bestimmte Zeit Quelle keine genaue Zeit erhält.  

Wenn Sie sich auf das System mit unterschiedlichen Zeitpunkten konzentrieren, können Sie diese Tools unten verwenden, um weitere Informationen zu sammeln, die Ihnen helfen, das Problem zu ermitteln und eine Lösung zu finden.  Der upstreamclocksource-Verweis unten ist die mit "w32tm/config/Status" erkannte Uhr.


- System Ereignisprotokolle
- Aktivieren der Protokollierung mit: W32tm Logs-W32tm/debug/enable/file: c:\windows\temp\w32time-Test.log/size: 10000000/entries: 0-300
- w32Time-Registrierungsschlüssel HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time
- Lokale Netzwerk Ablauf Verfolgungen
- Leistungsindikatoren (auf dem lokalen Computer oder upstreamclocksource)
- W32tm/stripchart/Computer: upstreamclocksource
- Ping upstreamclocksource, um die Latenz und die Anzahl der Hops zur Quelle zu verstehen
- Tracert upstreamclocksource

Problem|    Symptome|   Auflösung|
----- | ----- | ----- |
Die lokale TSC-Uhr ist nicht stabil.| Bei Verwendung von Perfmon-Physical Computer – die stabile Uhr der Synchronisierungs Uhr, aber Sie sehen weiterhin alle 1-2 Minuten von mehreren 100 US. |   Aktualisieren Sie die Firmware, oder überprüfen Sie, ob andere Hardware dasselbe Problem nicht anzeigt.|
Netzwerk Latenz|    w32tm stripchart zeigt eine roundtripdelay von mehr als 10 MS an.  Abweichungen in der Verzögerung führen zu einem Rauschen, das bei der Roundtripzeit um 1/2 verläuft, z. a. eine Verzögerung, die nur eine Richtung aufweist.</br></br>Upstreamclocksource ist mehrere Hops, wie durch Ping angegeben.  TTL sollte in der Nähe von 128 liegen.</br></br>Verwenden Sie tracert, um die Latenz bei jedem Hop zu ermitteln.    | Finden Sie eine genauere Zeit Quelle für die Zeit.  Eine Lösung besteht darin, eine quelluhr im gleichen Segment zu installieren oder manuell auf die geografisch engere quelluhr zu verweisen.  Fügen Sie in einem Domänen Szenario einen Computer mit der gtimeserv-Rolle hinzu. |  
Die NTP-Quelle kann nicht zuverlässig erreicht werden.|    W32tm/stripchart zeitweise "Timeout bei der Anforderung" zurückgegeben.    |NTP-Quelle reagiert nicht|
NTP-Quelle reagiert nicht|    Überprüfen Sie die Perfmon-Leistungsindikatoren für die NTP-Client Quellen Anzahl, eingehende NTP-Serveranforderungen, ausgehende NTP-Server Antworten und bestimmen Sie Ihre Nutzung im Vergleich zu ihren Basis Linien.|    Bestimmen Sie mithilfe von Server Leistungsindikatoren, ob sich das Laden in Bezug auf ihre Basis Linien geändert hat.</br></br>Gibt es Probleme mit der Netzwerk Überlastung?|
Der Domänen Controller verwendet nicht die genaueste Uhr.|    Änderungen in der Topologie oder vor kurzem hinzugefügte Master Zeit.|   w32tm/resync/Rediscover|
Client Uhren werden Abdriften| Das Zeit Dienst Ereignis 36 im System Ereignisprotokoll und/oder Text in der Protokolldatei, in der Folgendes beschrieben wird: Der Zähler "NTP-Client Zeit Quelle" wird von 1 auf 0 (null)|Beheben Sie Probleme mit der Upstreamquelle, und verstehen Sie, ob Leistungsprobleme auftreten.|

### <a name="baselining-time"></a>Baselining-Zeit
Baselining ist wichtig, damit Sie zunächst die Leistung und die Genauigkeit Ihres Netzwerks verstehen und in Zukunft mit der Baseline vergleichen können, wenn Probleme auftreten.  Sie möchten eine Baseline für den Stamm-PDC oder alle mit dem gtimesrv markierten Computer durchgehen.  Außerdem empfiehlt es sich, die PDC in jeder Gesamtstruktur als Grundlage zu Kennwerten.  Wählen Sie schließlich alle wichtigen DCS oder Computer aus, die interessante Merkmale aufweisen, wie z. b. Entfernung oder hohe Auslastung und Baseline.

Dies ist auch nützlich für die Baseline Windows Server 2016 vs 2012 R2, Sie haben jedoch nur W32tm/stripchart als Tool, das Sie für den Vergleich verwenden können, da Windows Server 2012r2 keine Leistungsindikatoren enthält.  Wählen Sie zwei Computer mit denselben Merkmalen aus, oder aktualisieren Sie einen Computer, und vergleichen Sie die Ergebnisse nach dem Update.  Der Nachtrag der Windows-Zeitmessung bietet weitere Informationen zum Ausführen ausführlicher Messungen zwischen 2016 und 2012.

Sammeln Sie mit allen Leistungsindikatoren für W32Time mindestens eine Woche Daten.  Dadurch wird sichergestellt, dass Sie im Laufe der Zeit über einen ausreichend großen Verweis auf das Konto für verschiedene im Netzwerk verfügen, um sicherzustellen, dass Ihre Zeit Genauigkeit stabil ist.

### <a name="ntp-server-redundancy"></a>NTP-Server Redundanz
Bei einer manuellen NTP-Serverkonfiguration, die für nicht mit der Domäne verbundene Computer oder den PDC verwendet wird, ist die Verwendung mehrerer Server bei der Verfügbarkeit ein gutes Redundanz Measure.  Dies kann auch eine bessere Genauigkeit bieten, wenn Sie davon ausgehen, dass alle Quellen genau und stabil sind.  Wenn die Topologie jedoch nicht gut entworfen wurde oder die Zeitquellen nicht stabil sind, ist die resultierende Genauigkeit möglicherweise schlechter, daher ist es ratsam, dies zu beachten.  Der Grenzwert für die unterstützten Zeitserver W32Time kann manuell auf 10 verweisen. 

## <a name="leap-seconds"></a>Schaltsekunden
Der Drehungs Zeitraum der Erde variiert im Laufe der Zeit aufgrund von Klima-und geologischen Ereignissen. In der Regel ist die Variation ungefähr eine Sekunde alle paar Jahre. Wenn die Variation von der atomaren Zeit zu groß wird, wird eine Korrektur von einer Sekunde (nach oben oder unten) eingefügt, die als Schaltsekunde bezeichnet wird. Dies erfolgt so, dass der Unterschied niemals 0,9 Sekunden überschreitet. Diese Korrektur wird sechs Monate vor der tatsächlichen Korrektur angekündigt. Vor Windows Server 2016 war der Microsoft-Zeit Dienst nicht auf die Schaltsekunden aufmerksam, sondern auf den Dienst für die externe Zeit, um dies zu erledigen. Mit der zunehmenden Zeit Genauigkeit von Windows Server 2016 arbeitet Microsoft an einer geeigneteren Lösung für das Problem der Schaltarbeit.

## <a name="secure-time-seeding"></a>Sicheres Zeit Seeding
W32Time in Server 2016 enthält das Feature für sicheres Zeit Seeding. Diese Funktion bestimmt die ungefähre aktuelle Zeit von ausgehenden SSL-Verbindungen.  Dieser Zeitwert wird verwendet, um die lokale Systemuhr zu überwachen und grobe Fehler zu beheben. Weitere Informationen zu diesem Feature finden Sie in [diesem Blogbeitrag](https://blogs.msdn.microsoft.com/w32time/2016/09/28/secure-time-seeding-improving-time-keeping-in-windows/).  Bei bereit Stellungen mit einer zuverlässigen Zeit Quelle (n) und überwachten Computern, die eine Überwachung für Zeit Offsets beinhalten, können Sie sich entscheiden, nicht das Feature für sicheres Zeit Seeding zu verwenden und stattdessen auf Ihre vorhandene Infrastruktur zu vertrauen. 

Sie können das Feature mit den folgenden Schritten deaktivieren:

1.  Legen Sie den Konfigurations Wert der utilizess ltimedata-Registrierung auf einem bestimmten Computer auf 0 fest:

    reg Add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\Config/v utilizess ltimedata/t REG_DWORD/d 0/f


2.  Wenn Sie den Computer aus irgendeinem Grund nicht sofort neu starten können, können Sie den W32Time-Dienst über das Konfigurationsupdate benachrichtigen. Dadurch wird die Zeitüberwachung und-Erzwingung basierend auf den von SSL-Verbindungen gesammelten Zeit Daten beendet. 

    W32tm. exe/config/Update

3.  Durch einen Neustart des Computers wird die Einstellung sofort wirksam und bewirkt, dass die Erfassung von Zeit Daten von SSL-Verbindungen nicht mehr möglich ist.  Der zweite Teil hat einen sehr kleinen Verwaltungsaufwand und sollte kein Leistungsproblem sein.

4.  Wenn Sie diese Einstellung in einer gesamten Domäne anwenden möchten, legen Sie den Wert für "utilizmeltimedata" in der Gruppenrichtlinien Einstellung W32Time auf 0 fest, und veröffentlichen Sie die Einstellung.  Wenn die Einstellung von einem Gruppenrichtlinie-Client abgerufen wird, wird der W32Time-Dienst benachrichtigt und beendet die Zeitüberwachung und-Erzwingung mithilfe von SSL-Zeit Daten. Die Erfassung der SSL-Zeit Daten wird beendet, wenn jeder Computer neu gestartet wird. Wenn Ihre Domäne übertragbare schlanke Laptops/Tablets und andere Geräte verfügt, können Sie diese Computer von dieser Richtlinien Änderung ausschließen. Diese Geräte stellen schließlich einen Akku Abfluss dar und benötigen das Feature für sicheres Zeit Seeding, um Ihre Zeit zu starten.


