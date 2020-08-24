---
ms.assetid: 72a90d00-56ee-48a9-9fae-64cbad29556c
title: Genaue Uhrzeit für Windows Server 2016
description: Die Genauigkeit der Zeitsynchronisierung in Windows Server 2016 wurde erheblich verbessert, während gleichzeitig die vollständige NTP-Abwärtskompatibilität mit älteren Windows-Versionen erhalten blieb.
author: dahavey
ms.author: dahavey
ms.date: 05/08/2018
ms.topic: article
ms.openlocfilehash: 82c4935adb10dea93a98c105191a52850b31ca42
ms.sourcegitcommit: b5b040a47cf48c94852de9aad8b91475f891d2f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88563320"
---
# <a name="accurate-time-for-windows-server-2016"></a>Genaue Uhrzeit für Windows Server 2016

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

Der Windows-Zeitdienst ist eine Komponente, die ein Plug-In-Modell für Client- und Serverzeit-Synchronisierungsanbieter verwendet.  Es gibt zwei integrierte Clientanbieter in Windows, und es sind Plug-Ins von Drittanbietern verfügbar. Ein Anbieter verwendet [NTP (RFC 1305)](https://tools.ietf.org/html/rfc1305) oder [MS-NTP](/openspecs/windows_protocols/ms-sntp/8106cb73-ab3a-4542-8bc8-784dd32031cc), um die lokale Systemzeit mit einem NTP- und/oder MS-NTP-kompatiblen Referenzserver zu synchronisieren. Der andere Anbieter ist für Hyper-V und synchronisiert virtuelle Computer (Virtual Machines, VM) mit dem Hyper-V-Host.  Wenn mehrere Anbieter vorhanden sind, wählt Windows den besten Anbieter aus, wobei das erste Kriterium die Stratumstufe ist, gefolgt von der Stammverzögerung, der Stammstreuung und schließlich der Zeitdifferenz.

> [!NOTE]
> Eine kurze Übersicht über den Windows-Zeitdienst findest du in diesem [Übersichtsvideo](https://aka.ms/WS2016TimeVideo).

In diesem Thema behandeln wir diese Themen, unter dem Aspekt, wie sie sich auf die Aktivierung einer exakten Zeit beziehen:

- Verbesserungen
- Messungen
- Empfehlungen

> [!IMPORTANT]
> Ein Nachtrag, auf den im Artikel „Windows 2016 – Genaue Uhrzeit“ verwiesen wird, kann [hier](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf) heruntergeladen werden.  In diesem Dokument findest du weitere Details zu unseren Test- und Messmethoden.

> [!NOTE]
> Das Windows-Zeitanbieter-Plug-In-Modell ist [auf TechNet dokumentiert](/windows/win32/sysinfo/time-provider).

## <a name="domain-hierarchy"></a>Domänenhierarchie
Domänen- und eigenständige Konfigurationen funktionieren unterschiedlich.

- Domänenmitglieder verwenden ein sicheres NTP-Protokoll, das Authentifizierung verwendet, um die Sicherheit und Authentizität der Zeitreferenz sicherzustellen.  Domänenmitglieder synchronisieren sich mit einer Masteruhr, die durch die Domänenhierarchie und ein Bewertungssystem bestimmt wird.  In einer Domäne gibt es eine hierarchische Schicht von Zeitstrata, bei denen jeder Domänencontroller (DC) einen übergeordneten DC mit einem präziseren Zeitstratum referenziert.  Die Hierarchie wird zum PDC oder einen DC in der Stammgesamtstruktur aufgelöst, oder zu einem DC mit dem Domänenkennzeichen GTIMESERV, das einen guten Zeitserver für die Domäne markiert.  Weitere Informationen findest du unten im Abschnitt „Angeben eines lokalen zuverlässigen Zeitdiensts mithilfe von GTIMESERV“.

- Eigenständige Computer sind so konfiguriert, dass sie standardmäßig „time.windows.com“ verwenden.  Dieser Name wird von deinem DNS-Server aufgelöst, der auf eine Ressource im Besitz von Microsoft verweisen sollte.  Wie alle Zeitreferenzen, die sich remote befinden, können Netzwerkausfälle die Synchronisierung verhindern.  Netzwerkdatenverkehrslasten und asymmetrische Netzwerkpfade können die Genauigkeit der Zeitsynchronisierung verringern.  Für eine Genauigkeit von 1 ms kann man nicht von Remotezeitquellen abhängig sein.

Da Hyper-V-Gästen mindestens zwei Windows-Zeitanbieter zur Auswahl stehen, die Hostzeit und NTP, kommt es eventuell zu unterschiedlichem Verhalten bei Domäne oder eigenständigem Computer, wenn die Ausführung als Gast erfolgt.

> [!NOTE]
> Weitere Informationen zur Domänenhierarchie und zum Bewertungssystem findest du im Blogbeitrag [„Was ist der Windows-Zeitdienst?“](/archive/blogs/w32time/what-is-windows-time-service) .

> [!NOTE]
> Stratum ist ein Konzept, das sowohl bei NTP- als auch bei Hyper-V-Anbietern verwendet wird, und dessen Wert den Standort der Uhr in der Hierarchie angibt.  Stratum 1 ist für die Uhr der höchsten Ebene reserviert, und Stratum 0 ist für die Hardware, die als exakt angesehen wird und nur wenig oder gar keine Verzögerung aufweist.  Stratum 2 kommuniziert mit Stratum 1-Servern, Stratum 3 mit Stratum 2 usw.  Obwohl ein niedrigeres Stratum häufig auf eine genauere Uhr hinweist, ist es möglich, Abweichungen zu finden.  Auch akzeptiert W32Time nur Zeiten von Stratum 15 oder niedriger.  Um das Stratum eines Clients anzuzeigen, verwende *w32tm /query /status*.

## <a name="critical-factors-for-accurate-time"></a>Kritische Faktoren für genaue Zeit
In jedem Fall gibt es drei kritische Faktoren für eine genaue Zeit:

1. **Stabile Quellenuhr**: Die Quellenuhr in deiner Domäne muss stabil und genau sein. Dies bedeutet in der Regel die Installation eines GPS-Geräts oder das Verweisen auf eine Stratum 1-Quelle, wobei Nr. 3 berücksichtigt wird. Die Analogie funktioniert wie folgt: Wenn du zwei Boote auf dem Wasser hast und versuchst, die Höhe des einen im Vergleich zum anderen zu messen, erhältst du die beste Genauigkeit, wenn das Quellboot sehr stabil und möglichst unbewegt ist. Dasselbe gilt für die Zeit, und wenn deine Quellenuhr nicht stabil ist, ist davon die gesamte Kette der synchronisierten Uhren betroffen, und die Auswirkungen verstärken sich auf jeder weiteren Stufe. Sie muss ferner erreichbar sein, weil Unterbrechungen der Verbindung die Zeitsynchronisierung stören. Und schließlich muss sie sicher sein. Wenn die Zeitreferenz nicht ordnungsgemäß aufrechterhalten oder von einer potenziell böswilligen Partei betrieben wird, könntest du deine Domäne eventuell zeitbasierten Angriffen aussetzen.
2. **Stabile Clientuhr**: Eine stabile Clientuhr gewährleistet, dass die natürliche Abweichung des Oszillators begrenzbar ist.  NTP verwendet mehrere Stichproben von potenziell mehreren NTP-Servern, um deine lokale Computeruhr zu regeln und zu stellen.  Dies stoppt nicht die Zeitänderungen, sondern verlangsamt oder beschleunigt eher die lokale Uhr, sodass eine schnelle Annäherung an die genaue Zeit erfolgt, und die Zeit zwischen NTP-Anforderungen exakt bleibt.  Wenn der Oszillator der Clientcomputeruhr jedoch nicht stabil ist, können mehr Fluktuationen zwischen Anpassungen auftreten, und die von Windows zum Regeln der Uhr verwendeten Algorithmen funktionieren dann nicht mehr exakt.  In einigen Fällen können Firmwareupdates erforderlich sein, um eine genaue Zeit zu erzielen.
3. **Symmetrische NTP-Kommunikation**: Es ist kritisch, dass die Verbindung für die NTP-Kommunikation symmetrisch ist.  NTP verwendet Berechnungen, um die Zeit anzupassen, bei denen vorausgesetzt wird, dass der Netzwerkpfad symmetrisch ist.  Wenn der Pfad, der vom NTP-Paket zum Server genommen wird, eine andere Dauer hat als der Rückweg, wird die Genauigkeit beeinträchtigt.  Beispielsweise könnte sich der Pfad aufgrund von Änderungen an der Netzwerktopologie ändern oder durch Pakete, die über Geräte weitergeleitet werden, die unterschiedliche Schnittstellengeschwindigkeiten aufweisen.

Bei akkubetriebenen Geräten, sowohl mobil als auch tragbar, musst du unterschiedliche Strategien in Erwägung ziehen.  Gemäß unserer Empfehlung erfordert die Aufrechterhaltung einer exakten Zeit, dass die Uhr einmal pro Sekunde reguliert wird, was mit der „Aktualisierungsrate der Uhr“ korreliert. Diese Einstellungen verbrauchen mehr Akkuleistung als erwartet und können den Energiesparmodus unter Windows für solche Geräte beeinträchtigen. Akkubetriebene Geräte verfügen auch über bestimmte Energiemodi, bei denen die Ausführung aller Anwendungen beendet wird, was die Fähigkeit von W32time beeinträchtigt, die Uhr zu regulieren und eine genaue Zeit aufrechtzuerhalten. Außerdem sind Uhren in mobilen Geräten möglicherweise grundsätzlich nicht sehr genau.  Umgebungsbedingungen wirken sich auf die Uhrgenauigkeit aus, und ein mobiles Gerät kann von einer Umgebungsbedingung zur nächsten wechseln, was seine Fähigkeit beeinträchtigen kann, die Zeit genauzuhalten.  Daher wird von Microsoft nicht empfohlen, akkubetriebene tragbare Geräte mit Einstellungen für hohe Genauigkeit zu betreiben.

## <a name="why-is-time-important"></a>Warum ist die Zeit wichtig?
Es gibt viele verschiedene Gründe, weshalb du eine genaue Zeit benötigen könntest.  Der typische Fall für Windows ist Kerberos, bei dem eine Genauigkeit von 5 Minuten zwischen Client und Server erforderlich ist.  Es gibt jedoch viele weitere Bereiche, die von der Zeitgenauigkeit betroffen sein können, dazu gehören:


- Behördliche Vorschriften wie:
    - Genauigkeit von 50 ms für FINRA in den USA
    - 1 ms ESMA (MiFID II) in der EU.
- Kryptografiealgorithmen
- Verteilte Systeme wie Cluster/SQL/Exchange und Document DBs
- Blockchain-Framework für Bitcoin-Transaktionen
- Verteilte Protokolle und Bedrohungsanalyse
- AD-Replikation
- Kartenzahlungsbranche (Payment Card Industry, PCI), zurzeit Genauigkeit von 1 Sekunde

## <a name="additional-references"></a>Weitere Verweise

- [Verbesserungen bei der Zeitgenauigkeit für Windows Server 2016](windows-server-2016-improvements.md)]