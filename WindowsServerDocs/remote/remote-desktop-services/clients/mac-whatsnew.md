---
title: Neuerungen für Remotedesktop auf Mac
description: Erfahren Sie mehr über die letzten Änderungen an den Remotedesktopclient für Mac
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
ms.openlocfilehash: d0cf81f24374e81ca28c2d2cfd83a394e096706c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844791"
---
# <a name="whats-new-for-the-remote-desktop-client-on-macos"></a>Neuigkeiten für den Remotedesktop-Client unter macOS

Wir aktualisieren regelmäßig die [Remotedesktop-Client für MacOS](remote-desktop-mac.md), neue Features hinzugefügt wurden, und Beheben von Problemen. Sehen Sie sich die neuesten Updates, die weiter unten.

Wenn Probleme auftreten, Sie können immer kontaktieren Sie uns über **Hilfe > ein Problem melden**.

## <a name="updates-for-version-1029"></a>Updates für Version 10.2.9
*Veröffentlichungsdatum: 3/6/2019*

- In dieser Version, die wir ein RD-Gateway-Konnektivitätsproblem, die auftreten können behoben, wenn die Umleitung wird zu platzieren.
- Wir auch eine RD-Gateway-Regression durch die 10.2.8 adressiert aktualisieren.

## <a name="updates-for-version-1028"></a>Updates für Version 10.2.8
*Veröffentlichungsdatum: 3/1/2019*

- Behobene Konnektivitätsprobleme, der angezeigt wird, wenn Sie ein RD-Gateway verwenden.
- Korrigiert falsche zertifikatwarnungen, die beim Herstellen einer Verbindung angezeigt wurden.
- Behandelt einige Fälle, in der Menüleiste und Andocken unnötig beim Starten von remote-apps verdecken würde.
- Überarbeitet, den Zwischenablage-Umleitung-Code zum Adresse Abstürze und Einfrieren, die Probleme von einigen Benutzern.
- Korrektur eines Fehlers, das das Connection Center unnötig Bildlaufes beim Drehen starten eine Verbindung verursacht hat.

## <a name="updates-for-version-1027"></a>Updates für Version 10.2.7
*Veröffentlichungsdatum: 2/6/2019*

- In dieser Version behoben wir Mispaints von Grafiken (verursacht durch einen Codierung Server-Fehler), die angezeigt wurden, bei Verwendung des AVC444-Modus.

## <a name="updates-for-version-1026"></a>Updates für Version 10.2.6
*Veröffentlichungsdatum: 1/28/2019*

- Unterstützung für den Codec AVC (420 und 444), die beim Verbinden mit aktuellen Versionen von Windows 10 verfügbar.
- In an Fenstermodus anpassen, eine Aktualisierung der Fenster nun tritt sofort nach dem auf der Ebene des richtigen Interpolation eine Größe aus, um sicherzustellen, dass der Inhalt gerendert wird.
- Korrektur eines Layout-Fehlers, das feed-Header für einige Benutzer überlappen verursacht hat.
- Die Benutzeroberfläche der Anwendung Einstellungen werden bereinigt.
- Optimierte die hinzufügen/bearbeiten von Desktop-Benutzeroberfläche.
- Versucht, viele anpassen und Fertigstellen Anpassungen vor, um das Connection Center Kachel und den Listenansichten für Desktops und Feeds.

>[!NOTE]
>Es ist ein Fehler im Ordner "MacOS 10.14.0 und 10.14.1, die die".com.microsoft.rdc.application-data_SUPPORT/_EXTERNAL_DATA"verursachen können" (geschachtelt tief im Ordner "~/Library"), um eine große Menge an Speicherplatz zu nutzen. Um dieses Problem zu beheben, löschen Sie den Ordnerinhalt, und ein upgrade auf MacOS 10.14.2. Beachten Sie, dass ein Nebeneffekt, dass der Inhalt des Ordners löschen, Momentaufnahmen, die zugewiesenen Lesezeichen gelöscht werden. Diese Images werden erneut generiert werden, beim Wiederherstellen der Verbindung mit dem remote-PC.

## <a name="updates-for-version-1024"></a>Updates für Version 10.2.4
*Veröffentlichungsdatum: 12/18/2018*

- Dunkel modusunterstützung für MacOS Mojave 10.14 hinzugefügt.
- Eine Option aus, um die von Microsoft Remote Desktop 8. nun importieren wird im Connection Center angezeigt, wenn es leer ist.
- Behandelt die Ordner-Umleitung-Kompatibilität mit manchen unternehmensanwendungen von Drittanbietern.
- Behobene Probleme, in dem Benutzer ein 0x30000069 Remotedesktop-Gateway-Fehler aufgrund von Sicherheit Probleme beim Protokoll abrufen, enthalten.
- Feste progressives Rendering-Problemen, die, denen einige Benutzer mit aufgetreten war, das Anpassen an ausgeführt.
- Korrektur eines Fehlers, der verhinderte Kopieren der Datei, und fügen Sie daran, die neueste Version einer Datei zu kopieren.
- Verbessert die Maus-basierte Bildlauf für kleinen Bildlauf Deltas.

## <a name="updates-for-version-1023"></a>Updates für Version 10.2.3
*Veröffentlichungsdatum: 11/06/2018*

- Unterstützung für die Einstellung "Remoteapplicationcmdline" RDP-Datei für remote-app-Szenarien.
- Der Titel des Fensters enthält jetzt den Namen des RDP-Datei (und Servername) Wenn Sie über eine RDP-Datei gestartet.
- Korrektur gemeldeten RD Gateway-Leistungsprobleme.
- Feste gemeldeten RD-Gateway stürzt ab.
- Behobene Probleme, in dem die Verbindung reagierte, wenn über das RD Gateway eine Verbindung herstellen.
- Bessere Verarbeitung von Vollbild-remote-apps, indem Sie auf intelligente Weise ausblenden, die Menüleiste und Andocken.
- Feste Szenarien, in dem RemoteApp ausgeblendet bleibt, nachdem er gestartet wurde.
- Langsame Rendering Updates behoben, bei Verwendung von "An Fenster anpassen" mit Hardwarebeschleunigung, die deaktiviert.
- Behandelt die Erstellung Datenbankfehler, die durch falsche Berechtigungen verursacht werden, wenn der Client wird gestartet. 
- Wurde behoben ein Problem, in dem der Client konsistent beim Start abstürzt und nicht für einige Benutzer ab.
- Korrektur ein Szenarios, in denen wurden Verbindungen nicht ordnungsgemäß als Vollbild-Schutz von Remote Desktop 8. importiert.

## <a name="updates-for-version-1022"></a>Updates für Version 10.2.2
*Veröffentlichungsdatum: 10/09/2018*

- Eine völlig neue Connection Center, das unterstützt Drag & drop, manuelle Anordnung von Desktops, veränderbare Spalten in den Modus der Listenansicht, spaltenbasierte sortieren und einfachere Verwaltung.
- Connection Center jetzt erinnert sich das letzte aktive Pivot-Element ("Desktops" oder "Feeds") beim Schließen der app.
- Die Anmeldeinformationen aufzufordern, Benutzeroberfläche und Flows wurden überholt.
- RD-Gateway-Feedback ist jetzt Teil der Benutzeroberfläche für eine Verbindung herstellen Status.
- Importieren von Einstellungen auf dem Client der Version 8 wurde verbessert.
- RDP-Dateien, die auf der RemoteApp-Endpunkte können jetzt in das Connection Center importiert werden.
- Retina Display Optimierungen für die einzelnen Monitor Remote Desktop-Szenarien.
- Unterstützung für die Angabe der Ebene der Grafik-Interpolation (die Unschärfe wirkt sich auf.) Wenn Retina-Optimierungen nicht verwendet.
- 256-Farben-Unterstützung für die Verbindung mit Windows 2000 zu aktivieren.
- Korrektur Kürzen von den rechten und unteren Rand des Bildschirms beim Verbinden mit Windows 7, WindowsServer 2008 R2 und früher.
- Kopieren jetzt eine lokale Datei in Outlook (die in einer Remotesitzung ausgeführt wird), wird die Datei als Anlage hinzugefügt.
- Ein Problem wurde behoben, die den Zwischenablage-basierte dateiübertragungen verlangsamen wurde, wenn die Dateien über ein freigegebenes Netzwerk stammt.
- Behandelt einen Fehler auf, der in Excel (die in einer Remotesitzung ausgeführt wird) verursacht wurde, nicht mehr reagiert, wenn in einer Datei in einem umgeleiteten Ordner speichern.
- Ein Problem wurde behoben, das kein Speicherplatz für umgeleitete Ordner gemeldet werden, verursacht wurde.
- Korrektur eines Fehlers, die Miniaturansichten zu viel Speicherplatz auf MacOS 10.14 nutzen verursacht hat.
- Unterstützung für die Umsetzung von RD-Gateway-Umleitung Geräterichtlinien hinzugefügt.
- Ein Problem wurde behoben, das Sitzungsfenster schließen verhindert, bei der Verbindung mit einer Verbindung mit RD-Gateway getrennt wird.
- Wenn (Network Level Authentication, NLA) nicht vom Server erzwungen wird, werden Sie jetzt zur Anmeldeseite weitergeleitet werden, wenn Ihr Kennwort abgelaufen ist.
- Korrigiert Leistungsprobleme, die beim tauchen viele Daten wurde über das Netzwerk übertragen werden.
- Umleitung von Smartcards behoben.
- Unterstützung für alle möglichen Werte der "EnableCredSspSupport" und "Authentifizierungsebene" RDP-dateieinstellungen Wenn der Standardschlüssel des ClientSettings.EnforceCredSSPSupport-Benutzer (in der Domäne com.microsoft.rdc.macos) auf 0 festgelegt ist.
- Unterstützung für die Einstellung der "Eingabeaufforderung für Anmeldeinformationen auf Client" RDP-Datei bei der Authentifizierung auf Netzwerkebene keine ausgehandelt wird.
- Unterstützung für die Smartcard-basierte Anmeldung über die Umleitung der Smartcard an der Eingabeaufforderung für Windows-Anmeldung bei der Authentifizierung auf Netzwerkebene keine ausgehandelt wird.
- Ein Problem wurde behoben, der verhinderte, Download des Feeds von Ressourcen, die Leerzeichen in der URL enthalten.

## <a name="updates-for-version-1021"></a>Updates für Version 10.2.1
*Veröffentlichungsdatum: 08/06/2018*

- Aktiviert Konnektivität zu Azure Active Directory (AAD) eingebundene PCs. Zum Herstellen einer Verbindung mit eine AAD eingebundenen PC handeln, Ihren Benutzernamen muss eines der folgenden Formate: "AzureAD\user" oder "AzureAD\user@domain".
- Behandelt einige Fehler, die Auswirkungen auf die Verwendung von Smartcards in einer Remotesitzung.

## <a name="updates-for-version-1020"></a>Updates für Version 10.2.0
*Veröffentlichungsdatum: 07/24/2018*

- Eingefügten Updates für die Einhaltung der dsgvo.
- MicrosoftAccount\username@domain wird nun als einen gültigen Benutzernamen akzeptiert werden.
- Freigabe der Zwischenablage wurde umgeschrieben, um schneller ausgeführt wird und Weitere Formate unterstützen.
- Kopieren und Einfügen von Text, Bilder oder Dateien zwischen den Sitzungen jetzt umgeht die Zwischenablage des lokalen Computers.
- Sie können jetzt über einen Remotedesktop-Gatewayserver mit einem nicht vertrauenswürdigen Zertifikat herstellen, (Wenn Sie die Warnung aufforderungen akzeptiert haben).
- -Metal-Hardware-Beschleunigung wird jetzt (sofern unterstützt) verwendet, um Rendering zu beschleunigen und zu Akkunutzung optimieren.
- Nach der Verwendung von-Metal-Hardware Acceleration wir versuchen, die Magie zu arbeiten, an die Sitzung Grafiken schärfere erscheinen.
- Wurde von einigen Instanzen entfernen, in denen Windows würde auf dem Auflegen geschlossen wird.
- Behobene Programmfehler, die den Start des RemoteApp-Programme in einigen Szenarien verhindert wurden.
- Wurde ein Synchronisierungsfehler RD-Gateway-Kanal, die sich in 0x204 Fehler ergeben wurde behoben.
- Die Mauscursorform aktualisiert nun ordnungsgemäß, wenn einer Sitzung oder die RemoteApp-Fenster verlassen.
- Korrektur eines Fehlers der Ordner-Umleitung, die Datenverlust verursacht, wurde beim Kopieren und Einfügen von Ordnern.
- Ein Ordner-Umleitung-Problem, das verursacht hat, fehlerhafte Berichte, Ordner Größen behoben.
- Korrektur einer Regression, die Protokollierung in einen AAD eingebundene Computer mit einem lokalen Konto verhindert hat.
- Behobene Programmfehler, die die Sitzung Fensterinhalt freistellen verursacht wurden.
- Unterstützung für Remotedesktop-Endpunkt-Zertifikaten, die Elliptische Kurve asymmetrische Schlüssel enthalten.
- Korrektur eines Fehlers, das das Herunterladen von verwalteten Ressourcen in einigen Szenarien verhindert hat.
- Behandelt ein Clipping-Problem mit angehefteten Connection Center an.
- Die Kontrollkästchen behoben in den zeigt die Eigenschaftenseite, besser zusammenarbeiten und.
- Seitenverhältnis sperren ist jetzt deaktiviert, wenn dynamische Anzeige Änderung aktiviert ist.
- Behandelt die Kompatibilitätsprobleme mit F5-Infrastruktur.
- Aktualisiert die Behandlung von leeren Kennwörtern, um sicherzustellen, dass die ordnungsgemäßen Nachrichten zum Zeitpunkt der Verbindung angezeigt werden.
- Feste Maus Kompatibilitätsprobleme mit MapInfra Pro scrollen.
- Einige Ausrichtungsprobleme behoben im Connection Center, bei Ausführung auf Mojave.

## <a name="updates-for-version-1018"></a>Updates für Version 10.1.8
*Veröffentlichungsdatum: 05/04/2018*

- Unterstützung für das Ändern der remote-Auflösung durch Ändern der Größe des Sitzungsfensters!
- Feste Szenarien, in denen Remoteressource Download Feed, würde eine übermäßig lange Zeit in Anspruch nehmen.
- Die 0x207-Fehler, der auftreten können, bei der Verbindung von Servern, die nicht mit dem CredSSP Verschlüsselung Oracle Wiederherstellung-Update (CVE-2018-0886) gepatcht wurde behoben.

## <a name="updates-for-version-1017"></a>Updates für Version 10.1.7 für
*Veröffentlichungsdatum: 04/05/2018*

- Versucht, Sicherheitsfixes CredSSP Verschlüsselung Oracle Wiederherstellung Updates zu integrieren, wie in der CVE-2018-0886 beschrieben.
- Verbessertes RemoteApp-Symbol und eine Maus Cursor Rendering gemeldeten Mispaints adressiert.
- Behandelt Probleme, in denen RemoteApp Windows hinter das Connection Center vorkam.
- Korrektur ein Problems, das aufgetreten sind, wenn Sie lokale Ressourcen nach dem Importieren aus Remote Desktop 8. bearbeiten.
- Sie können jetzt eine Verbindung starten, durch Drücken der EINGABETASTE eine desktop-Kachel.
- Wenn Sie im Vollbildmodus befinden, ordnet CMD + M jetzt ordnungsgemäß Windows-Taste + M.
- Die Connection Center, Einstellungen und Informationen zu Windows reagieren Sie jetzt auf CMD + M.
- Sie können jetzt beginnen, ermitteln Feeds durch Drücken der EINGABETASTE auf der **Remoteressourcen hinzufügen** Seite.
- Ein Problem behoben wurde, in dem ein neuer Remoteressourcen Feed datensuchvorgang im Connection Center bis gezeigt, nach der Aktualisierung.
 
## <a name="updates-for-version-1016"></a>Updates für Version 10.1.6
*Veröffentlichungsdatum: 03/26/2018*

- Ein Problem behoben, in denen würde RemoteApp Windows selbst neu anordnen.
- Ein Fehler auf, der einige Windows RemoteApp hinter ihren übergeordneten Fenster hängen bleiben verursacht wurde behoben.
- Behandelt ein Offset Mauszeiger-Problem mit Auswirkung auf eine RemoteApp-Programme.
- Ein Problem behoben, in denen gegeben haben eine neue Verbindung ab den Fokus zu einer vorhandenen Sitzung, statt eine neue Sitzung-Fenster öffnen.
- Es wurde einen Fehler mit einer Fehlermeldung behoben – sehen Sie die richtige Nachricht jetzt Wenn wir Ihr Gateway nicht finden können.
- Die Quit-Verknüpfung (⌘ + Q) ist jetzt durchgängig in der Benutzeroberfläche angezeigt.
- Die Bildqualität verbessert, wenn im Modus "an Fenster anpassen" Strecken.
- Korrektur einer Regression, die mehrere Instanzen von in der Remotesitzung angezeigt wird, wird der Ordner "home" verursacht hat.
- Aktualisiert das Standardsymbol für desktop-Kacheln.
