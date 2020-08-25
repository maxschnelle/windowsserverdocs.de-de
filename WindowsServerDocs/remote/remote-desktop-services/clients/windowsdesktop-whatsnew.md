---
title: Neuigkeiten im Windows-Desktopclient
description: Hier erfährst du mehr über aktuelle Änderungen am Remotedesktopclient für Windows-Desktop
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 08/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: b23c19304aa7773dbb3c4e1406e065fb68947c5d
ms.sourcegitcommit: 8e5530ba7f7d3e2569590949e1f443d908683a17
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702839"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Neuigkeiten im Windows-Desktopclient

Ausführlichere Informationen über den Windows-Desktopclient findest du unter [Erste Schritte mit dem Windows-Desktopclient](windowsdesktop.md). Die neuesten Updates für den Client findest du nachstehend.

## <a name="latest-client-versions"></a>Neueste Clientversionen

Der Client kann für verschiedene [Benutzergruppen](windowsdesktop-admin.md#configure-user-groups) konfiguriert werden. In der folgenden Tabelle sind die aktuellen Versionen aufgelistet, die für jede Benutzergruppe verfügbar sind:

|Benutzergruppe |Version  |
|-----------|---------|
|Öffentlich     |1.2.1186 |
|Insider    |1.2.1272 |

## <a name="updates-for-version-121272-insider"></a>Updates für Version 1.2.1272 [INSIDER]

*Veröffentlicht am: 11.08.2020*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4D7LK), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4D5aF), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4Dan3)

- Es wurden Funktionen zum automatischen Erkennen von unabhängigen Clouds aus der Identität des Benutzers hinzugefügt.
- Es wurden Funktionen zum Aktivieren benutzerdefinierter URL-Abonnements für alle Benutzer hinzugefügt.
- Ein Problem beim Anheften von Apps auf der Feed-Taskleiste wurde behoben.
- Ein Absturzproblem beim Abonnieren von URLs wurde behoben.
- Verbesserte Benutzererfahrung beim Ziehen der Fenster von Remote-Apps mit Toucheingabe oder Stift.

## <a name="updates-for-version-121186"></a>Updates für Version 1.2.1186

*Veröffentlicht am: 28.7.2020*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4C7Qy), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4Ciex), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4C7Qx)

- Sie können jetzt Arbeitsbereiche mit mehreren Benutzerkonten abonniert, indem Sie die Überlaufmenüoption ( **...** ) auf der Befehlsleiste oben im Client verwenden. Um Arbeitsbereiche zu unterscheiden, enthalten die Arbeitsbereichstitel jetzt den Benutzernamen, ebenso wie alle Titel von App-Verknüpfungen.
- Zusätzliche Informationen zu Abonnementfehlermeldungen wurden hinzugefügt, um die Problembehandlung zu verbessern.
- Der reduzierte/erweiterte Status von Arbeitsbereichen wird jetzt während einer Aktualisierung beibehalten.
- Dem Dialogfeld **Verbindungsinformationen** wurde eine Schaltfläche **Diagnose senden und schließen** hinzugefügt.
- Es wurde ein Problem mit der Tastenkombination STRG+UMSCHALT in Remotesitzungen behoben.

## <a name="updates-for-version-121104"></a>Updates für Version 1.2.1104

*Veröffentlicht am: 23.06.2020*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4zeHS), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4zrAd), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4zeHR)

- Die automatische Ermittlungslogik für die Option „**Subscribe**“ wurde aktualisiert, um die in Azure Resource Manager integrierte Version von Windows Virtual Desktop zu unterstützen. Kunden, die nur über Windows Virtual Desktop-Ressourcen verfügen, sollten nicht länger die Zustimmung für Windows Virtual Desktop (klassisch) erteilen müssen.
- Verbesserte Unterstützung für Geräte mit hohen DPI-Werten und einem Skalierungsfaktor von bis zu 400 %.
- Ein Problem wurde behoben, bei dem das Dialogfeld zum Trennen nicht angezeigt wurde.
- Ein Problem wurde behoben, bei dem die QuickInfos der Befehlsleiste länger als erwartet sichtbar blieben.
- Die Ursache für einen Absturz wurde behoben, der beim Versuch des Abonnierens unmittelbar nach einer Aktualisierung auftrat.
- Die Ursache für einen Absturz durch ein falsches Analysieren von Datum und Uhrzeit in einigen Sprachen wurde behoben.

## <a name="updates-for-version-121026"></a>Updates für Version 1.2.1026

*Veröffentlicht am: 27.05.2020*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4xsGB), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4xd8P), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4xq7m)

- Beim Abonnieren kannst du nun dein Konto auswählen, anstatt deine E-Mail-Adresse einzugeben.
- Es wurde eine neue Option **Mit URL abonnieren** hinzugefügt, die es dir ermöglicht, die URL des Arbeitsbereichs anzugeben, den du abonnierst, oder in Fällen, in denen deine Ressourcen nicht automatisch gefunden werden, die [E-Mail-Ermittlung](../rds-email-discovery.md) zu nutzen. Dieses Verfahren ähnelt dem Abonnementprozess auf den anderen Remotedesktopclients. Es kann verwendet werden, um die Windows Virtual Desktop-Arbeitsbereiche direkt zu abonnieren.
- Es wurde Unterstützung für das Abonnieren eines Arbeitsbereichs mit einem neuen [URI-Schema](remote-desktop-uri.md) hinzugefügt, das in einer E-Mail an Benutzer gesendet oder zu einer Supportwebsite hinzugefügt werden kann.
- Es wurde das neue Dialogfeld **Verbindungsinformationen** hinzugefügt, das Client-, Netzwerk- und Serverdetails für Desktop- und App-Sitzungen bereitstellt. Du kannst auf das Dialogfeld im Vollbildmodus über die Verbindungsleiste und im Fenstermodus über das Menüsystem zugreifen.
- Im Fenstermodus gestartete Desktopsitzungen werden nun immer maximiert, anstatt beim Maximieren des Fensters in den Vollbildmodus zu wechseln. Verwende die Option **Vollbild** im Systemmenü, um in den Vollbildmodus zu gelangen.
- Die Eingabeaufforderung „Abonnement kündigen“ weist nun ein Warnsymbol auf und zeigt die Namen der Arbeitsbereiche als Aufzählung an.
- Der Abschnitt „Details“ wurde in weiteren Fehlerdialogfeldern hinzugefügt, um bei der Diagnose von Problemen zu helfen.
- Dem Abschnitt „Details“ in Fehlerdialogfeldern wurde ein Zeitstempel hinzugefügt.
- Es wurde ein Problem behoben, bei dem die RDP-Dateieinstellung **desktop size id** nicht ordnungsgemäß funktionierte.
- Es wurde ein Problem behoben, bei dem die Anzeigeeinstellung **Update the resolution on resize** (Auflösung bei Größenänderung aktualisieren) nach dem Starten der Sitzung nicht angewandt wurde.
- Es wurden Lokalisierungsprobleme im Bereich „Desktopeinstellungen“ behoben.
- Die Größe des Fokusfelds beim Wechseln der Steuerelemente mit der TAB-TASTE im Bereich „Desktopeinstellungen“ wurde korrigiert.
- Es wurde ein Problem behoben, durch das die Ressourcennamen im Modus mit hohem Kontrast schwierig zu lesen waren.
- Es wurde ein Problem behoben, durch das die Updatebenachrichtigung im Wartungscenter mehrmals täglich angezeigt wurde.

## <a name="updates-for-version-12945"></a>Updates für Version 1.2.945

*Veröffentlicht am: 28.04.2020*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4vhNM), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4vhNO), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4vuSV)

- Es wurden neue Optionen für Anzeigeeinstellungen für Desktopverbindungen hinzugefügt, die beim Klicken mit der rechten Maustaste auf ein Desktopsymbol im Connection Center verfügbar sind.
  - Es gibt jetzt drei Anzeigekonfigurationsoptionen: **Alle Displays**, **Einzeldisplay** und **Displays auswählen**.
  - Es werden jetzt nur die verfügbaren Einstellungen angezeigt, wenn eine Anzeigekonfiguration ausgewählt ist.
  - Im Modus „Display auswählen“ ermöglicht eine neue Option **Auf aktuelle Displays maximieren** Ihnen, die für die Sitzung verwendeten Displays dynamisch zu ändern, ohne die Verbindung erneut herstellen zu müssen. Ist diese Option aktiviert, bewirkt das Maximieren der Sitzung, dass diese auf allen betroffenen Displays im Vollbildmodus angezeigt wird.
  - Eine neue Option **Einzeldisplay bei Fenstermodus** für alle Displays und „Displays auswählen“-Modi wurde hinzugefügt. Diese Option schaltet Ihre Sitzung automatisch auf ein einziges Display um, wenn Sie den Vollbildmodus verlassen, und kehrt automatisch zu mehreren Displays zurück, wenn Sie das Fenster maximieren.
- Dem Systemmenü, das angezeigt wird, wenn Sie mit der rechten Maustaste auf die Titelleiste einer im Fenstermodus angezeigten Desktopsitzung klicken, wurde eine neue **Anzeigeeinstellungen**-Gruppe hinzugefügt. Auf diese Weise können Sie einige Einstellungen während einer Sitzung dynamisch ändern. Sie können z. B. die neuen Einstellungen **Einzeldisplaymodus bei Fenstermodus** und **Auf aktuelle Displays maximieren** anzeigen.
- Wenn Sie den Vollbildschirm verlassen, kehrt das Sitzungsfenster an seine ursprüngliche Position zurück, an der Sie zum ersten Mal in den Vollbildmodus gewechselt sind.
- Die Hintergrundaktualisierung für Arbeitsbereiche wurde geändert und findet nun alle vier Stunden anstelle von stündlich statt. Beim Starten des Clients wird jetzt automatisch eine Aktualisierung durchgeführt.
- Das Zurücksetzen Ihrer Benutzerdaten über die Seite „Info“ leitet Sie jetzt nach Abschluss des Vorgangs zum Connection Center um, anstatt den Client zu schließen.
- Die Elemente im Systemmenü für Desktopverbindungen wurden neu angeordnet, und das Hilfethema verweist jetzt auf die Clientdokumentation.
- Es wurden einige Barrierefreiheitsprobleme bei der Registerkartennavigation und Sprachausgabe behoben.
- Es wurde ein Problem behoben, bei dem das Azure Active Directory-Authentifizierungsdialogfeld hinter dem Sitzungsfenster angezeigt wurde.
- Ein Problem mit Flackern und Schrumpfen beim Ziehen eines Desktopsitzungsfensters zwischen Displays mit unterschiedlichen Skalierungsfaktoren wurde behoben.
- Ein Fehler, der beim Umleiten von Kameras aufgetreten ist, wurde korrigiert.
- Mehrere Ursachen für Abstürze wurden beseitigt, um die Zuverlässigkeit zu verbessern.

## <a name="updates-for-version-12790"></a>Updates für Version 1.2.790

*Veröffentlicht am: 24.03.2020*

- Die Aktion „Update“ für Arbeitsbereiche wurde in „Aktualisieren“ umbenannt, um Konsistenz mit anderen Remotedesktopclients zu gewährleisten.
- Ein Arbeitsbereich kann jetzt direkt über das zugehörige Kontextmenü aktualisiert werden.
- Durch manuelles Aktualisieren eines Arbeitsbereichs wird sichergestellt, dass alle lokalen Inhalte aktualisiert werden.
- Die Benutzerdaten des Clients können jetzt über die Seite „Info“ zurückgesetzt werden, ohne die App deinstallieren zu müssen.
- Die Benutzerdaten des Clients können jetzt auch mit „msrdcw.exe /reset“ und einem optionalen „/f“-Parameter zurückgesetzt werden, um die Eingabeaufforderung zu überspringen.
- Bei der Navigation zur Seite „Info wird jetzt automatisch nach einem Clientupdate gesucht.
- Die Farbe der Schaltflächen wurde aus Konsistenzgründen aktualisiert.

## <a name="updates-for-version-12675"></a>Updates für Version 1.2.675

*Veröffentlicht am: 25.02.2020*

- Verbindungen mit Windows Virtual Desktop werden jetzt blockiert, wenn der RDP-Datei die Signatur fehlt oder eine der signscope-Eigenschaften geändert wurde.
- Wenn ein Arbeitsbereich leer ist oder entfernt wurde, scheint das Verbindungscenter nicht mehr leer zu sein.
- Trennungsmeldungen wurden die Aktivitäts-ID und der Fehlercode hinzugefügt, um die Problembehandlung zu verbessern. Du kannst die Dialogmeldung mit **STRG+C** kopieren.
- Ein Problem wurde behoben, das dazu geführt hat, dass die Desktopverbindungseinstellungen keine Anzeigen erkannt haben.
- Der PC wird von Clientupdates nicht mehr automatisch neu gestartet.
- Auf der Taskleiste sollten keine fensterlosen Symbole mehr angezeigt werden.

## <a name="updates-for-version-12605"></a>Updates für Version 1.2.605

*Veröffentlicht am: 29.01.2020*

- Du kannst jetzt auswählen, welche Anzeigen für Desktopverbindungen verwendet werden sollen. Zum Ändern dieser Einstellung klicke mit der rechten Maustaste auf das Symbol der Desktopverbindung, und wähle **Einstellungen** aus.
- Es wurde ein Problem behoben, bei dem in den Verbindungseinstellungen nicht die richtigen verfügbaren Skalierungsfaktoren angezeigt wurden.
- Es wurde ein Problem behoben, bei dem die Sprachausgabe den beim Initiieren der Verbindung gezeigten Dialog nicht lesen konnte.
- Es wurde ein Problem behoben, bei dem der falsche Benutzername angezeigt wurde, wenn die Namen von Azure Active Directory und Active Directory nicht übereinstimmten.
- Es wurde ein Problem behoben, durch das der Client beim Initiieren einer Verbindung nicht mehr reagierte, wenn keine Netzwerkverbindung vorlag.
- Es wurde ein Problem behoben, das dazu führte, dass der Client beim Anschließen eines Headsets nicht mehr reagierte.

## <a name="updates-for-version-12535"></a>Updates für Version 1.2.535

*Veröffentlicht am: 04.12.2019*

- Sie können jetzt direkt über die Schaltfläche „Weitere Optionen“ in der Befehlsleiste am oberen Rand des Clients auf Informationen über Updates zugreifen.
- Außerdem können Sie nun Feedback über die Befehlsleiste des Clients mitteilen.
- Die Feedbackoption wird jetzt nur angezeigt, wenn der Feedback-Hub verfügbar ist.
- Gewährleistet, dass die Updatebenachrichtigung nicht angezeigt wird, wenn Benachrichtigungen per Richtlinie deaktiviert sind.
- Es wurde ein Problem behoben, das das Starten einiger RDP-Dateien verhindert hat.
- Es wurde ein Absturz beim Starten des Clients behoben, der durch die Beschädigung einiger persistenter Einstellungen verursacht wurde.

## <a name="updates-for-version-12431"></a>Updates für Version 1.2.431

*Veröffentlicht am: 12.11.2019*

- Die 32-Bit-Version und die ARM64-Version des Clients sind nun verfügbar.
- Der Client speichert jetzt alle an der Verbindungsleiste vorgenommenen Änderungen (z.B. Position, Größe und angehefteter Zustand), und wendet diese Änderungen sitzungsübergreifend an.
- Aktualisierte Dialogfelder für Gatewayinformationen und Verbindungsstatus.
- Es wurde ein Problem behoben, das dazu führte, dass beim Verbindungsversuch nach Ablauf des Azure Active Directory-Token gleichzeitig zwei Mal Anmeldeinformationen angefordert wurden.
- Unter Windows 7 werden die Benutzer nun ordnungsgemäß zur Eingabe von Anmeldeinformationen aufgefordert, wenn sie Anmeldeinformationen gespeichert hatten und der Server dies nicht zulässt.
- Die Azure Active Directory-Eingabeaufforderung wird jetzt beim Wiederherstellen der Verbindung vor dem Verbindungsfenster angezeigt.
- Elemente, die an die Taskleiste angeheftet wurden, werden jetzt während einer Feedaktualisierung aktualisiert.
- Verbessertes Scrollen im Connection Center bei Verwendung der Toucheingabe.
- Die leere Zeile wurde aus dem Dropdownmenü „Auflösung“ entfernt.
- Unnötige Einträge in der Windows-Anmeldeinformationsverwaltung wurden entfernt.
- Beim Beenden des Vollbildmodus erfolgt nun eine ordnungsgemäße Größenanpassung der Desktopsitzungen.
- Das Dialogfeld zum Trennen der RemoteApp wird jetzt im Vordergrund angezeigt, wenn eine Sitzung aus dem Energiesparmodus wieder aufgenommen wird.
- Barrierefreiheitsprobleme, z.B. bei der Tastaturnavigation, wurden behoben.

## <a name="updates-for-version-12247"></a>Updates für Version 1.2.247

*Veröffentlicht am: 17.09.2019*

- Verbesserung der Reservesprachen für lokalisierte Versionen. (Beispielsweise wird FR-CA ordnungsgemäß in Französisch anstelle von Englisch angezeigt.)
- Beim Entfernen eines Abonnements entfernt der Client nun die gespeicherten Anmeldeinformationen ordnungsgemäß aus der Anmeldeinformationsverwaltung.
- Der Updatevorgang des Clients erfolgt jetzt nach dem Starten ohne Benutzereingriff, und der Client wird nach Abschluss neu gestartet.
- Der-Client kann jetzt unter Windows 10 im S-Modus verwendet werden.
- Es wurde ein Problem behoben, das für Benutzer mit einem Leerzeichen im Benutzernamen zu einem Fehler beim Update führte.
- Es wurde ein Absturz korrigiert, der vorkam, wenn während einer Verbindung eine Authentifizierung vorgenommen wurde.
- Es wurde ein Absturz korrigiert, der vorkam, wenn der Client geschlossen wurde.
