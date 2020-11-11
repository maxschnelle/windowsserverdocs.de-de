---
title: Neues beim iOS-Client
description: Hier wirst du über aktuelle Änderungen des Remotedesktopclients für iOS informiert.
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 11/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: beb97113165127c50c815ccca8a667a1654215fa
ms.sourcegitcommit: 5fc77b4325a18d8c22385d899b14fe724a662347
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361167"
---
# <a name="whats-new-in-the-ios-client"></a>Neues beim iOS-Client

Der [Remotedesktopclient für iOS](remote-desktop-ios.md) wird regelmäßig mit neuen Features und Problembehebungen aktualisiert. Auf dieser Seite findest du die neuesten Updates.

## <a name="how-to-report-issues"></a>Melden von Problemen

Wir sind bestrebt, den Remotedesktopclient für iOS bestmöglich zu gestalten, und wissen dein Feedback zu schätzen. Du kannst Probleme unter **Hilfe** > **Problem melden** melden.

## <a name="updates-for-version-1020"></a>Updates für Version 10.2.0

*Veröffentlicht am: 06.11.2020*

In dieser Version wurden einige Kompatibilitätsprobleme mit iOS und iPadOS 14 behoben. Außerdem wurden die folgenden Korrekturen und Featureupdates vorgenommen:

- Ursachen für Abstürze unter iOS und iPadOS 14 wurden beseitigt, die bei Eingaben über die Tastatur auftraten.
- Die Tastenkombinationen CMD+S und CMD+N für die Prozesse „Arbeitsbereich hinzufügen“ bzw. „PC hinzufügen“ wurden hinzugefügt.
- Die Tastenkombination CMD+F zum Aufrufen der Benutzeroberfläche für die Suche im Connection Center wurde hinzugefügt.
- Die Befehle „Alle erweitern“ und „Alle reduzieren“ wurden zur Registerkarte „Arbeitsbereiche“ hinzugefügt.
- Es wurde ein Fehler behoben, der einen 0xd06-Protokollfehler beim Ausführen von Outlook als Remote-App verursachte.
- Die Bildschirmtastatur wird nun ausgeblendet, wenn Sie im Connection Center durch Suchergebnisse scrollen.
- Die Animation, die in iPadOS 14 angezeigt wird, wenn Sie einen Maus- oder Trackpadzeiger über Arbeitsbereichssymbole bewegen, wurde aktualisiert.

## <a name="updates-for-version-1014"></a>Updates für Version 10.1.4

*Veröffentlicht am: 06.11.2020*

Wir haben einige Fehlerbehebungen und kleine Featureupdates für das Release 10.1.4 zusammengestellt. Neuigkeiten:

- Es wurde ein Problem behoben, durch das auf dem Client beim Versuch, eine Verbindung mit einem Remotedesktop-Gatewayserver herzustellen, eine 0x5000007-Fehlermeldung angezeigt wurde.
- Auf der Benutzeroberfläche für Anmeldeinformationen aktualisierte Benutzerkonto-Kennwörter werden nun nach erfolgreicher Anmeldung gespeichert.
- Es wurde ein Problem behoben, bei dem die Bereichs- und Mehrfachauswahl mit der Maus oder dem Trackpad (UMSHALT+Klicken und STRG+Klicken) nicht konsistent waren.
- Es wurde ein Fehler behoben, bei dem in der Benutzeroberfläche des Schnellzugriffs innerhalb einer Sitzung angezeigte Apps nicht mit der Remotesitzung synchronisiert wurden.
- Am Layout der Connection Center-Arbeitsbereichsheader wurden einige kosmetische Änderungen vorgenommen.
- Verbesserte Sichtbarkeit der Bildschirmtastatur-Schaltflächen für dunkle Hintergründe.
- Es wurde ein Lokalisierungsfehler im Dialogfeld „Trennen“ behoben.

## <a name="updates-for-version-1013"></a>Updates für Version 10.1.3

*Veröffentlicht am: 06.11.2020*

Wir haben einige Fehlerbehebungen und Featureupdates für das Release 10.1.3 zusammengestellt. Neuigkeiten:

- Der Eingabemodus (Mauszeiger oder Fingereingabemodus) ist jetzt für alle aktiven PCs und Remote-App-Verbindungen global verfügbar.
- Es wurde ein Problem behoben, das eine konsistente Funktion der Mikrofonumleitung verhinderte.
- Es wurde ein Fehler behoben, der bewirkte, dass die Audioausgabe über den iPhone-Kopfhörer anstelle des internen Lautsprechers wiedergegeben wurde.
- Der Client unterstützt jetzt das automatische Wechseln der Audioausgabe zwischen internen iPhone- oder iPad-Lautsprechern, Bluetooth-Lautsprechern und Airpods.
- Audiodaten werden jetzt im Hintergrund wiedergegeben, wenn Sie den Client verlassen oder das Gerät sperren.
- Der Eingabemodus wechselt automatisch in den Fingereingabemodus, wenn eine SwiftPoint-Maus mit iPhones oder iPads (auf denen nicht iPadOS, Version 13,4 oder höher ausgeführt wird) verwendet wird.
- Grafikausgabeprobleme wurden behoben, die auftraten, wenn der Server für die Verwendung des AVC444-Vollbildmodus konfiguriert wurde.
- Einige VoiceOver-Fehler wurden behoben.
- Das Schwenken in einer vergrößerten Sitzungsansicht mit einer externen Maus oder einem Trackpad funktioniert jetzt anders. Wenn Sie in einer vergrößerten Sitzungsansicht mit einer externen Maus oder einem Trackpad schwenken möchten, wählen Sie den Knopf „Schwenken“ aus, und ziehen Sie den Mauszeiger bei gedrückter Maustaste. Um im Fingereingabemodus zu schwenken, drücken Sie den Knopf „Schwenken“, und bewegen Sie den Finger. Die Sitzung bleibt am Finger „haften“, und folgt Ihren Bewegungen. Im Mauszeiger-Modus schieben Sie den virtuellen Mauszeiger gegen die Seiten des Bildschirms.

## <a name="updates-for-version-1012"></a>Updates für Version 10.1.2

*Veröffentlicht am 17.08.2020*

In diesem Update haben wir uns mit Problemen befasst, die für das Update auf Version 10.1.1 gemeldet wurden.

- Es wurde ein Absturz korrigiert, der bei einigen Benutzern auftrat, wenn ein Windows Virtual Desktop-Feed nicht mit Broker Authentifizierung abonniert wurde.
- Das Layout der Arbeitsbereichssymbole auf iPhone X, iPhone XS und iPhone 11 Pro wurde berichtigt.

## <a name="updates-for-version-1011"></a>Updates für Version 10.1.1

*Veröffentlicht am: 06.11.2020*

Dieses Release enthält folgende Änderungen:

- Ein Fehler wurde behoben, der Eingaben in Koreanisch verhinderte.
- Unterstützung für die Tasten F1 bis F12, POS1, ENDE, BILD-AUF und BILD-AB auf Hardwaretastaturen wurde hinzugefügt.
- Es wurde ein Fehler behoben, der das Verschieben des Mauszeigers an den oberen Bildschirmrand im Letterbox-Modus auf iPadOS-Geräten erschwerte.
- Es wurde ein Problem behoben, durch den beim Drücken der RÜCKTASTE nach einem Leerzeichen zwei Zeichen gelöscht wurden.
- Es wurde ein Fehler behoben, der bewirkte, dass der iPadOS-Mauszeiger im Modus „Tippen zum Klicken“ über Mauszeiger des Remotedesktopclients angezeigt wird.
- Es wurde ein Problem behoben, das Verbindungen mit einigen Remotedesktop-Gatewayserver verhinderte (Fehlercode 0x30000064).
- Es wurde ein Fehler behoben, bei dem der Mauszeiger auf iOS-Geräten bei Verwendung einer SwiftPoint-Maus in der Benutzeroberfläche des Schnellzugriffs innerhalb einer Sitzung angezeigt wurde.
- Die Größe des Remotedesktop-Mauszeigers wurde entsprechend dem aktuellen Clientskalierungsfaktor geändert.
- Der Client überprüft nun, ob eine Verbindung mit dem Netzwerk vorliegt, bevor eine Arbeitsbereichsressource oder eine PC-Verbindung gestartet wird.
- Durch Drücken der neu zugeordneten ESC-TASTE oder CMD+. werden jetzt alle Anmeldeaufforderungen abgebrochen.
- Es wurden einige Animationen und Optimierungen hinzugefügt, die angezeigt werden, wenn Sie den Mauszeiger auf iPads bewegen, auf denen iPadOS 13.4 oder höher ausgeführt wird.

## <a name="updates-for-version-1010"></a>Updates für Version 10.1.0

*Veröffentlicht am: 06.11.2020*

Hier sind die Neuerungen in dieser Version:

- Wenn Sie iPadOS 13.4 oder höher verwenden, können Sie die Remotesitzung jetzt mit einer Maus oder einem Trackpad steuern.
- Der Client unterstützt jetzt die folgenden Gesten der Apple Magic Mouse 2 und des Apple Magic Trackpad 2: Linksklicken, Linksklicken+Ziehen, Rechtsklicken, Rechtsklicken+Ziehen, horizontales und vertikales Scrollen sowie lokales Zoomen.
- Bei externen Mäusen unterstützt der Client jetzt Linksklicken, Linksklicken+Ziehen, Rechtsklicken, Rechtsklicken+Ziehen, Klicken der mittleren Maustaste und vertikales Scrollen.
- Der Client unterstützt jetzt Tastenkombinationen, bei denen die Tasten STRG, ALT oder UMSCHALT mit der Maus oder dem Trackpad verwendet werden, einschließlich Mehrfachauswahl und Bereichsauswahl.
- Der Client unterstützt jetzt das Feature „Tippen zum Klicken“ für das Trackpad.
- Die Rechtsklicken-Geste im Mauszeiger-Modus wurde in „Drücken und halten“ (nicht „Drücken und halten und loslassen") aktualisiert. Auf dem iPhone-Client wird Feedback angezeigt, wenn die Rechtsklicken-Geste erkannt wird.
- Eine Option zum Deaktivieren der NLA-Erzwingung unter **iOS-Einstellungen** > **Remotedesktopclient** wurde hinzugefügt.
- CONTROL+UMSCHALT+ESC wurde STRG+UMSCHALT+ESC zugeordnet, wobei ESC mithilfe einer neu zugeordneten Taste auf iPadOS oder BEFEHL+ erzeugt wird.
- BEFEHL+F wurde STRG+F zugeordnet.
- Es wurde ein Problem behoben, durch das die mittlere Taste einer SwiftPoint-Maus unter iPadOS, Version 13.3.1 oder früher, und iOS nicht funktionierte.
- Einige Fehler wurden behoben, die verhinderten, dass der Client den „rdp:“ URI erkennt.
- Es wurde ein Problem behoben, bei dem die Benutzeroberfläche des immersive Schnellzugriffs innerhalb einer Sitzung veraltete App-Einträge anzeigte, wenn eine Trennung vom Server initiiert wurde.
- Der Client unterstützt jetzt die in Azure Resource Manager integrierte Version von Windows Virtual Desktop.

## <a name="updates-for-version-1007"></a>Updates für Version 10.0.7

*Veröffentlicht am: 29.04.2020*

In diesem Update haben wir die Möglichkeit hinzugefügt, die PC-Listenansicht (auf dem iPhone verfügbar) nach dem Namen oder der Uhrzeit der letzten Verbindung zu sortieren.

## <a name="updates-for-version-1006"></a>Updates für Version 10.0.6

*Veröffentlicht am: 31.03.2020*

Es ist an der Zeit für ein schnelles Update mit einigen Fehlerbehebungen. Hier sind die Neuigkeiten in diesem Release:

- Eine Reihe von VoiceOver-Barrierefreiheitsproblemen wurde behoben.
- Es wurde ein Problem behoben, bei dem Benutzer mit türkischen Anmeldeinformationen keine Verbindung herstellen konnten.
- Die in der Wechselbenutzeroberfläche angezeigten Sitzungen werden nun nach dem Startzeitpunkt geordnet.
- Durch Auswählen der Schaltfläche „Zurück“ im Connection Center gelangst du nun zurück zur letzten aktiven Sitzung.
- Swiftpoint-Mäuse werden jetzt freigegeben, wenn vom Client zu einer anderen App gewechselt wird.
- Die Interoperabilität mit dem Windows Virtual Desktop-Dienst wurde verbessert.
- Es wurden Abstürze korrigiert, die in der Fehlerberichterstattung auftraten.

Wir freuen uns über alle über den App Store und das In-App-Feedback sowie per E-Mail gesendete Kommentare. Außerdem möchten wir uns besonders bei allen bedanken, die mit uns an der Diagnose von Problemen zusammengearbeitet haben.

## <a name="updates-for-version-1005"></a>Updates für Version 10.0.5

*Veröffentlicht am: 09.03.20*

Wir haben einige Fehlerbehebungen und Featureupdates für dieses Release 10.0.5 zusammengestellt. Neuigkeiten:

- Gestartete RDP-Dateien werden jetzt automatisch importiert (die Umschaltfläche findest du in den Einstellungen unter „Allgemein“).
- Du kannst jetzt iCloud-basierte RDP-Dateien starten, die noch nicht in die Dateien-App heruntergeladen wurden.
- Die Remotesitzung kann jetzt unter dem Home Indicator auf iPhones erweitert werden (die Umschaltfläche findest du in den Anzeigeeinstellungen).
- Unterstützung für die Eingabe zusammengesetzter Zeichen mit mehreren Tastenanschlägen, wie z. B. „é“.
- Unterstützung für die unverankerte Tastatur auf dem Bildschirm des iPad.
- Unterstützung für das Anpassen von Eigenschaften umgeleiteter Kameras aus einer Remotesitzung.
- Ein Fehler in der Gestenerkennung wurde behoben, der bewirkte, dass der Client während einer Verbindung mit einer Remotesitzung nicht mehr reagierte.
- Du gelangst jetzt mit einer einzigen Wischgeste nach oben in den App-Wechsel-Modus (außer wenn du dich im Fingereingabemodus befindest und die Sitzung in den Home Indicator-Bereich erweitert wurde).
- Der Home Indicator wird nun automatisch ausgeblendet, wenn eine Verbindung mit einer Remotesitzung besteht, und wieder angezeigt, wenn du auf den Bildschirm tippst.
- Eine Tastenkombination wurde hinzugefügt, um zu den App-Einstellungen im Connection Center zu gelangen ( **BEFEHL + ,** ).
- Eine Tastenkombination zum Aktualisieren aller Arbeitsbereiche im Connection Center wurde hinzugefügt ( **BEFEHL + R** ).
- Systemtastenkombination für „ESC“ während einer Verbindung mit einer Remotesitzung wurden eingebunden ( **Befehl + .** ).
- Es wurden Szenarien korrigiert, bei denen die Windows-Bildschirmtastatur in der Remotesitzung zu klein war.
- Der automatische Tastaturfokus wurde im gesamten Connection Center implementiert, um die Dateneingabe nahtloser zu gestalten.
- Wenn du auf eine Aufforderung zur Eingabe der Anmeldeinformationen die **EINGABETASTE** drückst, wird die Eingabeaufforderung jetzt verworfen, und der aktuelle Flow wird fortgesetzt.
- Ein Szenario wurde korrigiert, bei dem der Client beim Drücken von UMSCHALT+WAHL+NACH LINKS oder NACH OBEN oder NACH UNTEN abstürzte.
- Die Ursache für einen Absturz wurde beseitigt, der beim Entfernen eines SwiftPoint-Geräts auftrat.
- Weitere Absturzursachen wurden beseitigt, die seit dem letzten Release von Benutzern gemeldet wurden.

Wir danken allen Benutzern, die Fehler gemeldet haben und mit uns an der Diagnose der Probleme zusammengearbeitet haben.

## <a name="updates-for-version-1004"></a>Updates für Version 10.0.4

*Veröffentlicht am: 03.02.20*

Es ist Zeit für ein weiteres Update! Wir möchten allen Benutzern danken, die Fehler gemeldet haben und mit uns an der Diagnose der Probleme zusammengearbeitet haben. Hier sind die Neuerungen in dieser Version:

- Beim Löschen von Benutzerkonten und Gateways wird jetzt die Benutzeroberfläche zum Bestätigen angezeigt.
- Die Benutzeroberfläche der Suche im Connection Center wurde geringfügig überarbeitet.
- Der Hinweis zum Benutzernamen, falls vorhanden, wird jetzt in der Benutzeroberfläche für die Anmeldeinformationen angezeigt, wenn du über eine RDP-Datei oder einen URI startest.
- Ein Problem wurde behoben, bei dem die erweiterte Bildschirmtastatur unterhalb der iPhone-Kerbe angezeigt wird.
- Ein Fehler wurde behoben, bei dem externe Tastaturen nach dem Trennen und erneuten Verbinden nicht mehr funktionierten.
- Unterstützung für die ESC-TASTE auf externen Tastaturen wurde hinzugefügt.
- Ein Fehler wurde behoben, bei dem bei der Eingabe von chinesischen Zeichen englische Zeichen angezeigt wurden.
- Ein Fehler wurde behoben, bei dem einige chinesische Eingaben nach dem Löschen in der Remotesitzung erhalten blieben.
- Weitere Absturzursachen wurden beseitigt, die seit dem letzten Release von Benutzern gemeldet wurden.

Wir freuen uns über alle über den App Store, das In-App-Feedback und per E-Mail gesendeten Kommentare. Wir konzentrieren uns weiterhin darauf, diese App mit jedem Release noch besser zu machen.

## <a name="updates-for-version-1003"></a>Updates für Version 10.0.3

*Veröffentlicht am: 16.01.20*

Wir befinden uns im Jahr 2020, und es ist Zeit für das erste Release des Jahres, das heißt für neue Features und Fehlerbehebungen. In diesem Update ist Folgendes enthalten:

- Unterstützung für das Starten von Verbindungen auf RDP-Dateien und RDP-URIs.
- Arbeitsbereich-Kopfzeilen können nun reduziert werden.
- Das gleichzeitige Zoomen und Schwenken im Mauszeiger-Modus wird jetzt unterstützt.
- Eine Drücken-und-Halten-Geste im Mauszeiger-Modus löst jetzt einen Rechtsklick in der Remotesitzung aus.
- Die Force Touch-Geste für das Klicken der rechten Maustaste im Mauszeiger-Modus wurde entfernt.
- Der Bildschirm der In-Session-Umschaltung unterstützt jetzt das Trennen der Verbindung, auch wenn keine Apps verbunden sind.
- Das einfache Ausblenden wird jetzt im Bildschirm der In-Session-Umschaltung unterstützt.
- PCs und Apps werden im Bildschirm der In-Session-Umschaltung nicht mehr automatisch neu angeordnet.
- Der Treffer-Testbereich für das Auslassungspunkte-Menü „PC-Miniaturansicht“ wurde vergrößert.
- Die Einstellungsseite für Eingabegeräte enthält jetzt einen Link zu unterstützten Geräten.
- Es wurde ein Fehler behoben, der dazu führte, dass die Bluetooth-Berechtigungen-Benutzeroberfläche beim Start für einige Benutzer wiederholt angezeigt wurde.
- Weitere Absturzursachen wurden beseitigt, die seit dem letzten Release von Benutzern gemeldet wurden.

## <a name="updates-for-version-1002"></a>Updates für Version 10.0.2

*Veröffentlicht am: 20.12.19*

Wir haben hart daran gearbeitet, Fehler zu beheben und nützliche Features hinzuzufügen. Hier sind die Neuigkeiten in diesem Release:

- Unterstützung für japanische und chinesische Eingaben auf Hardwaretastaturen.
- In der PC-Listenansicht wird jetzt der Anzeigename des zugehörigen Benutzerkontos angezeigt, falls vorhanden.
- Die Berechtigungen-Benutzeroberfläche bei der Erstausführung wird jetzt im hellen Modus korrekt dargestellt.
- Die Ursache für einen Absturz wurde behoben, der immer dann auftrat, wenn jemand auf einer Hardwaretastatur gleichzeitig WAHL und NACH OBEN oder NACH UNTEN drückte.
- Das in der Kennwortabfrage-Benutzeroberfläche verwendete Bildschirmtastaturlayout wurde aktualisiert, um das Auffinden des umgekehrten Schrägstrichs (\) zu erleichtern.
- Weitere Absturzursachen wurden beseitigt, die seit dem letzten Release von Benutzern gemeldet wurden.

## <a name="updates-for-version-1001"></a>Updates für Version 10.0.1

*Veröffentlicht am: 15.12.19*

Hier sind die Neuigkeiten in diesem Release:

- Unterstützung für den Windows Virtual Desktop-Dienst.
- Aktualisierte Connection Center-Benutzeroberfläche.
- Aktualisierte In-Session-Benutzeroberfläche.

## <a name="updates-for-version-1000"></a>Updates für Version 10.0.0

*Veröffentlicht am: 13.12.19*

Es ist weit über ein Jahr her, dass wir den Remotedesktopclient für iOS das letzte Mal aktualisiert haben. Wir sind jedoch mit einem aufregenden neuen Update zurück, und es wird von nun an regelmäßig viele weitere Updates geben. Neuerungen in Version 10.0.0:

- Unterstützung für den Windows Virtual Desktop-Dienst.
- Eine neue Connection Center-Benutzeroberfläche.
- Eine neue In-Session-Benutzeroberfläche, die zwischen angeschlossenen PCs und Apps wechseln kann.
- Neues Layout für die zusätzliche Bildschirmtastatur.
- Verbesserte Unterstützung für externe Tastaturen.
- Unterstützung für SwiftPoint Bluetooth-Maus.
- Unterstützung für die Mikrofonumleitung.
- Unterstützung für die Umleitung des lokalen Speichers.
- Unterstützung für die Kameraumleitung (nur für Windows 10 ab Version 1809 verfügbar).
- Unterstützung für neue iPhone- und iPad-Geräte.
- Unterstützung des dunklen und hellen Designs.
- Kontrolle darüber, ob dein Telefon gesperrt werden kann, wenn es mit einem Remote-PC oder einer Remote-App verbunden ist.
- Die In-Session-Verbindungsleiste kann jetzt durch Drücken und Halten der Taste mit dem Remotedesktop-Logo reduziert werden.

## <a name="updates-for-version-8142"></a>Updates für Version 8.1.42

*Veröffentlicht am: 20.6.2018*

- Fehlerbehebungen und Leistungsverbesserungen.

## <a name="updates-for-version-8141"></a>Updates für Version 8.1.41

*Veröffentlicht am: 28.03.2018*

- Updates für die in CVE-2018-0886 beschriebene CredSSP-Encryption Oracle-Abwehr.
