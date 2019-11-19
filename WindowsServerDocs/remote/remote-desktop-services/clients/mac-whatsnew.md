---
title: Neues beim macOS-Client
description: Hier erfährst du mehr über aktuelle Änderungen beim Remotedesktopclient für Mac.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: daveba
ms.author: helohr
ms.date: 11/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: b44f7c14dce8a8c319f9240c24ebcd8e2d4f7202
ms.sourcegitcommit: b60fdd2efa57ff23834a324b75de8fe245a7631f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/19/2019
ms.locfileid: "74166165"
---
# <a name="whats-new-in-the-macos-client"></a>Neues beim macOS-Client

Der [Remotedesktopclient für macOS](remote-desktop-mac.md) wird regelmäßig mit neuen Features und Problembehebungen aktualisiert. Hier findest du die neuesten Updates.

Bei Problemen kannst du dich jederzeit gern über **Hilfe** > **Problem melden** an uns wenden.

## <a name="updates-for-version-1034"></a>Updates für Version 10.3.4

*Veröffentlicht am: 18.11.19*

Wir haben uns intensiv mit deinem Feedback beschäftigt und eine Sammlung von Bugfixes und Featureupdates zusammengestellt.

- Bei der Verbindung über ein RD-Gateway mit Multi-Factor Authentication bleibt die Gatewayverbindung geöffnet, um mehrfache Aufforderungen von MFA zu vermeiden.
- Die gesamte Clientbenutzeroberfläche ist nun vollständig über die Tastatur zugänglich und bietet Voiceover-Unterstützung.
- Dateien, die in der Remotesitzung in die Zwischenablage kopiert wurden, werden jetzt nur noch beim Einfügen auf den lokalen Computer übertragen.
- URLs, die in der Remotesitzung in die Zwischenablage kopiert wurden, werden jetzt auf dem lokalen Computer richtig eingefügt.
- Skalierungsfaktor-Remoting zur Unterstützung von Retina-Displays ist nun für Szenarien mit mehreren Bildschirmen verfügbar.
- Ein Kompatibilitätsproblem mit FreeRDP-basierten RD-Servern, das Verbindungsprobleme in Umleitungsszenarien verursachte, wurde behoben.
- Smartcard-Umleitungskompatibilität mit zukünftigen Versionen von Windows 10 wurde hergestellt.
- Ein Problem wurde behoben, das speziell unter macOS 10.15 auftrat und bei dem für umgeleitete Ordner ein falscher Wert für den verfügbaren Speicherplatz angegeben wurde.
- Veröffentlichte PC-Verbindungen werden mit einem neuen Symbol auf der Registerkarte „Arbeitsbereiche“ dargestellt.
- „Feeds“ heißen nun „Arbeitsbereiche“ und „Desktops“ heißen jetzt „PCs“.
- Inkonsistenzen und Fehler in der Handhabung von Benutzerkonten in der Benutzeroberfläche für Einstellungen wurden behoben.
- Viele Fehlerbehebungen machen den Betrieb reibungsloser und zuverlässiger.

## <a name="updates-for-version-1033"></a>Updates für Version 10.3.3

*Veröffentlicht am: 18.11.19*

Für das Release 10.3.3.3 haben wir ein Featureupdate erstellt und Fehlerbehebungen vorgenommen.

Zuerst haben wir Standardeinstellungen für Benutzer hinzugefügt, um Smartcard, Zwischenablage, Mikrofon, Kamera und Ordnerumleitung zu deaktivieren:

- ClientSettings.DisableSmartcardRedirection
- ClientSettings.DisableClipboardRedirection
- ClientSettings.DisableMicrophoneRedirection
- ClientSettings.DisableCameraRedirection
- ClientSettings.DisableFolderRedirection

Anschließend wurden folgende Fehler behoben:

- Ein Problem wurde behoben, durch das programmgesteuerte Sitzungsfenster-Größenänderungen nicht erkannt wurden.
- Ein Problem wurde behoben, bei dem der Sitzungsfensterinhalt beim Verbinden im Fenstermodus (bei aktivierter dynamischer Anzeige) klein erschien.
- Das anfängliche Flackern, das beim Herstellen der Verbindung mit einer Sitzung im Fenstermodus mit aktivierter dynamischer Anzeige auftrat, wurde beseitigt.
- Grafikfehler wurden behoben, die beim Herstellen der Verbindung mit Windows 7 nach dem Umschalten von „An Fenster anpassen“ bei aktivierter dynamischer Anzeige auftraten.
- Ein Fehler wurde behoben, der bewirkte, dass ein falscher Gerätename an die Remotesitzung gesendet wurde (was in einigen Drittanbieter-Apps zu Lizenzverlust führte).
- Ein Problem wurde gelöst, durch das Remote-App-Fenster beim Maximieren den kompletten Monitor ausfüllen.
- Ein Problem wurde behoben, bei dem die Benutzeroberfläche für Zugriffsberechtigungen unter lokalen Fenstern angezeigt wurde.
- Bestimmter Code für das Herunterfahren wurde bereinigt, um sicherzustellen, dass der Client zuverlässiger geschlossen wird.

## <a name="updates-for-version-1032"></a>Updates für Version 10.3.2

*Veröffentlicht am: 18.11.19*

In diesem Release wurde ein Fehler behoben, der bewirkte, dass die Anzeige beim Herstellen der Verbindung mit einer Sitzung in niedriger Auflösung dargestellt wurde

## <a name="updates-for-version-1031"></a>Updates für Version 10.3.1

*Veröffentlicht am: 18.11.19*

Für das Release 10.3.0 haben wir einige Korrekturen zusammengestellt, um Regressionen zu beheben, die es geschafft haben, sich in das Release 10.3.0 einzuschleichen.

- Probleme bei der Verbindung mit RD-Gatewayservern wurden behoben, die asymmetrische 4096-Bit-Schlüssel verwendeten.
- Ein Fehler wurde behoben, der dazu führte, dass der Client beim Herunterladen von Feedressourcen willkürlich nicht mehr reagierte.
- Ein Fehler wurde behoben, der dazu führte, dass der Client beim Öffnen abstürzte.
- Ein Fehler wurde behoben, der dazu führte, dass der Client beim Importieren von Verbindungen von Remotedesktop, Version 8, abstürzte.

## <a name="updates-for-version-1030"></a>Updates für Version 10.3.0

*Veröffentlicht am: 27.08.19*

Seit der letzten Aktualisierung sind einige Wochen vergangen, aber wir haben in dieser Zeit hart gearbeitet. Version 10.3.0 bietet einige neue Features und viele Korrekturen hinter den Kulissen.

- Kameraumleitung ist jetzt möglich, wenn eine Verbindung mit Windows 10 1809, Windows Server 2019 und höher hergestellt wird.
- Für Mojave und Catalina haben wir ein neues Dialogfeld hinzugefügt,das deine Erlaubnis anfordert, wenn Geräteumleitung für Mikrofon und Kamera verwendet werden soll.
- Der Feed-Abonnementablauf wurde neu geschrieben und ist jetzt einfacher und schneller.
- Die Umleitung der Zwischenablage schließt jetzt das RTF-Format (Rich-Text) ein.
- Bei der Kennworteingabe hast du jetzt die Option, es mithilfe des Kontrollkästchens „Kennwort anzeigen“ anzuzeigen.
- Es wurden Szenarien berücksichtigt, bei denen das Sitzungsfenster zwischen Monitoren hin- und her wechselte.
- Im Connection Center werden Remote-App-Symbole in hoher Auflösung angezeigt (sofern verfügbar).
- BEFEHL+A ist STRG+A zugeordnet, wenn Tastenkombinationen der Mac-Zwischenablage verwendet werden.
- BEFEHL+R aktualisiert jetzt alle von dir abonnierten Feeds.
- Es wurden neue Optionen für sekundäre Klicks hinzugefügt, um alle Gruppen oder Feeds im Connection Center zu erweitern oder zu reduzieren.
- Es wurde eine neue Option für sekundäre Klicks hinzugefügt, um die Symbolgröße auf der Feeds-Registerkarte im Connection Center zu ändern.
- Ein neues, vereinfachtes und übersichtliches App-Symbol.

## <a name="updates-for-version-10213"></a>Updates für Version 10.2.13

*Veröffentlicht am: 8.5.2019*

- Ein Problem mit einer Blockade beim Herstellen einer Verbindung über ein Remotedesktopgateway wurde behoben.
- Dem Dialogfeld „Feed hinzufügen“ wurde ein Datenschutzhinweis hinzugefügt.

## <a name="updates-for-version-10212"></a>Updates für Version 10.2.12

*Veröffentlicht am: 16.4.2019*

- Ein Problem mit zufälligen Verbindungstrennungen (mit Fehlercode 0x904) wurde behoben, das beim Herstellen einer Verbindung über ein Remotedesktopgateway auftrat.
- Ein Fehler wurde korrigiert, der zu einer leeren Auflösungsliste in den Anwendungseinstellungen nach einer Installation führte.
- Ein Fehler wurde korrigiert, der einen Absturz des Clients verursachte, wenn der Auflösungsliste bestimmte Auflösungen hinzugefügt wurden.
- Eine Schleife bei ADAL-Authentifizierungsaufforderungen wurde entfernt, die beim Herstellen einer Verbindung mit Bereitstellungen von virtuellen Windows-Desktops auftrat.

## <a name="updates-for-version-10210"></a>Updates für Version 10.2.10

*Veröffentlicht am: 30.3.2019*

- In dieser Version haben wir eine Instabilität behoben, die durch ein kürzlich erfolgtes Update für macOS 10.14.4 verursacht wurde. Wir haben außerdem Darstellungsfehler bei der Decodierung von AVC-Codecdaten korrigiert, die von einem Server mit NVIDIA-Hardware codiert wurden.

## <a name="updates-for-version-1029"></a>Updates für Version 10.2.9

*Veröffentlicht am: 6.3.2019*

- In dieser Version haben wir ein Konnektivitätsproblem beim Remotedesktopgateway behoben, das bei einer Serverumleitung auftreten kann.
- Wir haben auch eine Regression beim Remotedesktopgateway korrigiert, die durch das Update für 10.2.8 verursacht wurde.

## <a name="updates-for-version-1028"></a>Updates für Version 10.2.8

*Veröffentlicht am: 1.3.2019*

- Konnektivitätsprobleme wurden behoben, die beim Verwenden eines Remotedesktopgateways auftreten konnten.
- Falsche Zertifikatwarnungen wurden korrigiert, die beim Herstellen einer Verbindung angezeigt wurden.
- Es wurden einige Fälle korrigiert, bei denen beim Starten von Remote-Apps Menüleiste und Dock unnötigerweise ausgeblendet wurden.
- Der Code für die Umleitung aus der Zwischenablage wurde überarbeitet, um Probleme einiger Benutzer zu beheben, bei denen Systeme abstürzten oder nicht mehr reagierten.
- Ein Fehler wurde korrigiert, der dazu führte, dass das Connection Center beim Starten einer Verbindung unnötigerweise scrollt.

## <a name="updates-for-version-1027"></a>Updates für Version 10.2.7

*Veröffentlicht am: 6.2.2019*

- In dieser Version haben wir (durch einen Codierungsfehler auf dem Server entstandene) Grafikfehler korrigiert, die bei Verwendung des AVC444-Modus auftraten.

## <a name="updates-for-version-1026"></a>Updates für Version 10.2.6

*Veröffentlicht am: 28.1.2019*

- Wir haben Unterstützung für den AVC-Codec (420 und 444) hinzugefügt, der beim Herstellen einer Verbindung mit aktuellen Windows 10-Versionen verfügbar ist.
- Im Modus „An Fenster anpassen“ erfolgt die Fensteraktualisierung jetzt sofort nach einer Größenänderung, um sicherzustellen, dass der Inhalt auf der richtigen Interpolationsstufe gerendert wird.
- Ein Layoutfehler wurde korrigiert, der bei einigen Benutzern zu einem Überlappen von Feedkopfzeilen führte.
- Die Benutzeroberfläche für die Anwendungseinstellungen wurde überarbeitet.
- Die Benutzeroberfläche zum Hinzufügen und Bearbeiten von Desktops wurde optimiert.
- Die Anzeige der Kachel für das Connection Center und die Listenansichten für Desktops und Feeds wurden angepasst und optimiert.

>[!NOTE]
>In macOS 10.14.0 und 10.14.1 ist ein Fehler vorhanden, der dazu führen kann, dass der Ordner „.com.microsoft.rdc.application-data_SUPPORT/_EXTERNAL_DATA“ (der sich in einem Unterverzeichnis des Ordners „~/Library“ befindet) sehr viel Speicherplatz belegt. Um dieses Problem zu beheben, lösche die Inhalte dieses Ordners, und führe ein Upgrade auf macOS 10.14.2 durch. Beachte, dass beim Löschen von Ordnerinhalten auch Momentaufnahmenbilder gelöscht werden, die Lesezeichen zugewiesen sind. Diese Bilder werden erneut generiert, wenn erneut eine Verbindung mit dem Remote-PC hergestellt wird.

## <a name="updates-for-version-1024"></a>Updates für Version 10.2.4

*Veröffentlicht am: 18.12.2018*

- Unterstützung für den dunklen Modus für macOS Mojave 10.14 wurde hinzugefügt.
- Im Connection Center wird jetzt eine Option zum Importieren aus Microsoft-Remotedesktop 8 angezeigt, falls es leer ist.
- Die Kompatibilität der Ordnerumleitung mit einigen Unternehmensanwendungen von Drittanbietern wurde angepasst.
- Ein Problem wurde behoben, bei dem Benutzern aufgrund von Fallbackproblemen beim Sicherheitsprotokoll der Fehler „0x30000069“ für Remotedesktopgateway angezeigt wurde.
- Probleme mit dem progressiven Rendern wurden behoben, die bei einigen Benutzern beim Modus „An Fenster anpassen“ auftraten.
- Ein Fehler wurde behoben, der das Kopieren und Einfügen aus der letzten Version einer Datei verhinderte.
- Das Scrollen mit der Maus in kleinen Scrollbereichen wurde verbessert.

## <a name="updates-for-version-1023"></a>Updates für Version 10.2.3

*Veröffentlicht am: 06.11.2018*

- Unterstützung für die RDP-Dateieinstellung „remoteapplicationcmdline“ für Remote-App-Szenarien wurde hinzufügen.
- Der Titel des Sitzungsfensters enthält jetzt den Namen der RDP-Datei (und den Servernamen), wenn das Fenster über eine RDP-Datei gestartet wurde.
- Gemeldete Leistungsprobleme beim Remotedesktopgateway wurden behoben.
- Gemeldete Abstürze beim Remotedesktopgateway wurden behoben.
- Probleme mit nicht reagierenden Verbindungen über ein Remotedesktopgateway wurden behoben.
- Die Anzeige von Remote-Apps mit Vollbildschirm wurde durch intelligentes Ausblenden von Menüleiste und Dock verbessert.
- Szenarien wurden korrigiert, in denen Remote-Apps nach dem Start ausgeblendet blieben.
- Langsame Renderingupdates bei Verwendung der Option „An Fenster anpassen“ mit deaktivierter Hardwarebeschleunigung wurden behoben.
- Fehler bei der Datenbankerstellung wurden korrigiert, die durch falsche Berechtigungen beim Clientstart verursacht wurden.
- Ein Problem wurde behoben, bei dem bei einigen Benutzern der Client beim Start immer wieder abstürzte und nicht gestartet werden konnte.
- Ein Szenario wurde korrigiert, bei dem Verbindungen fälschlicherweise im Vollbildmodus aus Remotedesktop 8 importiert wurden.

## <a name="updates-for-version-1022"></a>Updates für Version 10.2.2

*Veröffentlicht am: 09.10.2018*

- Ein völlig neues Connection Center, das Drag & Drop-Vorgänge, die manuelle Gestaltung von Desktops, anpassbare Spalten im Listenansichtsmodus, spaltenbasiertes Sortieren und einfachere Gruppenverwaltung unterstützt.
- Das Connection Center merkt sich jetzt beim Schließen der App das zuletzt aktive Element (Desktops oder Feeds).
- Die Benutzeroberfläche und Flows für die Aufforderung zur Eingabe von Anmeldeinformationen wurden überarbeitet.
- Rückmeldungen aus dem Remotedesktopgateway gehören jetzt zur Benutzeroberfläche für den Verbindungsstatus.
- Der Import von Einstellungen aus Clients der Version 8 wurde verbessert.
- Remotedesktopprotokoll-Dateien, die auf RemoteApp-Endpunkte zeigen, können jetzt in das Connection Center importiert werden.
- Optimierungen für Retinadisplays in Remotedesktopszenarien mit einem Monitor.
- Unterstützung für die Angabe der Interpolationsstufe für Grafiken (die sich auf die Unschärfe auswirkt), wenn keine Retinaoptimierungen verwendet werden.
- Unterstützung für 256 Farben, um die Konnektivität mit Windows 2000 zu ermöglichen.
- Fehler beim Zuschneiden der rechten und unteren Seite eines Bildschirms wurden behoben, die beim Herstellen einer Verbindung mit Windows 7, Windows Server 2008 R2 und früheren Versionen auftraten.
- Beim Kopieren einer lokalen Datei in Outlook (ausgeführt in einer Remotesitzung) wird die Datei jetzt als Anlage hinzugefügt.
- Ein Problem wurde behoben, das Dateiübertragungen in die und aus der Zwischenablage verlangsamte, wenn die Dateien aus einer Netzwerkfreigabe stammten.
- Ein Fehler wurde korrigiert, der dazu führte, dass Excel (ausgeführt in einer Remotesitzung) nicht mehr reagierte, wenn eine Datei in einem umgeleiteten Ordner gespeichert wurde.
- Ein Problem wurde behoben, das dazu führte, dass für umgeleitete Ordner kein freier Speicherplatz gemeldet wurde.
- Ein Fehler wurde korrigiert, der dazu führte, dass Miniaturbilder unter macOS 10.14 zu viel Speicherplatz auf dem Datenträger belegten.
- Unterstützung für das Erzwingen von Remotedesktopgateway-Richtlinien für die Umleitung von Geräten wurde hinzugefügt.
- Ein Problem wurde behoben, das verhinderte, dass beim Trennen einer Verbindung über das Remotedesktopgateway Sitzungsfenster geschlossen wurden.
- Wenn die Authentifizierung auf Netzwerkebene (Network Level Authentication, NLA) nicht vom Server erzwungen wird, wirst du jetzt an den Anmeldebildschirm weitergeleitet, wenn dein Kennwort abgelaufen ist.
- Leistungsprobleme wurden behoben, die bei der Übertragung großer Datenmengen über das Netzwerk auftraten.
- Problembehebungen bei Smartcardumleitungen.
- Unterstützung für alle möglichen Werte der Remotedesktopprotokoll-Dateieinstellungen „EnableCredSspSupport“ und „Authentifizierungsebene“, wenn der Standardbenutzerschlüssel „ClientSettings.EnforceCredSSPSupport“ (in der Domäne „com.microsoft.rdc.macos“) auf 0 festgelegt ist.
- Unterstützung für die Remotedesktopprotokoll-Dateieinstellung „Zur Eingabe von Anmeldeinformationen auf dem Client auffordern“, wenn die Authentifizierung auf Netzwerkebene nicht ausgehandelt wurde.
- Unterstützung für die smartcardbasierte Anmeldung über eine Smartcardumleitung an der Eingabeaufforderung der Windows-Anmeldung, wenn die Authentifizierung auf Netzwerkebene nicht ausgehandelt wurde.
- Ein Problem wurde behoben, das das Herunterladen von Feedressourcen mit Leerzeichen in der URL verhinderte.

## <a name="updates-for-version-1021"></a>Updates für Version 10.2.1

*Veröffentlicht am: 06.08.2018*

- Konnektivität mit über Azure Active Directory (AAD) eingebundenen PCs wurde ermöglicht. Um eine Verbindung mit einem über AAD eingebundenen PC herzustellen, muss dein Benutzername in einem der folgenden Formate vorliegen: „AzureAD\Benutzer“ oder „AzureAD\user@domain“.
- Einige Fehler wurden korrigiert, die sich auf die Verwendung von Smartcards in einer Remotesitzung auswirkten.

## <a name="updates-for-version-1020"></a>Updates für Version 10.2.0

*Veröffentlicht am: 24.7.2018*

- Updates zum Zweck der Einhaltung der DSGVO wurden eingepflegt.
- MicrosoftAccount\username@domain wird jetzt als gültiger Benutzername akzeptiert.
- Die Freigabe der Zwischenablage wurde neu programmiert und ist jetzt schneller und unterstützt mehr Formate.
- Beim Kopieren und Einfügen von Text, Bildern oder Dateien zwischen Sitzungen wird jetzt die Zwischenablage des lokalen Computers umgangen.
- Du kannst jetzt mit einem nicht vertrauenswürdigen Zertifikat eine Verbindung über einen Remotedesktopgateway-Server herstellen (wenn du die Warnungen akzeptierst).
- Die Metal-Hardwarebeschleunigung wird jetzt verwendet (sofern unterstützt), um das Rendern zu beschleunigen und die Akkunutzung zu optimieren.
- Bei der Verwendung der Metal-Hardwarebeschleunigung wird versucht, die Grafiken in Sitzungen schärfer anzuzeigen.
- Einige Instanzen wurden entfernt, bei denen Fenster nach dem Schließen weiter sichtbar blieben.
- Fehler wurden korrigiert, die in einigen Szenarien den Start von RemoteApp-Programmen verhinderten.
- Ein Fehler bei der Kanalsynchronisierung im Remotedesktopgateway wurde korrigiert, der zu 0x204-Fehlern führte.
- Die Form des Mauszeigers wird jetzt ordnungsgemäß aktualisiert, wenn die Maus aus einem Sitzungs- oder RemoteApp-Fenster herausbewegt wird.
- Ein Fehler bei der Ordnerumleitung wurde korrigiert, der beim Kopieren und Einfügen von Ordnern zu Datenverlust führte.
- Ein Problem mit der Ordnerumleitung wurde behoben, das eine fehlerhafte Meldung von Ordnergrößen verursachte.
- Eine Regression wurde korrigiert, die eine Anmeldung bei einem über AAD eingebundenen Computer mit einem lokalen Konto verhinderte.
- Fehler wurden korrigiert, die dazu führten, dass die Inhalte von Sitzungsfenstern abgeschnitten wurden.
- Unterstützung für Remotedesktop-Endpunktzertifikate wurde hinzugefügt, die elliptische asymmetrische Schlüssel enthalten.
- Ein Fehler wurde korrigiert, der in einigen Szenarien das Herunterladen von verwalteten Ressourcen verhinderte.
- Ein Problem mit abgeschnittenen Inhalten im angehefteten Connection Center wurde behoben.
- Sie finden die Kontrollkästchen für bessere Zusammenarbeit im Fenster „Desktop hinzufügen“ auf dem Blatt mit den Anzeigeeigenschaften.
- Das Sperren des Seitenverhältnisses ist jetzt deaktiviert, wenn die dynamische Anzeigeänderung aktiviert ist.
- Kompatibilitätsprobleme mit der F5-Infrastruktur wurden behoben.
- Die Verarbeitung von leeren Kennwörtern wurde aktualisiert, um sicherzustellen, dass zum Zeitpunkt der Verbindungsherstellung die richtigen Meldungen angezeigt werden.
- Kompatibilitätsprobleme beim Scrollen mit der Maus in MapInfra Pro wurden behoben.
- Einige Ausrichtungsprobleme im Connection Center wurden behoben, die bei der Ausführung unter Mojave auftraten.

## <a name="updates-for-version-1018"></a>Updates für Version 10.1.8

*Veröffentlicht am: 4.5.2018*

- Unterstützung für das Ändern der Remoteauflösung durch Ändern der Größe des Sitzungsfensters wurde hinzugefügt.
- Szenarien wurden korrigiert, in denen das Herunterladen von Remoteressourcenfeeds übermäßig lange dauerte.
- Der 0x207-Fehler wurde korrigiert, der beim Herstellen einer Verbindung mit Servern auftreten konnte, die nicht mit dem CredSSP-Update für „Encryption Oracle Remediation“ (CVE-2018-0886) gepatcht sind.

## <a name="updates-for-version-1017"></a>Updates für Version 10.1.7

*Veröffentlicht am: 5.4.2018*

- Sicherheitsfixes zur Einbindung von CredSSP-Updates für „Encryption Oracle Remediation“, wie in CVE-2018-0886 beschrieben.
- Das Rendering von RemoteApp-Symbol und -Mauszeiger wurde verbessert, um gemeldete Darstellungsfehler zu beheben.
- Ein Problem wurde behoben, das dazu führte, dass RemoteApp-Fenster hinter dem Connection Center angezeigt wurden.
- Ein Problem wurde behoben, das beim Bearbeiten von lokalen Ressourcen nach dem Importieren aus Remotedesktop 8 auftrat.
- Du kannst jetzt eine Verbindung starten, indem du auf einer Desktopkachel die EINGABETASTE drückst.
- Im Vollbildmodus wird BEFEHLSTASTE+M jetzt ordnungsgemäß zu WINDOWS-TASTE+M zugeordnet.
- Die Fenster „Connection Center“, „Einstellungen“ und „Info“ reagieren jetzt auf BEFEHLSTASTE+M.
- Du kannst mit dem Erkunden von Feeds beginnen, indem du auf der Seite **Remoteressourcen hinzufügen** die EINGABETASTE drückst.
- Ein Fehler wurde behoben, der dazu führte, dass ein neuer Remoteressourcenfeed im Connection Center leer war, bis die Anzeige aktualisiert wurde.

## <a name="updates-for-version-1016"></a>Updates für Version 10.1.6

*Veröffentlicht am: 26.3.2018*

- Ein Problem wurde behoben, bei dem RemoteApp-Fenster sich selbst neu anordneten.
- Ein Fehler wurde korrigiert, der dazu führte, dass einige RemoteApp-Fenster hinter dem übergeordneten Fenster hängenblieben.
- Ein Versatzproblem beim Mauszeiger wurde behoben, das sich auf einige RemoteApp-Programme auswirkte.
- Ein Problem wurde behoben, bei dem beim Starten einer neuen Verbindung kein neues Sitzungsfenster geöffnet wurde, sondern eine vorhandene Sitzung den Fokus erhielt.
- Wir haben einen Fehler bei einer Fehlermeldung korrigiert: Dir wird jetzt die richtige Meldung angezeigt, wenn dein Gateway nicht gefunden wird.
- Der Tastaturbefehl zum Beenden (⌘ + Q) wird jetzt dauerhaft auf der Benutzeroberfläche angezeigt.
- Die Bildqualität beim Strecken in den Modus „An Fenster anpassen“ wurde verbessert.
- Eine Regression wurde korrigiert, die dazu führte, dass in einer Remotesitzung mehrere Instanzen des Basisordners angezeigt wurden.
- Das Standardsymbol für Desktopkacheln wurde aktualisiert.
