---
title: Neuigkeiten für Remotedesktop auf Mac
description: Erfahren Sie mehr über die aktuellen Änderungen an den Remotedesktop-Client für Mac
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 03/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: 11da8bc333da7f44b2732266837d2df216142f85
ms.sourcegitcommit: 971f6538e8d89af84ef50fc8aab2188bdf6f47cb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2019
ms.locfileid: "9279121"
---
# <a name="whats-new-for-the-remote-desktop-client-on-macos"></a>Neuigkeiten für den Remotedesktop-Client auf MacOS?

Wir aktualisieren regelmäßig den [Remotedesktopclient für MacOS](remote-desktop-mac.md), Hinzufügen neuer Funktionen und Behebung von Problemen. Sehen Sie sich die neuesten Updates unten.

Falls Probleme auftreten, können Sie uns immer über die **neuesten > Bericht ein Problem**wenden.

## <a name="updates-for-version-10210"></a>Updates für Version 10.2.10
*Datum der Veröffentlichung: 30/3/2019*

- In dieser Version behandelt wir machen, die durch das aktuelle Update MacOS 10.14.4 verursacht. Wir haben auch Mispaints, die angezeigt wird, bei der Decodierung von AVC Codecdaten von einem Server mit der NVIDIA-Hardware-codierte behoben.

## <a name="updates-for-version-1029"></a>Updates für Version 10.2.9
*Datum der Veröffentlichung: 6/3/2019*

- Platzieren Sie in dieser Version, die wir ein RD-Gateway-Konnektivitätsproblem, die auftreten können behoben, wenn Server Umleitung ausführt.
- Wir behandelt auch einen RD-Gateway Regression zurückzuführen, dass die 10.2.8 Update.

## <a name="updates-for-version-1028"></a>Updates für Version 10.2.8
*Datum der Veröffentlichung: 1/3/2019*

- Aufgelöst Probleme mit der Netzwerkkonnektivität, die bei Verwendung von RD-Gateway dargestellt.
- Feste falsch Zertifikat Warnungen, die beim Herstellen einer Verbindung angezeigt wurden.
- Behandelt einige Fälle, in denen die Menüleiste und Dock unnötigerweise zu beim Starten von remote-apps verbergen.
- Überarbeitet den Zwischenablage Umleitungscode Adresse abstürzen und Blockaden, die Probleme von einige Benutzer.
- Einen Fehler, der die Verbindung Center unnötigerweise Bildlauf beim Starten einer Verbindungs verursacht behoben.

## <a name="updates-for-version-1027"></a>Updates für Version 10.2.7
*Datum der Veröffentlichung: 2/6/2019*

- In dieser Version behandelt wir Grafiken Mispaints (durch einen Server encoding Fehler verursacht), die bei Verwendung des AVC444 Modus angezeigt.

## <a name="updates-for-version-1026"></a>Updates für Version 10.2.6
*Datum der Veröffentlichung: 1/28/2019*

- Unterstützung für den Codec AVC (420 und 444), die beim Verbinden mit aktuellen Versionen von Windows 10 verfügbar.
- Im Fenstermodus Bildschirmgröße anpassen, eine Aktualisierung eines Fensters jetzt tritt unmittelbar nach dem eine Größe ändern, um sicherzustellen, dass der Inhalt auf der Ebene der richtigen Interpolation gerendert wird.
- Einen Layout-Fehler, der für einige Benutzer überlappen feed Header verursacht behoben.
- Die Benutzeroberfläche der Anwendung Voreinstellungen werden bereinigt.
- Optimierte die Desktop hinzufügen/bearbeiten-Benutzeroberfläche.
- Gemacht viele anpassen und Fertigstellen Anpassungen, die die Verbindung Center Kachel- und Liste Ansichten für Desktops und Feeds.

>[!NOTE]
>Eine große Menge an Speicherplatz nutzen ist ein Fehler in MacOS 10.14.0 und 10.14.1, die die ".com.microsoft.rdc.application-data_SUPPORT/_EXTERNAL_DATA" verursachen können Ordner (geschachtelte tiefen Einblick in den Ordner "~/Library") vorhanden. Um dieses Problem zu beheben, löschen Sie den Ordnerinhalt, und Aktualisieren auf MacOS 10.14.2. Beachten Sie, dass ein Nebeneffekt, dass die Ordner Inhalte besteht darin, dass Snapshot-Bilder, Lesezeichen zugewiesen werden gelöscht. Diese Bilder werden neu erstellt werden, wenn erneut eine Verbindung mit dem remote-PC herstellen.

## <a name="updates-for-version-1024"></a>Updates für Version 10.2.4
*Datum der Veröffentlichung: 12/18/2018*

- Dunklen Modus-Unterstützung für MacOS Mojave 10.14 hinzugefügt.
- Eine Option zum Importieren von von Microsoft Remote Desktop 8 jetzt wird in der Mitte Verbindung angezeigt, wenn sie leer ist.
- Behandelt Ordner Umleitung Kompatibilität mit einigen Drittanbieter-unternehmensanwendungen.
- Behobene Probleme, in denen Benutzer eine 0x30000069 Remotedesktopgateway Fehler aufgrund der Sicherheit Protokoll fallback Probleme beim Abrufen wurden.
- Feste progressive Renderingprobleme, die, denen einige Benutzer mit jedem, passen, um eine Fenstermodus.
- Einem Fehler behoben, die verhindert, dass Datei kopieren und Einfügen aus kopieren die neueste Version der Datei.
- Verbesserte mausbasierte Bildlauf für kleinen Bildlauf Deltas.

## <a name="updates-for-version-1023"></a>Updates für Version 10.2.3
*Datum der Veröffentlichung: 11/06/2018*

- Unterstützung für die Einstellung "Remoteapplicationcmdline" RDP-Datei für remote-app-Szenarien.
- Der Titel des Sitzungsfensters enthält nun u. a. den Namen des die RDP-Datei (und Servername) in eine RDP-Datei gestartet wird.
- Feste gemeldeten RD-Gateway-Leistungsprobleme.
- Feste gemeldeten RD-Gateway stürzt ab.
- Behobene Probleme, in denen die Verbindung beim Herstellen einer Verbindung über einen RD-Gateway Blockade würde.
- Behandlung von remote Vollbild-apps durch Intelligent Ausblenden der Menüleiste besser und Andocken.
- Feste Szenarien, in denen remote apps ausgeblendet beibehalten, nachdem er gestartet wurde.
- Slow Rendering-Updates behandelt, bei Verwendung von "An Fenster anpassen" mit Hardwarebeschleunigung deaktiviert.
- Behandelt Datenbankfehler-Erstellung durch falsche Berechtigungen verursacht werden, wenn der Client wird gestartet. 
- Festen ein Problem wurde, in dem der Client beim Start konsistent abstürzt und nicht für einige Benutzer ab.
- Feste ein Szenario, in denen wurden Verbindungen falsch als Vollbild-von Remote Desktop 8 importiert.

## <a name="updates-for-version-1022"></a>Updates für Version 10.2.2
*Datum der Veröffentlichung: 10/09/2018*

- Ein völlig neues Verbindung-Center, das unterstützt Drag & Drop, manuelle Anordnung von Desktops, veränderbare Spalten im Modus der Listenansicht, Spalte-basierte sortieren und einfachere Verwaltung.
- Die Verbindung Center jetzt speichert das letzte aktive Pivot (Desktops oder Feeds) beim Schließen der app.
- Wurden die Anmeldeinformationen aufgefordert werden, Benutzeroberfläche und Flüsse überholt.
- RD-Gateway Feedback ist jetzt Teil des verbinden Status UI.
- Importieren der Einstellungen vom Client Version 8 wurde verbessert.
- RDP-Dateien, die auf RemoteApp-Endpunkte zeigen können jetzt in der Mitte Verbindung importiert werden.
- Netzhaut Display Optimierungen für einzelne Monitor Remotedesktop-Szenarien.
- Unterstützung für die Angabe der Grafiken Interpolation Ebene (die Unschärfe wirkt sich auf) bei nicht Netzhaut Optimierungen verwendet.
- Unterstützung von 256 Farben um Konnektivität mit Windows 2000 zu aktivieren.
- Mit fester Zuschneiden von den rechten und unteren Rand des Bildschirms beim Herstellen von Windows 7, WindowsServer 2008 R2 und früheren Versionen.
- Kopieren eine lokale Datei jetzt in Outlook (ausgeführt in einer Remotesitzung), wird die Datei als Anlage hinzugefügt.
- Feste ein Problem, das nach unten Arbeitsbereich-basierte Datei Übertragungen langsam wurde, wenn die Dateien von einer Netzwerkfreigabe stammt.
- Behandelt einen Fehler, der nach Excel (ausgeführt in einer Remotesitzung) verantwortlich war, abstürzt, wenn in einer Datei auf einen umgeleitete Ordner speichern.
- Feste ein Problem, das keine freien Speicherplatz für umgeleitete Ordner gemeldet werden verursacht hat.
- Einen Fehler, die Miniaturansichten nutzen zu viel Speicher auf MacOS 10.14 verursacht behoben.
- Unterstützung für RD-Gateway Gerät Umleitung Richtlinien durchgesetzt werden.
- Feste ein Problem, das Schließen Sitzung Windows verhindert werden, wenn Sie über eine Verbindung mit Remotedesktopgateway trennen.
- Wenn Authentifizierung (Netzwerk Ebene Authentifizierung auf Netzwerkebene) vom Server nicht erzwungen wird, werden Sie jetzt an die Anmeldeseite weitergeleitet werden, wenn Ihr Kennwort abgelaufen ist.
- Leistungsprobleme, die beim ermittlungsfunktionen behoben wurde viele Daten über das Netzwerk übertragen wird.
- Umleitung von Smartcards behebt.
- Unterstützung für alle möglichen Werte für die "EnableCredSspSupport" und "Authentifizierungsebene" RDP-dateieinstellungen Wenn ClientSettings.EnforceCredSSPSupport Standard Benutzerschlüssel (in der Domäne com.microsoft.rdc.macos) auf 0 festgelegt ist.
- Unterstützung für die Einstellung der "Für Anmeldeinformationen auf Client anfordern" RDP-Datei bei der Authentifizierung auf Netzwerkebene nicht ausgehandelt wird.
- Unterstützung für die Smartcard-basierte Anmeldung über Smartcard-Umleitung an der Eingabeaufforderung Winlogon, während die Authentifizierung auf Netzwerkebene nicht ausgehandelt wird.
- Ein Problem, die verhindert, dass das Herunterladen von Ressourcen mit Leerzeichen in der URL feed wurde behoben.

## <a name="updates-for-version-1021"></a>Updates für Version 10.2.1
*Datum der Veröffentlichung: 08/06/2018*

- Aktiviert Konnektivität zu Azure Active Directory (AAD) eingebundene PCs. Zum Herstellen einer AAD gehören PC, Ihren Benutzernamen muss in einem der folgenden Formate: "AzureAD\user" oder "AzureAD\user@domain".
- Behandelt einige Fehler, die Auswirkung auf die Verwendung von Smartcards in einer Remotesitzung vereinen.

## <a name="updates-for-version-1020"></a>Updates für Version 10.2.0
*Datum der Veröffentlichung: 07/24/2018*

- Eingebundenen Updates zur Einhaltung der DSGVO.
- MicrosoftAccount\username@domainwird jetzt als einen gültigen Benutzernamen akzeptiert.
- Gemeinsame Nutzung der Zwischenablage wurde neu geschrieben schneller und Weitere Formate unterstützt.
- Kopieren und Einfügen von Text, Bilder oder Dateien zwischen Sitzungen jetzt entfällt die Zwischenablage des lokalen Computers.
- Sie können jetzt über einen RD-Gateway-Server mit einem nicht vertrauenswürdigen Zertifikat verbinden (Wenn Sie die Warnung Anweisungen akzeptieren).
- Metal Hardwarebeschleunigung ist jetzt (sofern unterstützt) verwendet, um Rendering beschleunigen und Akkunutzung zu optimieren.
- Nach der Verwendung von Metal Hardwarebeschleunigung wir versuchen, funktionieren einige Magic, um sicherzustellen, werden die Sitzung Grafiken scharfe angezeigt.
- Haben Sie einigen Fällen entfernen, in denen Windows Blockade würde um nach geschlossen wird.
- Behobenen Problemen, die den Start von RemoteApp-Programmen in einigen Szenarien verhindert wurden.
- Feste RD-Gateway Kanal Synchronisierungsfehler, der in 0x204 Fehlern resultierenden wurde.
- Die Maus Cursorform aktualisiert jetzt ordnungsgemäß beim Bewegen aus aus einer Sitzung oder RemoteApp-Fenster.
- Einen Ordner Umleitung Fehler, die Datenverluste verursachen, wurde behoben beim Kopieren und Einfügen von Ordnern.
- Ein Ordner Umleitung Problem, die fehlerhafte Berichte Ordner Größen verursacht wurde behoben.
- Feste eine Regression, die Anmeldung bei einem AAD eingebundenen Computer mithilfe eines lokalen Kontos verhindert hat.
- Behobenen Problemen, die die Sitzung Fensterinhalte abgeschnitten wird verursacht wurden.
- Unterstützung für Remotedesktop-Endpunkt-Zertifikate, die ECDSA Kurve asymmetrische Schlüssel enthalten.
- Einen Fehler, der den Download von verwalteten Ressourcen in einigen Szenarien verhindert wurde behoben.
- Behandelt ein Problem Zuschneiden mit der angehefteten Verbindungscenter.
- Die Kontrollkästchen behoben in der zeigt die Eigenschaftenseite besser zusammenarbeiten.
- Seitenverhältnis sperren ist jetzt deaktiviert, wenn die Änderung der dynamischen Anzeige aktiv ist.
- Behandelt Kompatibilitätsprobleme mit F5-Infrastruktur.
- Aktualisiert die Behandlung von leeren Kennwörtern um sicherzustellen, dass die richtigen Nachrichten zum Zeitpunkt der Verbindung angezeigt werden.
- Feste Blättern mit der Maus Kompatibilitätsprobleme mit MapInfra Pro.
- Einige Ausrichtungsprobleme behoben in der Mitte Verbindung, während der Ausführung auf Mojave.

## <a name="updates-for-version-1018"></a>Updates für Version 10.1.8
*Datum der Veröffentlichung: 05/04/2018*

- Unterstützung für das Ändern der remote Auflösung von der Größe des Sitzungsfensters!
- Feste Szenarien, in denen remote Ressource Download Feed, würde übermäßig lange dauern.
- Den 0x207-Fehler, der auftreten können, bei der Verbindung mit Servern, die nicht mit dem CredSSP Verschlüsselung Oracle Wartung-Update (CVE-2018-0886) gepatcht wird aufgelöst.

## <a name="updates-for-version-1017"></a>Updates für Version 10.1.7 für
*Datum der Veröffentlichung: 04/05/2018*

- Gemacht Sicherheitspatches CredSSP Verschlüsselung Oracle Wartung Updates integrieren, wie in CVE-2018-0886 beschrieben.
- Verbesserte RemoteApp-Symbol und Maus Cursor Rendering gemeldeten Mispaints kümmern.
- Behandelt Probleme, in denen RemoteApp Windows hinter dem Center Verbindung angezeigt wurde.
- Behebt ein Problem, die aufgetreten sind, wenn Sie lokale Ressourcen nach dem Importieren von Remote Desktop 8 bearbeiten.
- Nun können Sie eine Verbindung mit der EINGABETASTE auf einem desktop-Kachel.
- Wenn Sie in der Vollbildansicht sind, ordnet CMD + M jetzt ordnungsgemäß WIN + M.
- Die Verbindung Center, Einstellungen und Informationen zum Windows reagieren Sie jetzt auf CMD + M.
- Nun können Sie ermitteln von Feeds durch Drücken der EINGABETASTE auf der Seite " **Remote-Ressourcen hinzufügen** ".
- Ein Problem behoben wurde, in denen ein neues remote-Ressourcen-Feed oben in der Mitte Verbindung bis leeren gezeigt, nachdem Sie aktualisiert.
 
## <a name="updates-for-version-1016"></a>Updates für Version 10.1.6
*Datum der Veröffentlichung: 03/26/2018*

- Ein Problem behoben, in denen würde RemoteApp Windows selbst neu anzuordnen.
- Aufgelöst einen Fehler, der einige RemoteApp Windows hinter ihren übergeordneten Fensters weiterkommen verursacht hat.
- Behandelt ein Offset Mauszeiger-Problem, das einige RemoteApp-Programme betroffen.
- Ein Problem behoben, in denen gegeben haben Starten einer neuen Verbindungs den Fokus zu einer vorhandenen Sitzung, statt eine neue Sitzung-Fenster.
- Wir haben einen Fehler behoben, mit einer Fehlermeldung – sehen Sie die richtige Nachricht jetzt Wenn wir das Gateway nicht finden können.
- Die Verknüpfung beenden (⌘ + Q) wird jetzt konsistent in der Benutzeroberfläche angezeigt.
- Verbessert die Bildqualität, wenn im Modus "an Fenster anpassen" gestreckt.
- Feste eine Regression, die mehrere Instanzen des Ordners "Privat" in der Remotesitzung angezeigt werden verursacht hat.
- Aktualisiert die Standardsymbol für desktop-Kacheln.
