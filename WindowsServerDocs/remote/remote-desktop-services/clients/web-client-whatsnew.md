---
title: What's new for Remote Desktop Web-Client zu finden?
description: Erfahren Sie mehr über aktuelle Änderungen an den Webclient für Remotedesktop
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
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5be9b05da1e78cc54e12254f43d0f44f7ff65c5d
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804880"
---
# <a name="whats-new-for-the-remote-desktop-web-client"></a>Neuigkeiten für den Remotedesktop-Webclient

Wir aktualisieren regelmäßig die [Remote Desktop WebClient](remote-desktop-web-client.md), neue Features hinzugefügt wurden, und Beheben von Problemen. Sehen Sie sich die neuesten Updates, die weiter unten.

> [!NOTE]
> Wir haben das System zur zeilenversionsverwaltung für den WebClient geändert. Ab Version 1.0.18.0 werden alle Releaseversionen der Web-Client (im Format "W.X.Y.Z") enthalten. Releasenummer für den Remotedesktop-Webclient endet immer mit 0 (z. B. W.X.Y.0). Jeder virtuelle Windows-Desktop Web Client-Version wird die letzte Ziffer bis zur nächsten Remote Desktop Web Client Veröffentlichung (z. B. 1.0.18.1) geändert.

## <a name="updates-for-version-10180"></a>Updates für Version 1.0.18.0
*Veröffentlichungsdatum: 5/14/2019*

- Hinzugefügte Ressource Launch Method-Konfiguration in der Registerkarte "Einstellungen", ermöglicht den Benutzern auf Ressourcen im Browser öffnen oder eine RDP-Datei mit einem anderen Client herunterladen. Diese Einstellung kann von Ihrem Administrator konfiguriert werden Details in Bezug auf die Administratorkonfigurationen für dieses Feature Sie in finden der [web-Client-Setup-Dokumentation](remote-desktop-web-client-admin.md).
- Feste Farbe, die Probleme, die Aktivierung mehr lebendige Rendern Farben in der Remotesitzung.
- Überarbeitete Fehlermeldungen im Zusammenhang mit der Remoteressource, die feed-Fehler. 
- Unterstützung für weitere Office Tastenkombinationen, z. B. spezielle einfügen (Strg + Alt + V).
- Zusätzliche Tastenkombinationen für Benutzer zum Aufrufen der Windows-Schlüssel in der Remotesitzung (Alt + F3)
- Aktualisierte Fehlermeldung für Benutzer, die für die Authentifizierung mit einem abgelaufenen Kennwort.
- Feed aktualisiert Benutzeroberfläche auf der Seite "alle Ressourcen".
- Verbinden aufgelöst überlappende Dialoge, die während der Sitzung aufgetreten sind.
- Größenanpassung der Remoteressource-Symbol behoben in der Taskleiste Ressource.

## <a name="updates-for-version-1011"></a>Updates für Version 1.0.11
*Veröffentlichungsdatum: 2/22/2019*

- Aktiviert die Verbindung mit RD-Broker ohne RD-Gateway in Windows Server-2019.
- Feeds alphabetisch sortiert (d. h. RemoteApps zuerst Desktops zweite).
- Verbessern der Kompatibilität mit Bildschirmleseprogrammen mehrere Eingabehilfen-Fehler behoben.
- Unsere Buildtools wird aktualisiert.
- Verschiedene Fehlerbehebungen.

## <a name="updates-for-version-107"></a>Updates für Version 1.0.7
*Veröffentlichungsdatum: 1/24/2019*

- Offline-Verwendung in internen Netzwerken wird jetzt unterstützt.
- Verbessertes Rendering für nicht - Microsoft Edge-Browser.
- Implementierte Limit für das Abrufen von feed "Wiederholen" versucht, die DoS zu verhindern.
- Feste Eingabehilfen-Fehler, aktivieren die Benutzer mit sehbehinderung den Webclient verwenden.
- Verbesserte Fehlermeldungen, die dem Benutzer für den feed Fehler angezeigt.
- Hinzugefügt Strg + Alt + Ende (Windows) und fn + Steuerelement + Option + löschen (Mac)-Tastenkombinationen STRG + Alt + ENTF auf remote-Computer aufrufen.
- Verbesserte Telemetrie für absturzereignissen.
- Verbesserte unsere Buildpipeline und Buildtools.
- Verschiedene Fehlerbehebungen.

## <a name="updates-for-version-101"></a>Updates für Version 1.0.1
*Veröffentlichungsdatum: 10/29/2018*

- Eine Option aus, um hinzugefügt **Capture Supportinformationen** auf der Seite "Info", um Probleme zu diagnostizieren.
- InPrivate-Modus wird jetzt unterstützt.
- Verbesserte Unterstützung für nicht-englischen Tastaturen.
- Ein Problem behoben wurde gezeigt, in denen nicht ordnungsgemäß, QuickInfos mit nicht englischen Zeichen.
- Problem behoben, Grafiken Rendering der Chrome-Benutzer betroffen.
- Zeitzone Umleitung mit vollständigen DST-Unterstützung aktualisiert.
- Verbessert die Fehlermeldung für die Out-of-Memory-Fehler.
- Verschiedene Fehlerbehebungen.

## <a name="updates-for-version-100"></a>Updates für Version 1.0.0
*Veröffentlichungsdatum: 07/16/2018*

- Remotedesktop-Client ist nun allgemein verfügbar.
- Administratoren können global für den WebClient-Telemetrie deaktivieren aktivieren.
- Verschiedene Fehlerbehebungen.

## <a name="updates-for-version-090"></a>Updates für Version 0.9.0
*Veröffentlichungsdatum: 07/05/2018*

- Neue Anmeldeoberfläche WebClient heraus.
- Nicht mehr zur Eingabe von Anmeldeinformationen aufgefordert, beim Starten von einer Desktop- oder app-Verbindungs (einmaliges Anmelden).
- Den WebClient verschoben in eine neue URL: <https://server_FQDN/RDWeb/webclient/index.html>
- Hinzugefügte Zeitzone Umleitung.
- Verschiedene Fehlerbehebungen.

## <a name="updates-for-version-081"></a>Updates für Version 0.8.1
*Veröffentlichungsdatum: 05/17/2018*

- Aktualisiert, um CredSSP Verschlüsselung Oracle Wiederherstellung in CVE-2018-0886 beschrieben.
- Verbindungsfehler für einige Sprachen behoben, wenn das Drucken aktiviert ist.
- Verbesserte Fehlermeldungen, wenn ein Gateway nicht als Teil der Bereitstellung ist.
- **Hilfe** und **Feedback** Optionen hinzugefügt wurden.

## <a name="updates-for-version-080"></a>Updates für Version 0.8.0
*Veröffentlichungsdatum: 03/28/2018*

- Erste öffentliche Vorschauversion des Webclients.
- Kopieren und Einfügen von Text über die Zwischenablage mit **STRG + C** und **STRG + V**.
- Druckt in eine PDF-Datei.
- In 18 Sprachen lokalisiert.
 
