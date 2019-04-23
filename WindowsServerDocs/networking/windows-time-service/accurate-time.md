---
ms.assetid: 72a90d00-56ee-48a9-9fae-64cbad29556c
title: Genaue Uhrzeit für WindowsServer 2016
description: Synchronisierung uhrzeitsynchronisierungsdienst in Windows Server 2016 wurde erheblich, und gleichzeitig vollständige Abwärtskompatibilität NTP-Kompatibilität mit älteren Windows-Versionen verbessert.
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: ea4d957ee68f14f4568d3cefe664736585e50cce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864011"
---
# <a name="accurate-time-for-windows-server-2016"></a>Genaue Uhrzeit für WindowsServer 2016

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

Der Windows-Zeitdienst ist eine Komponente, die ein Plug-In-Modell für die Client- und Zeit Synchronisierungsanbieter verwendet.  Es gibt zwei integrierten Client-Anbieter für Windows und Drittanbieter-Plug-ins sind verfügbar. Ein Anbieter verwendet [NTP (RFC 1305)](https://tools.ietf.org/html/rfc1305) oder [MS-NTP](https://msdn.microsoft.com/library/cc246877.aspx) die lokalen Systemzeit mit einem NTP und/oder MS-NTP-kompatible Verweis-Server zu synchronisieren. Der andere Anbieter ist für Hyper-V und virtuellen Computern (VMs) mit dem Hyper-V-Host synchronisiert.  Wenn mehrere Anbieter vorhanden sind, wird Windows wählen Sie den besten-Anbieter zunächst mithilfe von Stratum Ebene gefolgt von Stamm-Verzögerung, Root-Verteilung, und endlich an Offset der Zeit.

>[!NOTE]
>Für eine kurze Übersicht über Windows-Zeitdienst, sehen Sie sich diese [auf hoher Ebene übersichtsvideo](https://aka.ms/WS2016TimeVideo).

<!-- Not sure what to do with the following -->
In diesem Thema wird erläutert... in diesen Themen im Zusammenhang mit den genaue Uhrzeit zu aktivieren: 

- Verbesserungen
- Messungen
- Empfehlungen

>[!IMPORTANT]
>Ein Nachtrag der Windows 2016 genau Zeit-Artikel kann heruntergeladen werden [hier](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf).  Dieses Dokument enthält weitere Details zu unseren Tests und Messungen-Methoden.



>[!NOTE] 
>Die Anbieter-Plug-in das Modell für Windows ist [auf TechNet-Website dokumentiert](https://msdn.microsoft.com/library/windows/desktop/ms725475%28v=vs.85%29.aspx).

## <a name="domain-hierarchy"></a>Domänenhierarchie
Domänen-und eigenständigen funktionieren unterschiedlich.

- Mitglieder der Domäne verwenden, ein sicheres NTP-Protokoll, das Authentifizierung verwendet, um sicherzustellen, dass die Sicherheit und die Authentizität des Verweises Zeit.  Mitglieder der Domäne, die mit einer master Uhr bestimmt, indem Sie die Domäne und eines Punktesystems synchronisiert werden.  In einer Domäne ist es eine hierarchische Ebene der Zeit Stratums, bei dem jeder Domänencontroller zu einem übergeordneten Element DC mit einer möglichst genauen Zeitpunkt Stratum verweist.  Die Hierarchie wird in den primären Domänencontroller oder ein Domänencontroller in der Root-Gesamtstruktur oder eines Domänencontrollers mit dem GTIMESERV Domäne-Flag, die kennzeichnet eine gute Zeit-Server für die Domäne aufgelöst werden.  Finden Sie unter den [Geben Sie einen lokalen zuverlässige Zeit Service mithilfe von GTIMESERV](#GTIMESERV) Abschnitt weiter unten.

- Eigenständige Computer werden standardmäßig konfiguriert, um "Time.Windows.com" zu verwenden.  Dieser Name wird vom DNS-Server aufgelöst, die auf einer Microsoft in Besitz befindliche Ressource verweisen soll.  Wie alle Remote-Standorten Uhrzeitangaben, Netzwerkausfällen, kann die Synchronisierung verhindern.  Lädt den Netzwerkverkehr und den asymmetrisch Netzwerkpfade reduzieren können die Genauigkeit der Synchronisierung.  Sie können nicht für 1 ms Genauigkeit einer remote-Zeitquellen abhängen.

Da Hyper-V-Gastbetriebssystemen über mindestens zwei Windows-Uhrzeit-Anbietern zur Auswahl hat, kann der Host-Zeit und NTP, unterschiedliche Verhaltensweisen mit Domäne oder eigenständige angezeigt, wenn als Gast ausgeführt.

> [!NOTE] 
> Weitere Informationen über die Domänenhierarchie und Punktesystems finden Sie unter den ["Was ist Windows-Zeitdienst?"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) .

> [!NOTE]
> Stratum ist ein Konzept, das sowohl die Hyper-V die NTP-Anbieter verwendet und der Wert gibt an, die Uhren der Position in der Hierarchie.  Stratum 1 ist für die oberste Uhr reserviert und Stratum 0 ist für die Hardware, die davon ausgegangen, dass genau reserviert und hat damit wenig oder keine Verzögerung zugeordnet.  Stratum 2 wenden Sie sich an Stratum 1-Servern, Stratum 3 auf Schicht 2 und so weiter.  Während eine untere Schicht häufig eine genauere Uhr angegeben wird, ist es möglich, um Unstimmigkeiten zu finden.  Darüber hinaus akzeptiert W32time nur Zeit von Stratum 15 oder unten.  Um die Stratum eines Clients anzuzeigen, verwenden *w32tm/Query/Status*.

## <a name="critical-factors-for-accurate-time"></a>Kritischen Faktoren für die genaue Uhrzeit
In jedem Fall nach der genauen Zeit gibt es drei wichtige Faktoren:

1. **Solid Quelle Uhr** -die Source-Uhr in Ihrer Domäne muss stabil und genau ist. Dies bedeutet normalerweise, GPS-Gerät installieren oder auf einer Stratum 1-Quelle, wobei #3 verweist. Die Analogie wechselt, wenn Sie zwei Boote auf das Wasser, und Sie haben die Höhe eines im Vergleich zu den anderen messen möchten, ist Ihre Genauigkeit am besten, wenn das Schiff Quelle sehr stabil und nicht bewegt wird. Das gleiche gilt für die Zeit, und wenn Ihre Quelle Uhr nicht stabil ist, klicken Sie dann die gesamte Kette von synchronisierten Uhren beeinflusst und vergrößert in jeder Phase. Sie müssen auch zugegriffen werden kann, da Unterbrechungen der Verbindung mit der zeitsynchronisierung beeinträchtigt. Und schließlich muss es sicherer sein. Wenn die Zeit, die Verweis nicht ordnungsgemäß ist verwaltet, oder eine potenziell böswillige Partei betrieben, können Sie Ihre Domäne für die zeitbasierte Angriffe verfügbar machen.
2. **Stabile Client Uhr** -eine stabile Clientuhren wird sichergestellt, dass die natürliche Abweichung von der Oscillator containable ist.  NTP-Server mehrere Beispiele von potenziell mehreren NTP-Server, Fehler und Ihre lokalen Computern Uhr discipline verwendet.  Es die Zeit geändert wird, wird kein Einzelschritt jedoch eher verlangsamt wird, oder die lokale Uhr beschleunigt, damit Sie die genaue Uhrzeit schnell Ansatz und zwischen NTP-Anforderungen genau bleiben.  Allerdings ist die Client-Computeruhr Oscillator nicht stabil, klicken Sie dann weitere schwankungen zwischen Anpassungen können auftreten, und die Algorithmen, mit denen, die Windows verwendet wird, um die Uhr für die erste Bedingung, nicht korrekt funktionieren.  In einigen Fällen können die Firmware-Updates nach der genauen Zeit erforderlich sein.
3. **Symmetrische NTP-Kommunikation** – es ist wichtig, dass die Verbindung für die Kommunikation mit NTP symmetrisch ist.  NTP-Server verwendet Berechnungen anpassen, die Zeit, die davon ausgehen, dass der Netzwerk-Patch symmetrisch ist.  Wenn der Pfad der NTP-Paket wird auf dem Server verwendet eine unterschiedliche Menge an Zeit für die Rückgabe, die Genauigkeit ist betroffen.  Beispielsweise konnte den Pfad ändern, aufgrund von Änderungen an der Netzwerktopologie und Pakete, die über Geräte, auf denen Geschwindigkeit der anderen Schnittstelle weitergeleitet werden.


Bei Akkubetrieb-Geräten müssen sowohl mobile als auch portable, verschiedene Strategien berücksichtigt werden.  Gemäß der Empfehlung erfordert halten die genaue Uhrzeit die Uhr auf einmal pro Sekunde, die mit der Update-Taktfrequenz korreliert, objektiver werden aus. Diese Einstellungen belegt mehr Akkuleistung als erwartet und der Energiesparmodus versetzt verfügbar in Windows für solche Geräte beeinträchtigen können. Akkubetrieb-Geräte können auch bestimmte Energiestatus alle Anwendungen ausgeführt werden, beendet der W32time Fähigkeit discipline der Uhr, und verwalten die genaue Uhrzeit beeinträchtigt. Darüber hinaus die Uhren auf mobilen Geräten sehr präzise zunächst möglicherweise nicht.  Ambiente umgebungsbedingungen Auswirkungen auf die Genauigkeit der Uhr, und ein mobiles Gerät von einer ambient-Bedingung in der nächsten, die durch die Möglichkeit zur Zeitpunkt genau zu bewahren beeinträchtigen könnten verschieben.  Aus diesem Grund rät Microsoft davon, dass Sie Akkubetrieb tragbaren Geräten mit hoher Genauigkeit Einstellungen einrichten. 

## <a name="why-is-time-important"></a>Warum ist die Uhrzeit wichtig?  
Es gibt viele verschiedene Gründe, dass Sie möglicherweise die genaue Zeit benötigen.  Die typische Fall für Windows ist Kerberos verwendet, die 5 Minuten der Genauigkeit zwischen Client und Server erforderlich ist.  Es gibt jedoch viele andere Bereiche, die dazu zählen Genauigkeit auswirken können:


- Gesetzliche Vorschriften wie folgt vor:
    - 50 ms beträgt die Genauigkeit für FINRA in den USA
    - 1 ms ESMA (MiFID II) in der EU.
- Kryptografischen Algorithmen
- Verteilte Systeme wie Cluster/SQL/Exchange und der Dokument-Datenbanken
- Blockchain-Framework für Bitcoin-Transaktionen
- Verteilte Protokolle und Bedrohungsanalyse 
- AD-Replikation
- PCI (Payment Card Industry), Zeit 1 Sekunde Genauigkeit



[!INCLUDE [windows-server-2016-improvements](windows-server-2016-improvements.md)]
