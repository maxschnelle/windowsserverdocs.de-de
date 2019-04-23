

## <a name="windows-server-2016-improvements"></a>Verbesserungen in Windows Server 2016
### <a name="windows-time-service-and-ntp"></a>Windows-Zeitdienst und NTP
Windows Server 2016 wurde die Algorithmen verbessert, die er verwendet, um Zeit zu beheben und die lokale Uhr zum Synchronisieren mit UTC-Bedingung.  NTP verwendet 4 Werte zum Berechnen des Zeitoffsets basierend auf den Zeitstempeln der Client-Anforderung/Antwort und Anforderung/Antwort des Servers.  Allerdings Netzwerke enthalten viel überflüssiges, und können Spitzen in der Daten von NTP aufgrund von Überlastung des Netzwerks und andere Faktoren, die Auswirkungen von Netzwerklatenz auf vorhanden sein.  Windows 2016 Algorithmen entstehen, dieses Rauschen, das über eine Reihe unterschiedlicher Verfahren, was zu einer stabilen und genau Uhr führt.  Darüber hinaus verwenden die Quelle wir für die genaue Uhrzeit Verweise eine verbesserte API die bietet uns eine bessere Auflösung.  Mit diesen Verbesserungen können wir 1 ms Genauigkeit im Hinblick auf die UTC in eine Domäne zu erreichen.

### <a name="hyper-v"></a>Hyper-V
Windows 2016 wurde verbessert, dass den Hyper-V-TimeSync-Dienst. Verbesserungen umfassen die genauere Anfangszeit für die VM starten "oder" VM-Wiederherstellung "und" Interrupt Latenz Korrektur Beispiele bereitgestellt, um w32time.  Diese Verbesserung ermöglicht uns, bleiben auf 10µs des Hosts mit einem RMS (Root Mean quadriert, der Varianz angibt), der 50µs, sogar auf einem Computer mit 75 % laden. Weitere Informationen finden Sie unter [Hyper-V-Architektur](https://msdn.microsoft.com/library/cc768520.aspx).

> [!NOTE]
> Load erstellt wurde, prime95-Benchmark mit ausgeglichene Profil verwenden.

Darüber hinaus ist die Stratum-Ebene, die der Host zum Gast meldet transparenter.  Zuvor würde der Host einen festen Stratum von 2 ist, unabhängig von der Genauigkeit darstellen.  Mit den Änderungen in Windows Server 2016 meldet der Host eine Stratum eins größer ist als Host einer Schicht, die Zeit für virtuelle Gäste führt.  Der Host Stratum richtet sich nach w32time auf normale Weise basierend auf der Quellzeit.  Domäne eingebundenen Windows 2016 Gäste findet die genaueste Uhr, anstatt auf den Host automatisch.  Es wurde aus diesem Grund, die wir empfohlen Zeitanbieter Hyper-V-Einstellung für Computer, die in einer Domäne in Windows 2012 R2 und unter Einbeziehung manuell deaktivieren.

### <a name="monitoring"></a>Überwachung
Systemmonitor-Leistungsindikatoren wurden hinzugefügt.  Diese können Sie grundlegende, Überwachung und Problembehandlung uhrzeitsynchronisierungsdienst.  Zu diesen Zählern gehören:

Leistungsindikator|Beschreibung|
----- | ----- |
Offset der Zeit berechnet|   Die absolute Zeit zwischen der Systemuhr und die gewählte Zeitquelle, versetzt werden, wie vom W32Time-Dienst in Mikrosekunden berechnet. Wenn ein neues Beispiel für gültige verfügbar ist, wird die berechnete Zeit mit der Zeitoffset, angegeben durch das Beispiel aktualisiert. Dies ist der tatsächliche Zeitoffset der lokalen Uhr. W32Time Uhr Korrektur, die mit diesem Offset initiiert und aktualisiert den berechneten zwischen Beispiele mit der verbleibenden Zeitoffset, der die für die lokale Uhr angewendet werden. Clock-Genauigkeit kann überwacht werden, verwenden diesen Leistungsindikator mit einem niedrigen Abrufintervall (z. B.: 256 Sekunden oder weniger) und nach der Wert dieses Indikators, die kleiner als der Grenzwert des gewünschten Uhr Genauigkeit sind.|
Häufigkeit der Uhrzeitanpassung| Der absolute Häufigkeit uhrzeitanpassung an die lokale Systemuhr W32Time in Teilen 1 Mrd. vorgenommen wurden. Dieser Leistungsindikator wird die Aktionen von W32time visualisieren.|
NTP-Roundtrip-Verzögerung|    Die letzte Round-Trip Verzögerung, die den NTP-Client im Empfangen einer Antwort vom Server in Mikrosekunden. Dies ist die Zeit auf dem Client NTP zwischen eine Anforderung mit dem NTP-Server übertragen, und erhalten eine gültige Antwort vom Server verstrichen. Dieser Indikator wird der Verzögerungen der NTP-Client charakterisieren. Vergrößern oder zu unterschiedlichen Roundtrips können Rauschen NTP Zeit Berechnungen hinzufügen, die sich wiederum auf die Genauigkeit der zeitsynchronisierung durch NTP auswirken kann.|
NTP-Client-Quellenanzahl|    Aktive Anzahl der NTP-Zeitquellen von der NTP-Client verwendet wird. Dies ist die Anzahl der aktiven, unterschiedliche IP-Adressen der Zeit-Servern, die auf dieser Client-Anforderungen reagieren. Diese Zahl möglicherweise größer oder kleiner als die konfigurierte Peers, je nach DNS-Auflösung von Peernamen und aktuelle Reach-Fähigkeit.|
NTP-Server eingehenden Anforderungen|   Anzahl der Anforderungen, die von der NTP-Server (Anfragen/s) empfangen.|
NTP-Server für ausgehende Antworten|  Anzahl der Anforderungen, die von NTP-Server (Antworten/s) beantwortet.|

Die ersten 3 Leistungsindikatoren Szenarien für die Problembehandlung bei der Genauigkeit als Ziel verwenden.  Die Problembehandlung-Uhrzeitsynchronisierungsdienst und NTP im Abschnitt unten unter [Best Practices](#BestPractices), beinhaltet mehr Details.
Die letzten 3 Leistungsindikatoren werden NTP-Server-Szenarien behandelt und sind hilfreich bei bestimmen das Laden und der Baseline für die aktuelle Leistung.

### <a name="configuration-updates-per-environment"></a>Konfigurationsupdates pro Umgebung
Im folgenden werden die Änderungen in der Standardkonfiguration zwischen Windows 2016 und früheren Versionen für jede Rolle beschrieben.  Die Einstellungen für Windows Server 2016 und Windows 10 Anniversary Update (Build 14393), sind nun eindeutig ist es als separate Spalten angezeigt werden. 

|Role-Eigenschaft|Einstellung|Windows Server 2016|Windows 10|Windows Server 2012 R2</br>Windows Server 2008 R2</br>Windows 10|
|---|---|---|---|---|
|**Eigenständige/Nano Server**||||
| |*Zeitserver*|time.windows.com|Nicht verfügbar|time.windows.com|
| |*Abrufhäufigkeit*|64 - 1024 Sekunden|Nicht verfügbar|Einmal pro Woche|
| |*Update-Taktfrequenz*|Einmal pro Sekunde|Nicht verfügbar|Nach einer Stunde|
|**Eigenständiger Client**||||
| |*Zeitserver*|Nicht verfügbar|time.windows.com|time.windows.com|
| |*Abrufhäufigkeit*|Nicht verfügbar|Einmal pro Tag|Einmal pro Woche|
| |*Update-Taktfrequenz*|Nicht verfügbar|Einmal pro Tag|Einmal pro Woche|
|**Domänencontroller**||||
| |*Zeitserver*|PDC/GTIMESERV|Nicht verfügbar|PDC/GTIMESERV|
| |*Abrufhäufigkeit*|64-1024 Sekunden|Nicht verfügbar|1024 - 32768 Sekunden|
| |*Update-Taktfrequenz*|Einmal pro Tag|Nicht verfügbar|Einmal pro Woche|
|**Domänenmitgliedsserver**||||
| |*Zeitserver*|DC|Nicht verfügbar|DC|
| |*Abrufhäufigkeit*|64-1024 Sekunden|Nicht verfügbar|1024 - 32768 Sekunden|
| |*Update-Taktfrequenz*|Einmal pro Sekunde|Nicht verfügbar|Einmal alle 5 Minuten|
|**Domänenclient-Element**||||
| |*Zeitserver*|Nicht verfügbar|DC|DC|
| |*Abrufhäufigkeit*|Nicht verfügbar|1204 - 32768 Sekunden|1024 - 32768 Sekunden|
| |*Update-Taktfrequenz*|Nicht verfügbar|Einmal alle 5 Minuten|Einmal alle 5 Minuten|
|**Hyper-V-Gastcomputers**||||
| |*Zeitserver*|Wählt die beste Option, die basierend auf Stratum von Host und die Uhrzeit-server|Wählt die beste Option, die basierend auf Stratum von Host und die Uhrzeit-server|Der Standardwert ist Host|
| |*Abrufhäufigkeit*|Basierend auf Rolle, die oben genannten|Basierend auf Rolle, die oben genannten|Basierend auf Rolle, die oben genannten|
| |*Update-Taktfrequenz*|Basierend auf Rolle, die oben genannten|Basierend auf Rolle, die oben genannten|Basierend auf Rolle, die oben genannten|

>[!NOTE]
>Unter Linux in Hyper-V finden Sie unter den [Linux ermöglicht, für das Hyper-V-Host verwenden](#AllowingLinux) Abschnitt weiter unten.

### <a name="impact-of-increased-polling-and-clock-update-frequency"></a>Auswirkungen der erhöhte Abruf- und Update-Taktfrequenz
Um genauer Zeitpunkt, zu gewährleisten die Standardwerte für das Abrufen von Frequenzen und Clock-Updates werden erhöht, die uns kleine Anpassungen vornehmen, häufiger zu ermöglichen.  Dies bewirkt, dass weitere UDP/NTP-Datenverkehr, diese Pakete sind jedoch klein, daher sollten nur sehr wenig oder gar keinen über Breitband-Verbindungen. Der Vorteil ist, ist jedoch Zeit sollte auf einem breiteren Spektrum von Hardware und Umgebungen besser sein.

Bei Pufferbatterie-Geräten kann der Abruf häufiger Probleme verursachen.  Akku Geräte speichern nicht die Zeit, während Sie deaktiviert.  Wenn sie fortsetzen möchten, kann es häufig Korrekturen vor, um die Uhr erforderlich.  Bewirkt, dass die Uhr instabil wird und leistungsfähiger können auch verwenden, erhöhen das Abrufintervall.  Microsoft empfiehlt, dass Sie die Client-Standardeinstellungen nicht ändern.

Domänencontroller sollten auch mit dem multipliziertes Effekt der erhöhte Updates von NTP-Clients in einer AD-Domäne nur minimal beeinträchtigt werden.  NTP weist eine viel kleinere Verbrauch im Vergleich zu anderen Protokolle und eine marginale Auswirkung.  Sie sind eher Grenzwerten für andere Domänenfunktionen erreicht wird, bevor die Auswirkungen von die größere Anzahl von Einstellungen für Windows Server 2016.  Active Directory verwendet sichere NTP, die tendenziell weniger genau als einfache NTP Uhrzeit zu synchronisieren, sondern Sie haben sichergestellt, dass er auf Clients zwei Stratum Weg von der PDC skaliert werden kann.

Als konservative Plan sollten Sie 100 NTP-Anforderungen pro Sekunde und Kern reservieren.  Beispielsweise sollten eine Domäne, setzt sich aus 4 DCs mit 4 Kernen, Sie 1600 NTP-Anforderungen pro Sekunde verarbeiten können.  Wenn Sie 10 k-Clients, die zum Zeitpunkt der Synchronisierung alle 64 Sekunden konfiguriert haben und die Anforderungen gleichmäßig im Laufe der Zeit empfangen werden, sehen Sie 10.000/64 oder CA. 160 Anforderungen/Sekunde, die auf allen Domänencontrollern verteilt.  Dies liegt einfach in unsere 1600 NTP-Anforderungen/s basierend auf diesem Beispiel.  Diese sind vorsichtig planen die Empfehlungen und natürlich haben eine große Abhängigkeit im Netzwerk, prozessorgeschwindigkeiten und Lasten umgehen kann, sodass wie immer Baseline und Test in Ihrer Umgebung.

Es ist auch wichtig zu beachten, dass wenn Ihre Domänencontroller mit einer beträchtlichen CPU-Auslastung, die größer als 40 %, dies wird mit großer Wahrscheinlichkeit Rauschen NTP Antworten hinzufügen und Auswirkungen auf Ihre uhrzeitsynchronisierungsdienst in Ihrer Domäne.  In diesem Fall müssen Sie in Ihrer Umgebung die tatsächlichen Ergebnisse zu testen.

## <a name="time-accuracy-measurements"></a>Zeit Genauigkeitsmessungen
### <a name="methodology"></a>Methodik
Um die Genauigkeit der Zeit für Windows Server 2016 zu messen, haben wir eine Vielzahl von Tools, Methoden und Umgebungen verwendet werden.  Sie können diese Techniken verwenden, zu messen und Optimieren Ihrer Umgebung und zu bestimmen, ob der genauigkeitsergebnisse Ihre Anforderungen zu erfüllen. 

Unsere Domäne Quelle Uhr Bestand aus zwei NTP-Server mit hoher Genauigkeit mit GPS-Hardware.  Auch verwendet einen separaten Verweis Testcomputer für, das auch hohe Genauigkeit GPS-Hardware, die eines anderen Herstellers installiert wurde.  Für einige der Tests benötigen Sie eine präzise und verlässliche Taktquelle als Referenz zusätzlich zu Ihrer Domäne Taktquelle verwenden.

Wir haben vier verschiedene Methoden zum Messen der Genauigkeit mit sowohl physischen und virtuellen Computern verwendet. Mehrere Methoden bereitgestellt, unabhängige Möglichkeit, die Ergebnisse zu überprüfen.


1. Messen Sie die lokale Uhr, die von w32tm abhängig ist, für unseren Test-Referenzcomputer mit separaten GPS-Hardware.  
2.  Measure NTP-Ping-Nachrichten aus dem NTP-Server an Clients, die mithilfe von W32tm "Stripchart"
3.  Measure NTP-Ping-Nachrichten vom Client mit dem NTP-Server mithilfe von W32tm "Stripchart"
4.  Measure-Hyper-V führt zwischen dem Host und Gast mithilfe von Time Stamp Indikator (TSC).  Dieser Leistungsindikator wird zwischen Partitionen und die Systemzeit in beiden Partitionen gemeinsam genutzt.  Berechnet die Differenz zwischen dem Host und dem Client auf dem virtuellen Computer.  Klicken Sie dann verwenden wir im TSC-Format, um die Host-Zeit zwischen dem Gast, da die Maße nicht zur gleichen Zeit ausfallen zu interpolieren.  Außerdem verwenden wir die TSV-Format Verzögerungen und Latenz auszuklammern in der API.

W32tm ist eine integrierte Funktion, aber die anderen Tools, die wir bei unseren Tests verwendet stehen für das Microsoft-Repository auf GitHub als open Source-für die Tests und die Nutzung.  Das WIKI auf das Repository enthält weitere Informationen, die beschreibt, wie Sie die Tools von Messungen durchführen.

> [https://github.com/Microsoft/Windows-Time-Calibration-Tools](https://github.com/Microsoft/Windows-Time-Calibration-Tools)

Die unten gezeigten Testergebnisse sind eine Teilmenge der Messungen, die wir in einer der testumgebungen vorgenommen.  Sie zeigen die Genauigkeit, die am Anfang der Time-Hierarchie, und der untergeordneten Domänenclient am Ende der Time-Hierarchie verwaltet werden.  Dies wird mit denselben Computern in einer Topologie für 2012-basiertes für den Vergleich verglichen.

### <a name="topology"></a>Topologie
Für den Vergleich haben wir sowohl ein Windows Server 2012 R2 und Windows Server 2016-basierte Topologie getestet.  Beide Topologien bestehen aus zwei physischen Hyper-V-Hostcomputer, die auf einen Windows Server 2016-Computer mit GPS-Uhr-Hardware installiert verweisen.  Jeder Host führt 3 Domäne eingebundenen Windows-Gäste, die gemäß der folgenden Topologie angeordnet sind.  Die Zeilen stellen dar, die Zeithierarchie aus, und die/den Transport, der verwendet wird.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology1.png)

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology2.png)

### <a name="graphical-results-overview"></a>Übersicht über die grafische Ergebnisse
Die folgenden beiden Diagramme stellen die Genauigkeit der Zeit für zwei bestimmte Elemente in einer Domäne, die anhand der oben genannten Topologie dar.  Jedes Diagramm zeigt sowohl die Windows Server 2012 R2 und 2016 Ergebnisse zusammen, die visuell, die Verbesserungen veranschaulicht.  Die Genauigkeit wurde measure aus auf dem Gastcomputer im Vergleich zu dem Host.  Die grafischen Daten stellt eine Teilmenge der gesamte Satz von Tests, die wir gemacht haben, und zeigt die besten Fall ungünstigsten Fall.  

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology3.png)

### <a name="performance-of-the-root-domain-pdc"></a>Leistung der PDC-Stammdomäne
Der Stamm-PDC ist mit dem Hyper-V-Host (mit VMIC) synchronisiert, Windows Server 2016 mit GPS-Hardware, die nachweislich sowohl genaue und stabil sein.  Dies ist eine wichtige Voraussetzung für die 1 ms-Genauigkeit, die als die grün schattierten Bereich dargestellt wird.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart1.png)

### <a name="performance-of-the-child-domain-client"></a>Leistung des untergeordneten Domäne-Clients
Der untergeordneten Domäne-Client wird an einen untergeordneten Domain Controller, PDC angefügt findet eine Kommunikation mit dem Stamm-PDC statt.  Es Zeit ist auch in der 1 ms-Anforderung.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart2.png)


### <a name="long-distance-test"></a>Ferngespräche Test
Das folgende Diagramm vergleicht 1 virtuelles Netzwerk-Hops auf 6 physischen Netzwerk-Hops mit Windows Server 2016.  Zwei Diagramme sind mit Transparenz, die sich überschneidenden Daten anzeigen voneinander gelegt.  Zunehmende Netzwerkhops bedeuten höhere Latenz und mehr Zeit abweichungen.  Das Diagramm ist, vergrößerten und dies der Fall ist die 1 ms-Begrenzungen, dargestellt durch den grünen Bereich ist größer.  Wie Sie sehen können, ist die Zeit immer noch innerhalb von 1 ms mit mehreren Hops.  Es wird sich negativ auf verlagert das veranschaulicht, ein Netzwerk Asymmetrie.  Natürlich unterscheidet sich jedes Netzwerk, und Messungen auf einer Vielzahl von Umgebungsfaktoren abhängen.

![Windows-Zeitdienst](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart3.png)

## <a name="BestPractices"></a>Bewährte Methoden für die genaue Zeitbestimmung
### <a name="solid-source-clock"></a>Solid Quelle Uhr
Ein Computer wird nur so gut wie die Quelle Uhr, die, der Sie mit synchronisiert wird.  Zum Erzielen von 1 ms der Genauigkeit, benötigen Sie GPS-Hardware oder eine Appliance für die Zeit in Ihrem Netzwerk, das Sie verweisen auf als die masterquelle Uhr.  Verwenden den Standardwert "Time.Windows.com", möglicherweise keine stabile und eine Ortszeit Quell-bereit.  Darüber hinaus, wie Sie die weiter vom Blickfokus entfernt die Uhr Quelle erhalten, wirkt sich auf das Netzwerk die Genauigkeit.  Eine Uhr masterquelle müssen in jeder Data Center für die der höchsten Genauigkeit erforderlich ist.

### <a name="hardware-gps-options"></a>Hardware-GPS-Optionen
Es gibt verschiedene hardwarelösungen, die genaue Uhrzeit bieten können.  Lösungen basieren im Allgemeinen noch heute auf GPS-Antennen.  Es gibt auch Radio und DFÜ-Modem-Lösungen, die mithilfe von dedizierten Zeilen.  Sie fügen Sie mit Ihrem Netzwerk entweder als eine Einheit oder an einem PC, z. B. Windows, über ein PCIe oder einem USB-Gerät anschließen.  Verschiedene Optionen liefert auf verschiedene Ebenen der Genauigkeit, und wie immer, hängen die Ergebnisse Ihrer Umgebung.  Variablen, die Genauigkeit beeinflussen enthalten GPS-Verfügbarkeit, Netzwerkstabilität und Last sowie PC-Hardware.  Dies sind alles wichtige Faktoren, wenn eine Uhr Quelle auswählen, die wie wir bereits erwähnt, eine Voraussetzung für die stabilen und genaue Uhrzeit ist.

### <a name="domain-and-synchronizing-time"></a>Domäne und die Zeit synchronisieren
Mitglieder der Domäne die Domänenhierarchie verwenden, um zu bestimmen, welche Computer sie als Quelle verwenden, um Zeit zu synchronisieren.  Jedes Mitglied der Domäne findet sich auf einem anderen Computer mit und speichern Sie sie als die-Uhr-Quelle zu synchronisieren.  Jeder Typ, der Mitglied der Domäne folgt einen anderen Satz von Regeln, um eine Taktquelle für die zeitsynchronisierung zu finden.  Der PDC im Stamm Gesamtstruktur ist die standardmäßige-Uhr-Quelle für alle Domänen.  Unten finden Sie verschiedene Rollen und allgemeine Beschreibung wie sie eine Quelle finden:


- **Domänencontroller mit dem PDC-Rolle** : Dieser Computer ist die zeitverwaltungsquelle für eine Domäne. Sie müssen in der Domäne die genaueste Zeit zur Verfügung und müssen mit einem Domänencontroller in der übergeordneten Domäne synchronisieren, außer in Fällen, in denen [GTIMESERV](#GTIMESERV) -Rolle ist aktiviert. 
- **Alle anderen Domänencontroller** : Dieser Computer fungiert als Zeitquelle für Clients und Servern in der Domäne. Ein Domänencontroller kann mit dem PDC ihrer eigenen Domäne oder einem beliebigen Domänencontroller in der übergeordneten Domäne synchronisieren.
- **Clients/Mitgliedsserver** : Dieser Computer kann mit jedem DC oder PDC seine eigene Domäne, oder ein Domänencontroller oder PDC in der übergeordneten Domäne synchronisieren.

Basierend auf den verfügbaren Kandidaten, wird ein Punktesystems verwendet, um die beste Zeitquelle zu finden.  Dieses System berücksichtigt die Zuverlässigkeit der Zeitquelle und den jeweiligen Speicherort.  Dies geschieht, wenn bei der Dienst wurde gestartet wird.  Wenn eine präzisere Kontrolle über Zeit wie synchronisiert werden sollen, können Sie Gelegenheit-Server an bestimmten Speicherorten hinzufügen oder Hinzufügen von Redundanz.  Finden Sie unter den [Geben Sie einen lokalen zuverlässige Zeit Service mithilfe von GTIMESERV](#GTIMESERV) Abschnitt, um weitere Informationen.

#### <a name="mixed-os-environments-win2012r2-and-win2008r2"></a>Gemischte OS-Umgebungen (Win2012R2 und Win2008R2)
Während eine reine Windows Server 2016-Domäne-Umgebung für die beste Genauigkeit erforderlich ist, stehen immer noch Vorteile in einer gemischten Umgebung.  Bereitstellen von Windows Server 2016 Hyper-V in einer Windows 2012-Domäne werden die Gäste aufgrund der Verbesserungen profitieren, die wir weiter oben erwähnt habe, aber Sie nur, wenn die Gäste auch Windows Server 2016 sind.  Ein Windows Server 2016-PDC kann genauer Zeitpunkt bereitstellen, aufgrund der optimierte Algorithmen für die Komponente wird eine stabilere Quelle.  Ersetzt Ihren PDC nicht möglicherweise eine Option, können Sie stattdessen ein Windows Server 2016-Domänencontroller mit Hinzufügen der [GTIMESERV](#GTIMESERV) Zurücksetzen der Reihe, die ein Upgrade mit einer Genauigkeit für Ihre Domäne im wäre.  Ein Windows Server 2016-Domänencontroller können downstream-zeitclients besseren Zeitpunkt bereitstellen, es ist jedoch nur so gut wie der Quelle NTP-Zeit.

Die Uhr abrufen und aktualisieren Sie die Häufigkeiten wurden geändert, wie bereits erwähnt, auch mit Windows Server 2016.  Diese können auf Ihre älteren DCs manuell geändert oder über die Gruppenrichtlinie angewendet.  Während wir die folgenden Konfigurationen getestet haben, sollten sie verhalten sich auch in Win2008R2 und Win2012R2 und einige Vorteile.

Versionen vor Windows Server 2016 musste eine mehrere Probleme, halten die genaue Zeit geführt hat das System Zeit, die bereits sofort, nachdem eine Änderung vorgenommen wurde.  Führt aus diesem Grund für das Abrufen von Stichproben aus einer genauen NTP-Quelle ist es häufig und Vorbereitung die lokale Uhr mit den Daten um kleinere abweichungen in ihrer Systemuhren innerhalb der interne sampling, was zu einer besseren Zeitpunkt, die auf älteren Versionen des Betriebssystems. Beobachtete Genauigkeit war ca. 5 ms, wenn ein Windows Server 2012 R2 NTP-Client, mit den Einstellungen hoher-Genauigkeit konfiguriert die Zeit von einem genauen Windows 2016 NTP-Server synchronisiert.

In einigen Szenarien im Zusammenhang mit Gast-Domänencontroller können Hyper-V-TimeSync Beispiele Domäne zeitsynchronisierung stören.  Dies sollte nicht mehr ein Problem für Server 2016-Gäste, die auf Server 2016 Hyper-V-Hosts ausgeführt werden.

Um den Hyper-V-TimeSync-Dienst von der Bereitstellung von Beispiele zum w32time zu deaktivieren, legen Sie den folgenden Registrierungsschlüssel für den Gast:

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider 
    "Enabled"=dword:00000000

#### <a name="AllowingLinux"></a>Zulassen von Linux verwendet, um die Hyper-V-Host verwenden
Für Linux-Gäste in Hyper-V ausgeführt wird sind Clients in der Regel verwenden Sie den NTP-Daemon für die zeitsynchronisierung für NTP-Server konfiguriert.  Wenn der Linux-Distribution das Protokoll, Version 4 TimeSync unterstützt und Linux-Gast des TimeSync Integration-Diensts aktiviert, werden sie mit dem Host Zeitpunkt synchronisiert. Dies kann zu inkonsistenten Zeit beibehalten werden, wenn beide Methoden aktiviert sind.

Um ausschließlich mit dem Host Zeitpunkt zu synchronisieren, wird empfohlen, deaktivieren Sie die NTP-zeitsynchronisierung entweder:

- Deaktivieren alle NTP-Server in der Datei "ntp.conf"
- oder deaktivieren den NTP-daemon

In dieser Konfiguration ist der Zeitserver-Parameter dieses Hosts.  Die Häufigkeit abrufen beträgt 5 Sekunden und der Update-Taktfrequenz auch 5 Sekunden.

Um ausschließlich über NTP zu synchronisieren, wird empfohlen, den TimeSync Integration-Dienst auf dem Gast zu deaktivieren.

> [!NOTE]
> Hinweis:  Unterstützung für die genaue Uhrzeit mit Linux-Gäste ist erforderlich, ein Feature, das nur in den letzten upstream Linux-Kernel unterstützt wird, und es ist nicht allgemein verfügbar für alle Linux-Distributionen noch ist. Verweisen Sie auf [unterstützt Linux und FreeBSD-VMs für Hyper-V unter Windows](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows) ausführliche Informationen zur Unterstützung Verteilungen.

#### <a name="GTIMESERV"></a>Geben Sie einen lokalen zuverlässigen Zeitdienst mit dem GTIMESERV
Können Sie eine oder mehrere Domänencontroller als genaue Quelle Uhren angeben der GTIMESERV, gute Zeitserver mit flags.  Beispielsweise können bestimmte Domänencontroller ausgestattet mit GPS-Hardware als ein GTIMESERV gekennzeichnet.  Somit ist sichergestellt, dass Ihre Domäne eine Uhr basierend auf der Hardware GPS verweist.

> [!NOTE]
> Weitere Informationen zu den Flags der Domäne befinden sich die [MS-ADTS Protokoll Dokumentation](https://msdn.microsoft.com/library/mt226583.aspx).

TIMESERV ist eine andere verknüpfte Domäne Services-Flag das angibt, ob ein Computer aktuell autorisierend ist, die es ändern können, wenn die Verbindung ein Domänencontrollers verliert.  Einem Domänencontroller in diesem Zustand wird "Unbekannter Stratum" bei Abfragen über NTP zurückgegeben.  Nach mehreren versuchen, wird der DC System Event Zeitdienst Ereignis 36 protokolliert.

Wenn Sie einen Domänencontroller als eine GTIMESERV konfigurieren möchten, kann dies manuell mit dem folgenden Befehl konfiguriert werden.  In diesem Fall wird der DC einen anderen Computer als die master-Uhrzeit verwendet.  Dies kann ein Gerät oder einen dedizierten Computer sein.

    w32tm /config /manualpeerlist:”master_clock1,0x8 master_clock2,0x8” /syncfromflags:manual /reliable:yes /update

> [!NOTE]
> Weitere Informationen finden Sie unter [Konfigurieren der Windows-Zeitdienst](https://technet.microsoft.com/library/cc731191.aspx)

Wenn der Domänencontroller die GPS-Hardware installiert wurde, müssen Sie mithilfe dieser Schritte den NTP-Client deaktivieren und aktivieren Sie den NTP-Server.

Durch das Deaktivieren der NTP-Client starten Sie, und aktivieren Sie den NTP-Server, die mit diesen Änderungen des Registrierungsschlüssels.

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpClient /v Enabled /t REG_DWORD /d 0 /f

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpServer /v Enabled /t REG_DWORD /d 1 /f

Starten Sie dann den Windows-Zeitdienst neu.

    net stop w32time && net start w32time

Abschließend geben Sie an, dass eine zuverlässige Quelle mithilfe des Computers ist.
   
    w32tm /config /reliable:yes /update

Um zu überprüfen, dass die Änderungen ordnungsgemäß ausgeführt wird, können Sie die folgenden Befehle ausführen, die unten angegebenen Ergebnisse beeinflussen. 

    w32tm /query /configuration

Wert|Erwarteten Einstellung|
----- | ----- |
AnnounceFlags|  5 (lokal)|
NtpServer   |(Lokal)|
DllName |C:\WINDOWS\SYSTEM32\w32time.DLL (Local)|
Enabled |1 (lokal)|
NtpClient|  (Lokal)|

    w32tm /query /status /verbose

Wert|  Erwarteten Einstellung|
----- | ----- |
Stratum|    1 (primäre Referenz - Synchr. durch Radio Uhr)|
ReferenceId|    0x4C4F434C (Name der Datenquelle:  "LOCAL")|
Source| Lokale CMOS-Uhr|
Phase Offset|   0.0000000s|
Serverrolle|    576 (zuverlässigen Zeitdienst)|

#### <a name="windows-server-2016-on-3rd-party-virtual-platforms"></a>WindowsServer 2016 in 3rd Party virtuellen Plattformen
Windows virtualisiert ist, ist der Hypervisor standardmäßig für die Bereitstellung Zeit verantwortlich.  Aber Domäne Member muss synchronisiert mit dem Domänencontroller in der Reihenfolge für die Active Directory ordnungsgemäß funktioniert.  Es wird empfohlen, alle Virtualisierung Zeit zwischen dem Gast und Host alle 3. Partei virtuellen Plattformen deaktivieren.

#### <a name="discovering-the-hierarchy"></a>Ermitteln die Hierarchie
Da die Kette der Time-Hierarchie mit der master-Uhrzeit-Quelle in einer Domäne dynamisch und ausgehandelten ist, müssen Sie Abfragen des Status eines bestimmten Computers zu verstehen, dass es sich um Zeitquelle "und" Chain ", um die Uhr masterquelle handelt.  Dies kann helfen, Probleme bei der Synchronisierung von Zeit zu diagnostizieren.

Bei der Sie einen bestimmten Client; Problembehandlung durchführen möchten, der erste Schritt ist, dessen Zeitquelle, die mit diesem Befehl w32tm zu verstehen.

    w32tm /query /status

Die Ergebnisse zeigen die Quelle, unter anderem.  Die Quelle Gibt an, mit denen Sie die Zeit in der Domäne synchronisieren.  Dies ist der erste Schritt von diesem Computer Time-Hierarchie.
Als Nächstes verwenden Sie Eintrag der Quelle von oben, und verwenden Sie die /StripChart-Parameter, um die nächste Zeitquelle finden Sie in der Kette.

    w32tm /stripchart /computer:MySourceEntry /packetinfo /samples:1

Auch nützlich, der folgende Befehl listet jeden Domänencontroller, die in der angegebenen Domäne gefunden werden kann und druckt ein Ergebnis für jeden Partner bestimmen können.  Mit diesem Befehl werden Computer enthalten, die manuell konfiguriert wurden.
    
    w32tm /monitor /domain:my_domain

Mithilfe der Feldliste können Sie verfolgen die Ergebnisse über die Domäne und verstehen, die Hierarchie als auch für den Zeitversatz bei jedem Schritt.  Suchen Sie den Punkt, in dem das Zeitoffset erheblich schlimmer wird, können Sie den Stamm der falsche Zeit festlegen.  Von dort aus können Sie versuchen, zu verstehen, warum dieser Zeit falsch ist, indem einschalten [w32tm Protokollierung](#W32Logging). 

#### <a name="using-group-policy"></a>Mithilfe von Gruppenrichtlinien
Sie können mithilfe einer Gruppenrichtlinie zum Ausführen von strengere Genauigkeit durch, z. B. Zuweisen von Clients auf bestimmte NTP-Server verwenden oder Steuerelement wie kompatible Betriebssysteme konfiguriert werden, wenn virtualisiert.  
Im folgenden finden Sie eine Liste der möglichen Szenarien und entsprechenden Gruppenrichtlinien-Einstellungen:

**Virtualisierte Domänen** - um die virtualisierte Domänencontroller in Windows 2012 R2 zu steuern, sodass sie die Uhrzeit mit der Domäne synchronisieren, statt mit dem Hyper-V-Host können Sie diesen Registrierungseintrag deaktivieren.   Für den PDC möchten nicht den Eintrag deaktivieren, wie Hyper-V-Hosts die stabile Zeitquelle übermittelt.  Der Registrierungseintrag erfordert, dass Sie nach der Änderung den w32time-Dienst neu starten.

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider]
    "Enabled"=dword:00000000

**Genauigkeit vertrauliche lädt** – für vertrauliche arbeitsauslastungen der Uhrzeit-Genauigkeit, konnte Sie Gruppen von Computern, legen Sie die NTP-Server konfigurieren, und alle zugehörigen Uhrzeiteinstellungen, wie z. B. Abruf "und" Clock Häufigkeit aktualisiert.  Dies erfolgt normalerweise durch die Domäne, jedoch mehr Kontrolle können Sie bestimmte fest zugeordnete Computer direkt auf die master-Uhrzeit verweisen abzielen.

Gruppenrichtlinieneinstellung|   Neuer Wert|
----- | ----- |
NtpServer|  ClockMasterName,0x8|
MinPollInterval|    6 – 64 Sekunden|
MaxPollInterval|    6|
UpdateInterval| 100 – einmal pro Sekunde|
EventLogFlags|  3 – alle speziellen Anmeldung|

> [!NOTE]
> Die Einstellungen für NtpServer und EventLogFlags befinden sich unter Serverbasisbetriebssystem\Windows Zeit Service\Time Anbieter mit den Einstellungen für Windows NTP-Client konfigurieren.  Die anderen 3 befinden sich unter Serverbasisbetriebssystem\Windows Zeitdienst mit dem die globalen Konfigurationseinstellungen.

**Remote Genauigkeit vertrauliche lädt Remote** – für Systeme in Branch Domänen für Retail-Instanz und der Zahlung Guthaben Industry (PCI), Windows verwendet die aktuellen Informationen und Domänencontrollerlocator Suche nach einem lokalen Domänencontroller, es sei denn, es eine manuelle NTP ist Zeitquelle konfiguriert.  Diese Umgebung erfordert 1 Sekunde der Genauigkeit, die schnellere Konvergenz auf die richtige Uhrzeit verwendet.  Diese Option ermöglicht den w32time-Dienst, um die Uhr rückwärts zu bewegen.  Wenn dies zulässig ist und Ihre Anforderungen erfüllt, können Sie die folgende Richtlinie erstellen.   Wie bei jeder Umgebung stellt sicher, Test und Baseline Ihres Netzwerks. 

Gruppenrichtlinieneinstellung|   Neuer Wert|
----- | ----- |
MaxAllowedPhaseOffset|  1, stellen Wenn mehr als am zweiten, Uhr zum richtigen Zeitpunkt.|

Die Einstellung Max. zugelassener Phasenoffset befindet sich unter Serverbasisbetriebssystem\Windows Zeitdienst mit dem die globalen Konfigurationseinstellungen.

> [!NOTE]
> Weitere Informationen zu Gruppenrichtlinien und verwandte Einträge, finden Sie unter [Windows-Zeitdienst: Tools](windows-time-service-tools-and-settings.md) und Einstellungen Artikel auf TechNet.

## <a name="azure-and-windows-iaas-considerations"></a>Überlegungen zu Azure und Windows-IaaS

### <a name="azure-virtual-machine-active-directory-domain-services"></a>Virtueller Azure-Computer: Active Directory Domain Services
Die Azure-VM, die mit der Active Directory Domain Services ist Teil einer vorhandenen lokalen sollte Active Directory-Gesamtstruktur, klicken Sie dann TimeSync(VMIC), deaktiviert werden. Dies ist auf allen Domänencontrollern in der Gesamtstruktur, physischen und virtuellen, mit einer einzelnen Synchronisierung Zeithierarchie zu ermöglichen. Finden Sie in der best Practice-Whitepaper ["Ausführen von Domain Controller in Hyper-V"](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx)

### <a name="azure-virtual-machine-domain-joined-machine"></a>Virtueller Azure-Computer: Domäne eingebundener Computer
Wenn Sie einen Computer, der Domäne, die mit einer vorhandenen Active Directory-Gesamtstruktur verknüpft ist hosten, ist virtuell oder physisch, die bewährte Methode, TimeSync für das Gastbetriebssystem zu deaktivieren, und stellen Sie sicher, dass W32Time konfiguriert ist, um mit seinen Domänencontroller über das Konfigurieren von Zeit zu synchronisieren Typ = NTP5

### <a name="azure-virtual-machine-standalone-workgroup-machine"></a>Virtueller Azure-Computer: Eigenständige Arbeitsgruppencomputer
Wenn der Azure-VM ist nicht mit einer Domäne verknüpft, noch er ein Domänencontroller ist, wird empfohlen, die Standardkonfiguration für die Zeit beibehalten und den virtuellen Computer mit dem Host zu synchronisieren.

## <a name="windows-application-requiring-accurate-time"></a>Windows-Anwendung, die erfordern genaue Uhrzeit
### <a name="time-stamp-api"></a>Zeitstempel-API
Programme, die die größte Genauigkeit im Hinblick auf die UTC-Zeit und nicht den zeitlichen Verlauf, erfordern sollten verwenden die [GetSystemTimePreciseAsFileTime API](https://msdn.microsoft.com/library/windows/desktop/Hh706895.aspx).  Dadurch wird sichergestellt, dass Ihre Anwendung die Systemzeit, ruft die von der Windows-Zeitdienst abhängig ist.

### <a name="udp-performance"></a>UDP-Leistung
Wenn Sie eine Anwendung, verwendet UDP-Kommunikation für Transaktionen und es ist wichtig, das Minimieren der Latenzzeit können stehen einige zugehörige Einträge in der Registrierung können Sie einen Bereich der Ports, die ausgeschlossen werden soll, konfigurieren, das die Basis-Engine-Filterung port haben.  Dies verbessert die Latenz und den Durchsatz zu erhöhen.  Allerdings sollten Änderungen an der Registrierung auf erfahrene Administratoren beschränkt werden.  Darüber hinaus schließt diese problemumgehung Ports aus, die von der Firewall geschützt wird.  Finden Sie im Artikel unten Weitere Informationen.

Für Windows Server 2012 und Windows Server 2008 müssen Sie zuerst einen Hotfix zu installieren.  Sie können diesem KB-Artikel verweisen: [Wenn Sie eine multicast-empfängeranwendung in Windows 8 und Windows Server 2012 ausführen-datagrammverlust](https://support.microsoft.com/kb/2808584)

### <a name="update-network-drivers"></a>Aktualisieren Sie die Netzwerktreiber
Einige Anbieter Netzwerk haben Treiberupdates kann die Leistung im Hinblick auf Latenz der Treiber und UDP-Pakete Pufferung verbessert.  Wenden Sie sich an den Netzwerk-Anbieter, um festzustellen, ob Updates, um UDP-Durchsatz zu unterstützen.

## <a name="logging-for-auditing-purposes"></a>Protokollierung für Überwachungszwecke
Um Zeit Ablaufverfolgung Vorschriften können Sie manuell w32tm Protokolle, Ereignisprotokolle und systemmonitorinformationen archivieren.  Die archivierte Informationen kann später verwendet werden, Kompatibilität, zu einem bestimmten Zeitpunkt in der Vergangenheit zu bestätigen.  Die folgenden Faktoren werden verwendet, um die Genauigkeit anzugeben.


1. Clock-Genauigkeit bei Verwendung des Systemmonitors Zeitversatz berechnet.  Dies zeigt die Uhr, mit der gewünschten Genauigkeit.
2.  Taktquelle "Peerantwort" in den Protokollen w32tm gesucht.   Hinter dem Nachrichtentext ist, die IP-Adresse oder den VMIC, die die Datenquelle für die Zeit und die nächste in der Kette von Verweis Uhren überprüft beschreibt.
3.  Clock-Bedingung-Status, die mithilfe der w32tm-Protokolle zu überprüfen, ob "ClockDispl Disziplin: \*NEIGEN\*Zeit\*"auftreten.  Dies gibt an, dass diese w32tm zur Zeit aktiv ist.

### <a name="event-logging"></a>Protokollierung von Komponentenereignissen
Um die ganze Geschichte zu erhalten, benötigen Sie auch Sicherheitsereignis-Protokollinformationen.  Durch das Sammeln von Systemereignisprotokoll Zeitserver filtern und, Microsoft-Windows-Kernel-Boot, Microsoft-Windows-Kernel-Allgemein "", Sie möglicherweise zu ermitteln, ob es gibt andere beeinflusst, die die Zeit, z. B. Drittanbieter geändert haben.  Diese Protokolle möglicherweise erforderlich, um externe Störungen auszuschließen.  Gruppenrichtlinien kann Auswirkungen auf die Ereignisprotokolle in das Protokoll geschrieben werden.  Weitere Informationen finden Sie im oben stehenden Abschnitt auf mithilfe von Gruppenrichtlinien.

### <a name="W32Logging"></a>W32Time-Debugprotokollierung
Um w32tm zu Überwachungszwecken zu aktivieren, aktiviert der folgende Befehl die Protokollierung, die zeigt die regelmäßige Updates an der Uhr, und gibt Sie an der Quelle Uhr.  Starten Sie den Dienst aus, um die neue Protokollierung zu aktivieren.  

Weitere Informationen finden Sie unter [Informationen zum Aktivieren von Debug-Protokollierung in der Windows-Zeitdienst](https://support.microsoft.com/kb/816043).

    w32tm /debug /enable /file:C:\Windows\Temp\w32time-test.log /size:10000000 /entries:0-73,103,107,110

### <a name="performance-monitor"></a>Performance Monitor (Leistungsüberwachung)
Der Windows Server 2016-Windows-Zeitdienst-Dienst verfügbar macht, Leistungsindikatoren, die verwendet werden kann, um die Protokollierung für die Überwachung zu sammeln.  Diese können lokal oder Remote protokolliert werden.  Sie können die Computer Zeitversatz Roundtrip Verzögerung Indikatoren und aufzeichnen.  
Und wie alle Leistungsindikatoren können Sie sie per Remotezugriff zu überwachen und erstellen Sie Warnungen mithilfe von System Center Operations Manager.  Sie können z. B. eine Warnung verwenden, auf Sie alarm, wenn der Offset der Zeit, die aus der gewünschten Genauigkeit abweicht.  Die [System Center Management Pack](https://social.technet.microsoft.com/wiki/contents/articles/15251.system-center-management-pack-authoring-guide.aspx) finden Sie weitere Informationen.

### <a name="windows-traceability-example"></a>Beispiel für die nachverfolgung von Windows
Aus den Protokolldateien w32tm sollten Sie zwei Angaben zu überprüfen.  Die erste ist ein Hinweis, dass die Protokolldatei aktuell Bedingung Uhr ist.  Dies beweisen, dass die Uhr die Aufgabe, strittigen zum Zeitpunkt von der Windows-Zeitdienst bedingte wird wurde.

    151802 20:18:32.9821765s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:223 CR:156250 UI:100 phcT:65 KPhO:14307
    151802 20:18:33.9898460s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:64 KPhO:41
    151802 20:18:44.1090410s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:65 KPhO:38

Der wichtigste Aspekt ist, dass Nachrichten, die mit dem Präfix ClockDispln Disziplin Proof w32time wird die Systemuhr interagieren wird angezeigt.
 
Als Nächstes müssen Sie im Protokoll den letzten Bericht vor dem Zeitpunkt der Aufgabe, strittigen finden, das den Quellcomputer meldet der aktuell, als der Uhr des Verweises verwendet wird.  Dies kann sein, eine IP-Adresse, Name des Computers oder der VMIC-Anbieter, der angibt, dass es mit dem Hyper-V-Host synchronisiert wird.  Im folgenden Beispiel wird eine IPv4-Adresse des 10.197.216.105.

    151802 20:18:54.6531515s - Response from peer 10.197.216.105,0x8 (ntp.m|0x8|0.0.0.0:123->10.197.216.105:123), ofs: +00.0012218s

Nun, dass Sie das erste System in der Referenz-Time-Kette validiert haben, müssen Sie untersuchen die Protokolldatei auf Verweis Zeitquelle, und wiederholen die gleichen Schritte aus.  Dieser Vorgang wird fortgesetzt, bis Sie auf einer physischen Uhr, wie z. B. GPS- oder eine bekannte Zeitquelle wie NIST.  Ist die Referenzuhr-GPS-Hardware, können Protokolle von der produzierten auch erforderlich sein.

## <a name="network-considerations"></a>Überlegungen zu Netzwerken
Die NTP-Protokoll-Algorithmen setzen voraus, auf die Symmetrie Ihres Netzwerks.  Wenn Ihre steigt die Anzahl der Netzwerkhops nimmt auch die Wahrscheinlichkeit Asymmetrie.  Es ist es, schwer vorherzusagen, welche Arten von genauigkeiten in Ihre spezifischen Umgebungen angezeigt werden. 

Systemmonitor und die neuen Windows-Uhrzeit-Indikatoren in Windows Server 2016 können Ihre Umgebungen Genauigkeit bewerten, und Erstellen von Konfigurationsbasislinien verwendet werden. Darüber hinaus können Sie die Problembehandlung, um zu bestimmen, den aktuellen Offset von einem beliebigen Computer in Ihrem Netzwerk durchführen.

Es gibt zwei allgemeine Standards für die genaue Zeit über das Netzwerk ein.  PTP ([Genauigkeit Time Protocol - IEEE-1588](https://www.nist.gov/el/intelligent-systems-division-73500/introduction-ieee-1588)) hat strengere Anforderungen auf die Netzwerkinfrastruktur, aber untergeordnete Mikrosekunde Genauigkeit kann häufig bereitstellen.  NTP ([Network Time Protocol – RFC 1305](https://tools.ietf.org/html/rfc1305)) funktioniert auf eine größere Vielzahl von Netzwerken und Umgebungen, wodurch es einfacher zu verwalten. 

Windows unterstützt einfache NTP (RFC2030) wird standardmäßig nicht in die Domäne eingebundenen Computer an.  Für in die Domäne eingebundene Computer verwenden wir eine sichere NTP namens [MS-SNTP](https://msdn.microsoft.com/library/cc246877.aspx), die Domäne, die ausgehandelte Kennwörter verwendet, die Geben Sie einen Management-Vorteil gegenüber authentifiziert NTP RFC1305 und RFC5905 beschriebenen nutzt.   

Sowohl domänenbezogene als auch nicht in die Domäne eingebundenen Protokolle müssen UDP-Port 123.  Weitere Informationen zu bewährten Methoden für NTP finden Sie unter [Netzwerk Zeit Protokoll bewährte aktuelle Methoden IETF Draft](https://tools.ietf.org/html/draft-ietf-ntp-bcp-00).

### <a name="reliable-hardware-clock-rtc"></a>Zuverlässige Hardware-Uhr (RTC)
Windows ist nicht mit Schritt Zeit, wenn bestimmte Grenzen überschritten werden, jedoch eher bestraft die Uhr.  Das bedeutet, dass es sich bei w32tm in regelmäßigen Abständen, mithilfe der Update-Taktfrequenz festlegen, die standardmäßig einmal pro Sekunde unter Windows Server 2016 wird die Häufigkeit der Uhr angepasst.  Wenn die Uhr hinter befindet, wird er beschleunigt die Häufigkeit und ist es nun, es langsamer die Häufigkeit.  Allerdings ist die Hardware-Uhr während dieser Zeit zwischen Uhr Häufigkeit Anpassungen im Steuerelement.  Liegt ein Problem mit der Firmware oder Hardware-Uhr, kann die Uhrzeit auf dem Computer weniger genau ausfallen.

Dies ist ein weiterer Grund, die, den Sie testen möchten, und der Baseline in Ihrer Umgebung.  Wenn Sie der Leistungsindikator "Zeitversatz berechnet" nicht auf die Genauigkeit Zeitraums stabilisiert wird, die Sie verwenden möchten, empfiehlt es sich möglicherweise um sicherzustellen, dass die Firmware auf dem neuesten Stand ist.  Einen weiteren Test aus sehen Sie, ob doppelter Hardware das gleiche Problem reproduzieren.

### <a name="troubleshooting-time-accuracy-and-ntp"></a>Problembehandlung bei der Genauigkeit der Zeit und NTP
Sie können das Ermitteln von der Hierarchie-Abschnitt oben, um die falsche Systemzeit ermitteln.  Betrachten den Offset der Zeit, suchen Sie die Punkt in der Hierarchie, in dem Zeit am häufigsten von der NTP-Quelle abweicht.  Wenn Sie die Hierarchie verstehen, sollten Sie testen und zu verstehen, warum dieser bestimmte Zeitquelle keine genaue Uhrzeit erhält.  

Konzentriert sich auf das System mit voneinander abweichende Zeit und können diese folgenden Tools Sie zum Sammeln von Informationen können Sie das Problem zu bestimmen und eine Lösung zu finden.  Die folgenden UpstreamClockSource-Verweis ist es sich um die Uhr, die mithilfe von "w32tm/config/Status".


- System-Ereignisprotokolle
- Die Protokollierung unter: w32tm-Logs - w32tm/Debug/Enable / /file:C:\Windows\Temp\w32time-test.log /size:10000000 /entries:0-300
- w32Time-Registrierungsschlüssel HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time
- Lokales Netzwerk-ablaufverfolgungen
- Leistungsindikatoren (aus dem lokalen Computer oder die UpstreamClockSource)
- W32tm /stripchart /computer:UpstreamClockSource
- PING UpstreamClockSource zu Latenz und Anzahl der Hops an Quelle
- Tracert UpstreamClockSource

Problem|    Symptome|   Auflösung|
----- | ----- | ----- |
Lokale TSC-Uhr ist nicht stabil.| Perfmon - physische Computer – Sync Uhr stable-Format, aber immer noch angezeigt, alle 1-2 Minuten von mehreren 100us. |   Aktualisieren der Firmware oder Überprüfen anderer Hardware wird nicht das gleiche Problem angezeigt.|
Netzwerklatenz|    W32tm Stripchart zeigt eine RoundTripDelay von mehr als 10 ms.  Bei der Verzögerung dazu führen, dass Störungen, die so groß wie ½, der die Roundtripzeit, z. B. eine Verzögerung, die nur in einer Richtung ist.</br></br>UpstreamClockSource wird mehrere Hops an, wie durch PING angezeigt.  Gültigkeitsdauer (TTL) sollte in der Nähe 128 sein.</br></br>Verwenden Sie "tracert", um die Latenz bei jedem Hop zu ermitteln.    | Finden Sie eine genauere Taktquelle Zeit.  Eine Lösung ist zum Installieren von einer Quelle Uhr auf dem gleichen Segment oder manuell für Quelle Uhr, die geografisch näher liegt.  Fügen Sie einen Computer mit der Rolle GTimeServ für ein Szenario Domäne hinzu. |  
Kann nicht zuverlässig die NTP-Quelle zu erreichen|    W32tm /stripchart zurückgegeben zeitweise "Timeout für Anforderung".    |NTP-Quelle nicht reaktionsfähig ist.|
NTP-Quelle nicht reaktionsfähig ist.|    Überprüfen Sie Perfmon-Leistungsindikatoren für ausgehende Antworten von NTP Client Quellenanzahl, die eingehende Anforderungen der NTP-Server, NTP-Server aus, und ermitteln Sie Ihre Nutzung im Vergleich zu Ihrer Baselines zu.|    Verwenden Server-Leistungsindikatoren, bestimmt, ob Load in Bezug auf Ihre Basispläne geändert hat.</br></br>Gibt es Netzwerk Probleme bei der netzwerküberlastung?|
Domänencontroller, die nicht über die genaueste Uhr|    Änderungen in der Topologie oder die zuletzt hinzugefügte master Uhrzeit-Format.|   w32tm /resync /rediscover|
Clientuhren sind bereits.| Zeitdienst Ereignis 36 in das Systemereignisprotokoll und/oder Text in die Protokolldatei, die beschreibt, die: "NTP Client Zeit Quellenanzahl" Zähler, die Umstellung von 1 auf 0|Problembehandlung bei der upstreamquelle und verstehen Sie, wenn sie Probleme mit der Leistung ausgeführt wird.|

### <a name="baselining-time"></a>Basislinienüberwachung mit zwei Mal
Basislinienüberwachung mit zwei ist wichtig, sodass zuerst, erkennen Sie die Leistung und Genauigkeit des Netzwerks, und Vergleichen mit der Basislinie in der Zukunft auf, wenn Probleme auftreten.  Möchten Sie Baseline des Stamms-PDC, oder alle Computer, die mit der GTIMESRV markiert.  Auch wird der Baseline der PDC in jeder Gesamtstruktur empfohlen.  Wählen Sie zum Schluss alle kritischen DCs und dem angegebenen Computer, die interessante Eigenschaften wie Abstand oder hoher Auslastung und die Baseline haben diese.

Es ist auch nützlich, um die Baseline Windows Server 2016 und 2012 R2, jedoch nur w32tm /stripchart als Tool haben, die Sie für den Vergleich, da Windows Server 2012 R2-Leistungsindikatoren nicht verwenden können.  Sie wählen zwei Computer mit den gleichen Eigenschaften, oder aktualisieren ein Computers, und vergleichen Sie die Ergebnisse nach dem Update.  Weitere Informationen zur Vorgehensweise finden Sie ausführliche Messungen zwischen den 2016 und 2012 aufweist der Windows-Zeitmaßeinheiten Nachtrag

Sammeln von Daten verwenden, die alle w32time Leistungsindikatoren, für mindestens eine Woche.  Somit ist sichergestellt, dass Sie genug einen Verweis auf die verschiedenen im Netzwerk im Laufe der Zeit berücksichtigen und eine Ausführung zu vertrauen, dass Ihre uhrzeitsynchronisierungsdienst stabil genug.

### <a name="ntp-server-redundancy"></a>NTP Server Redundancy
Informationen zur manuellen NTP-Server-Konfiguration, die mit nicht in die Domäne eingebundene Computer oder den PDC verwendet ist mehr als einem Server ein Measure gute Redundanz bei Verfügbarkeit.  Es kann auch bieten eine höhere Genauigkeit, vorausgesetzt, dass alle Quellen genau und stabil sind.  Allerdings könnte, wenn die Topologie ist auch nicht ausgelegt, oder die Zeitquellen nicht stabil sind, die Genauigkeit des resultierenden noch schlimmer, sodass Vorsicht empfohlen wird.  Die maximal unterstützte Mal, wenn Server w32time manuell verweisen können, beträgt 10. 

## <a name="leap-seconds"></a>Schaltsekunden
Zeitraum für Kennwortrotation Erde hängt im Laufe der Zeit durch Klima und geological Ereignisse verursacht. In der Regel ist die Variation etwa eine Minute alle paar Jahre. Wenn die Abweichung von atomaren Zeit zu groß wird, ist eine Korrektur von einer Sekunde (nach oben oder unten) eingefügt, eine Schaltsekunde aufgerufen. Dies erfolgt so, dass die Differenz nie 0.9 Sekunden überschreitet. Diese Korrektur wird sechs Monate vor der tatsächlichen Korrektur angekündigt. Vor Windows Server 2016 der Microsoft-Zeitdienst war nicht bewusst Schaltsekunden allerdings setzt auf den externen Zeitdienst für diese Probleme zu umgehen. Microsoft arbeitet mit der Genauigkeit mehr Zeit von Windows Server 2016 an eine geeignetere Lösung des Problems Schaltsekunden verwendet wird.

## <a name="secure-time-seeding"></a>Sichern Sie die Zeit Seeding
W32Time in Server 2016 umfasst die sichere Zeit Seeding-Funktion. Diese Funktion bestimmt die aktuelle ungefähre ausgehende SSL-Verbindungen.  Dieses Zeitwerts dient zum Überwachen von der lokalen Systemuhr, und beheben Sie alle gross Fehler. Erfahren Sie mehr über das Feature in [in diesem Blogbeitrag](https://blogs.msdn.microsoft.com/w32time/2016/09/28/secure-time-seeding-improving-time-keeping-in-windows/).  Bei Bereitstellungen mit einer zuverlässigen Quellen und auch überwachte Computer, die Überwachung für Zeitoffsets, können Sie keine verwenden Secure Zeit Seeding und verlassen Sie sich stattdessen auf die vorhandene Infrastruktur. 

Sie können die Funktion mit den folgenden Schritten deaktivieren:

1.  Konfiguration den UtilizeSSLTimeData-Registrierungswert auf 0 festgelegt, für einen bestimmten Computer:

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\Config /v UtilizeSslTimeData /t REG_DWORD /d 0 /f


2.  Wenn Sie nicht sofort an irgendeinem Grund neu gestartet werden können, können Sie W32time-Dienst über die Aktualisierung der Konfiguration benachrichtigen. Dies beendet die Überwachung von Zeit und basierend auf Zeitdaten Erzwingung von SSL-Verbindungen erfasst. 

    W32tm.exe /config /update

3.  Neustarten des Computers, auch bewirkt, dass das Sammeln von SSL-Verbindungen von jedem Beenden und die Einstellung wird sofort wirksam wird.  Das letzte Teil verfügt über einen sehr kleinen Mehraufwand und sollte sich nicht auf die Leistung relevant.

4.  Um diese Einstellung in einer gesamten Domäne anzuwenden, legen Sie den UtilizeSSLTimeData-Wert in der W32time-gruppenrichtlinieneinstellung auf 0, und veröffentlichen Sie die Einstellung.  Wenn die Einstellung durch eine Gruppenrichtlinienclient ausgewählt wird, W32time-Dienst benachrichtigt, und wird angehalten, Zeit zu überwachen und erzwingen, die mithilfe von SSL-Time-Daten. Die SSL-Time-Datensammlung wird beendet, wenn es sich bei jedem Computer neu gestartet. Wenn Ihre Domäne portable slim Laptops/Tablets und anderen Geräten enthält, empfiehlt es sich, diese richtlinienänderung solche Computer ausgeschlossen werden sollen. Diese Geräte werden schließlich akkuentleerung konfrontiert, und müssen zum Bootstrapping ihrer Zeit die Funktion das sichere Zeit Seeding.


