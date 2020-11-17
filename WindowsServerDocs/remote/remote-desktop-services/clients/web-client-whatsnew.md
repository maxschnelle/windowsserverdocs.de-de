---
title: Neues beim Webclient
description: Hier erfährst du mehr über aktuelle Änderungen für den Remotedesktop-Webclient.
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 09/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8519d69c39cb86f10c66b3c28410a285ca06252d
ms.sourcegitcommit: 14c9526b1c74821341d4b66de92adce9bee92f10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/12/2020
ms.locfileid: "94558277"
---
# <a name="whats-new-in-the-web-client"></a>Neues beim Webclient

Der [Remotedesktop-Webclient](remote-desktop-web-client.md) wird regelmäßig mit neuen Features und Problembehebungen aktualisiert. Hier findest du die neuesten Updates.

> [!NOTE]
> Wir haben das Versionsverwaltungssystem für den Webclient geändert. Ab Version 1.0.18.0 enthalten alle Releaseversionen des Webclients Zahlen (im Format „W.X.Y.Z“). Releasenummern für den Remotedesktop-Webclient enden immer mit einer Null (Beispiel: W.X.Y.0). Mit jedem Windows Virtual Desktop-Webclientrelease ändert sich die letzte Stelle bis zum nächsten Remotedesktop-Webclientrelease (Beispiel: 1.0.18.1).

## <a name="updates-for-10220"></a>Updates für 1.0.22.0
*Veröffentlicht am: 2.9.2020*

> [!IMPORTANT]
> In Version 1.0.22.0 wurde eine Regression eingeführt, die sich auf einige Chromebook-Betriebssysteme auswirkt. Benutzer auf betroffenen Betriebssystemen können keine Verbindung zu einer Remotesitzung über den Webclient herstellen. Wir untersuchen dieses Problem derzeit und werden eine neue Version des Webclients veröffentlichen, sobald wir diese Regression behoben haben. In der Zwischenzeit können Sie das Problem vermeiden, indem Sie die Version 1.0.21.0 wiederherstellen. 

- Benutzer können nun das minimierte Menü verschieben.
- Die Unterstützung für 4K- und Ultra-Wide-Monitore wurde verbessert, und ein Problem wurde behoben, bei dem das Kopieren großer Datenmengen zum Absturz von Sitzungen führte.
- Die Unterstützung für die Verwendung eines Eingabemethoden-Editors in der Remotesitzung wurde verbessert. Weitere Informationen zur Verwendung eines Eingabemethoden-Editors mit dem Webclient finden Sie unter [Herstellen der Verbindung zu Windows Virtual Desktop mit dem Webclient](/azure/virtual-desktop/connect-web.md).
- Die UI der Seite **Alle Ressourcen** wurde geändert.
- Mehrere Fehler in der Verbindungssequenz wurden behoben, bei denen der Webclient einen *allgemeinen Protokollfehler* zurückgab.
- Es wurden Probleme bei der Tastatureingabe behoben, bei denen bestimmte Tastenfolgen nicht richtig verarbeitet wurden.
- Barrierefreiheitsverbesserungen

## <a name="updates-for-version-10210"></a>Updates für Version 1.0.21.0
*Veröffentlicht am: 15.11.2019*

- Unterstützung für die Verwendung eines Eingabemethoden-Editors (IME) in der Remotesitzung zum Hinzufügen komplexer Zeichen.
- Eine Regression wurde behoben, durch die Benutzer von macOS-Geräten keine Kopier- und Einfügevorgänge in der Remotesitzung durchführen konnten.
- Eine Regression wurde behoben, durch die ein lokaler Tastendruck der Windows-Taste in Firefox an die Remotesitzung gesendet wurde.
- Ein Link zum Ändern des RDWeb-Kennworts wurde hinzugefügt, der von Ihrem Administrator aktiviert werden kann.

## <a name="updates-for-version-10200"></a>Updates für Version 1.0.20.0
*Veröffentlicht am: 18.10.2019*

- Unterstützung für Verbindungen mit Windows 7- und Windows Server 2008 R2-Hosts hinzugefügt.
- Es wurde ein Problem behoben, bei dem bestimmte App-Symbole als transparente Kacheln angezeigt wurden.
- Verbindungsprobleme beim Internet Explorer-Browser unter Windows 7 behoben.
- Unerwartete Verbindungstrennungen wurden korrigiert, die bei Änderung der Größe des Browsers aufgetreten sind.
- Barrierefreiheitsverbesserungen
- Bibliotheken von Drittanbietern wurden aktualisiert.

## <a name="updates-for-version-10180"></a>Updates für Version 1.0.18.0
*Veröffentlicht am: 14.5.2019*

- Konfiguration für die Ressourcenstartmethode auf der Registerkarte „Einstellungen“ hinzugefügt, sodass Benutzer wählen können, ob Ressourcen im Browser geöffnet werden sollen oder ob eine RDP-Datei für einen anderen Client heruntergeladen werden soll. Diese Einstellung kann von deinem Administrator konfiguriert werden. Details zu Administratorkonfigurationen für dieses Feature findest du in der [Setupdokumentation für den Webclient](remote-desktop-web-client-admin.md).
- Probleme beim Rendern von Farben behoben, um kräftigere Farben in deiner Remotesitzung zu ermöglichen.
- Fehlermeldungen im Zusammenhang mit Feedfehlern für Remoteressourcen überarbeitet.
- Unterstützung für weitere Office-Tastenkombinationen hinzugefügt – beispielsweise „Inhalte einfügen“ (STRG+ALT+V).
- Tastenkombination hinzugefügt, mit der Benutzer die Windows-Taste in der Remotesitzung verwenden können (ALT+F3).
- Fehlermeldung für Benutzer aktualisiert, die versuchen, sich mit einem abgelaufenen Kennwort zu authentifizieren.
- Feedbenutzeroberfläche auf der Seite „Alle Ressourcen“ aktualisiert.
- Problem mit überlappenden Dialogen beim Wiederherstellen der Sitzungsverbindung behoben.
- Größenanpassung des Remoteressourcensymbols auf der Ressourcentaskleiste korrigiert.

## <a name="updates-for-version-1011"></a>Updates für Version 1.0.11
*Veröffentlicht am: 22.2.2019*

- Verbindung mit RD-Broker ohne RD-Gateway in Windows Server 2019 ermöglicht.
- Feeds alphabetisch sortiert (zuerst RemoteApps, dann Desktops).
- Mehrere Barrierefreiheitsfehler behoben, um die Bildschirmsprachausgabe zu verbessern.
- Buildtools aktualisiert.
- Verschiedene Fehler behoben.

## <a name="updates-for-version-107"></a>Updates für Version 1.0.7
*Veröffentlicht am: 24.1.2019*

- Offlineverwendung in internen Netzwerken wird jetzt unterstützt.
- Rendering in Microsoft Edge-fremden Browsern verbessert.
- Limit für erneute Feedabrufversuche implementiert, um DoS-Angriffen vorzubeugen.
- Barrierefreiheitsfehler behoben, um Benutzern mit Sehbehinderung die Verwendung des Webclients zu ermöglichen.
- Fehlermeldungen verbessert, die dem Benutzer bei Feedfehlern angezeigt werden.
- Tastenkombinationen STRG+ALT+ENDE (Windows) und FN+CTRL+OPTION+ENTF (Mac) hinzugefügt, um STRG+ALT+ENTF auf dem Remotecomputer verwenden zu können.
- Telemetriedaten für Absturzereignisse verbessert.
- Buildpipeline und Buildtools verbessert.
- Verschiedene Fehler behoben.

## <a name="updates-for-version-101"></a>Updates für Version 1.0.1
*Veröffentlicht am: 29.10.2018*

- Option zum **Erfassen von Supportinformationen** auf der Infoseite hinzugefügt, um Probleme zu diagnostizieren.
- InPrivate-Modus wird jetzt unterstützt.
- Unterstützung nicht-englischer Tastaturen verbessert.
- Problem behoben, das dazu führte, dass QuickInfos mit nicht englischen Zeichen falsch angezeigt wurden.
- Problem beim Grafikrendering für Chrome-Benutzer behoben.
- Zeitzonenumleitung mit vollständiger DST-Unterstützung aktualisiert.
- Fehlermeldung für unzureichenden Arbeitsspeicher verbessert.
- Verschiedene Fehler behoben.

## <a name="updates-for-version-100"></a>Updates für Version 1.0.0
*Veröffentlicht am: 16.7.2018*

- Der Remotedesktop-Webclient ist nun allgemein verfügbar.
- Administratoren können Telemetriedaten global für den Webclient deaktivieren.
- Verschiedene Fehler behoben.

## <a name="updates-for-version-090"></a>Updates für Version 0.9.0
*Veröffentlicht am: 5.7.2018*

- Neue Anmeldeoberfläche innerhalb des Webclients
- Keine Aufforderung zur Eingabe von Anmeldeinformationen beim Starten einer Desktop- oder App-Verbindung mehr (einmaliges Anmelden)
- Webclient zu einer neuen URL verschoben: <https://server_FQDN/RDWeb/webclient/index.html>
- Zeitzonenumleitung hinzugefügt.
- Verschiedene Fehler behoben.

## <a name="updates-for-version-081"></a>Updates für Version 0.8.1
*Veröffentlicht am: 17.5.2018*

- Aktualisierungen für die in CVE-2018-0886 beschriebene CredSSP-Encryption Oracle-Abwehr
- Verbindungsfehler bei Druckaktivierung für einige Sprachen behoben.
- Fehlermeldung verbessert, die angezeigt wird, wenn die Bereitstellung kein Gateway enthält.
- Optionen **Hilfe** und **Feedback** hinzugefügt.

## <a name="updates-for-version-080"></a>Updates für Version 0.8.0
*Veröffentlicht am: 28.03.2018*

- Erstes Public Preview-Release des Webclients
- Kopieren und Einfügen von Text über die Zwischenablage mit **STRG+C** und **STRG+V**
- Drucken in eine PDF-Datei
- Lokalisierung in 18 Sprachen
