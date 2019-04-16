---
title: Remotedesktop - vergleichen Sie die Client-apps
description: Erfahren Sie, wie die verschiedenen RD-apps vergleichen, Optik auf unterstützten Features und Funktionen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc20d1a2c51abddb8ae014efc621f4f0b36c3677
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297409"
---
# Vergleichen Sie die Client-apps

>Gilt für: Windows 10, Windows 8.1, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2

Wir werden häufig gefragt, wie die verschiedenen Remotedesktop-Client-apps miteinander vergleichen. Tun sie alle das gleiche? Hier sind die Antworten auf diese Fragen.

## Umleitung-Unterstützung

In den folgenden Tabellen vergleichen Sie Unterstützung für die Geräte- und andere Umleitung auf Remotedesktopverbindung-app, uwp, Android-app, iOS-app, MacOS-app und Web-Client. Diese Tabellen behandelt die Umleitung, die Sie einmal in einer Remotesitzung zugreifen können. 

Wenn Sie in Ihren persönlichen Desktop remote, stehen zusätzliche Umleitung, die Sie in den **Zusätzlichen Einstellungen** für die Sitzung konfigurieren können. Wenn Ihre Remotedesktop oder apps von Ihrer Organisation verwaltet werden, kann der Administrator aktivieren oder deaktivieren Umleitung über Gruppenrichtlinien-Einstellungen.

### Eingabe-Umleitung

| Umleitung | Remotedesktop<br> Verbindung | Universelle | Android | iOS | MacOS | WebClient |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| Tastatur    | X                             | X         | X       | X   | X     | X          |
| Maus       | X                             | X         | X       | X *    | X     | X          |
| Toucheingabe       | X                             | X         | X       | X   |       |            |
| Other       | Stift                           |           |         |     |       |            |
* Zeigen Sie die [Liste der unterstützten Eingabegeräte für den Remotedesktop iOS Beta-Client](remote-desktop-ios.md#supported-input-devices).

### Port-Umleitung   

| Umleitung | Remotedesktop <br>Verbindung | Universelle | Android | iOS | MacOS | WebClient |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| Seriellen port | X                             |           |         |     |       |            |
| USB         | X                             |           |         |     |       |            |

Wenn Sie den USB-Port-Umleitung aktivieren, werden alle USB-Geräte an den USB-Anschluss automatisch in der Remotesitzung erkannt.

### Andere Umleitung (Geräte usw.)



| Umleitung         | Remotedesktopverbindung | Universelle   | Android | iOS         | MacOS                                    | WebClient    |
|---------------------|---------------------------|-------------|---------|-------------|------------------------------------------|---------------|
| Kameras             | X                         |             |         |             |                                          |               |
| Zwischenablage           | X                         | Text, Bild | Text    | Text, Bild | X                                        | Text          |
| Lokale Drive-Speicher | X                         |             | X       |             | x                                        |               |
| Standort            | X                         |             |         |             |                                          |               |
| Mikrofone         | X                         |X            |         |             | X                                        |               |
| Drucker            | X                         |             |         |             | X (nur TASSEN)                            | PDF drucken     |
| Scanner            | X                         |             |         |             |                                          |               |
| Smartcards         | X                         |             |         |             | X (Windows-Authentifizierung nicht unterstützt) |               |
| Lautsprecher            | X                         | X           | X       | X           | X                                        | X (außer Internet Explorer) |

* Drucker Umleitung - unterstützt die MacOS-app den Druckertreiber Publisher Belichter standardmäßig. Sie unterstützen keine systemeigenen Druckertreiber umleiten.

### Unterstützte RDP-Einstellungen
Diese Tabelle enthält die Liste der unterstützten RDP-Datei-Einstellungen, die mit der Windows- und HTML-Clients verwendet werden kann. Ein "X" in der Spalte "Plattform" gibt an, dass die Einstellung unterstützt wird. Bitte beachten Sie, dass es sich nicht um eine vollständige Liste der unterstützten Einstellungen für die Windows- und HTML5-Clients handelt. Wir werden weiterhin diese Tabelle, um mehr unterstützten RDP-Einstellungen für die Windows- und HTML5-Clients als auch die MacOS, iOS und Android-Clients enthalten zu aktualisieren.

| RDP-Einstellung                        | Beschreibung            | Werte                 | Standardwert          | Virtuelle Windows-Desktop | Windows | HTML5   |
|------------------------------------|------------------------|------------------------|:----------------------:|:-----------------------:|:-------:|:-------:|
| Alternative vollständige Adresse: s:value | Gibt ein alternativer Name oder IP-Adresse des Remotecomputers. | Alle gültigen Namen oder IP-Adresse des Remotecomputers, z. B. "10.10.15.15" | | x | x | x |
| Alternative Shell: s:value        | Bestimmt, ob ein Programm wird beim Herstellen einer mit RDP Verbindung automatisch gestartet. Diese Einstellung entspricht Pfad und Name das Programm auf der Registerkarte "Programme" des Remotedesktopverbindung-Clients. Um eine alternative Shell anzugeben, geben Sie einen gültigen Pfad zu einer ausführbaren Datei für den Wert, z. B. "" C:\ProgramFiles\Office\word.exe"". Diese Einstellung legt außerdem den Pfad oder den Alias der Remote-Anwendung zum Zeitpunkt der Verbindung gestartet werden, wenn RemoteApplicationMode aktiviert ist. | z. B. "C:\ProgramFiles\Office\word.exe" || x | x | x |
| audiocapturemode:i:value | Gibt an, ob audio Input/Output-Umleitung aktiviert ist. Diese Einstellung entspricht das Remote-Audio von Remotedesktop-Verbindungsclient. | (0) deaktivieren Audioaufnahme aus dem lokalen Gerät; (1) aktivieren Sie die Audioaufnahme aus dem lokalen Gerät und eine Umleitung auf eine Audio-Anwendung in der Remotesitzung | 0 | x | x | |
| audiomode:i:value | Bestimmt, welche Computer (d. h., lokal oder Remote) audio wiedergegeben wird. | (0) Wiedergeben von Sounds auf lokalen Computer (auf diesem Computer wiedergeben); (1) Spielsounds auf remote-Computer (auf dem Remotecomputer wiedergeben); (2) wiedergeben Sie Sounds nicht (nicht wiedergegeben) | 0 | x | x | x |
| Authentifizierung Ebene: i:value | Definiert die Server Authentication Level-Einstellungen. | (0) Wenn Serverauthentifizierung fehlschlägt, mit dem Computer ohne Warnung verbinden (Connect und nicht warnen); (1) Wenn Serverauthentifizierung fehlschlägt, keine Verbindung herstellen (keine Verbindung); (2) Wenn Serverauthentifizierung ein Fehler auftritt, zeigt eine Warnung und eine Verbindung herstellen, ob die Verbindung (warnen); oder zulassen (3) keine Authentifizierungsanforderung wird angegeben. | 3 | x | x ||
| Autoreconnection aktiviert: I:value | Diese Einstellung bestimmt, ob der Clientcomputer automatisch versuchen werden, mit dem Remotecomputer zu verbinden, wenn die Verbindung unterbrochen wird. beispielsweise, wenn eine Unterbrechung der Netzwerkkonnektivität besteht. Diese Einstellung entspricht der Wiederherstellung der Verbindung ist die Verbindung abgelegte Kontrollkästchen auf der Registerkarte "Erweitert" unter Optionen in Desktop (Remote Desktop Connection, RDC).| (0) Clientcomputer versucht Verbinden nicht automatisch; (1) Clientcomputer versucht automatisch erneut eine Verbindung herstellen| 1 | x | x | x |
| bandwidthautodetect:i:value | Bestimmt, ob automatische Netzwerk erkennen aktiviert ist. | (0) deaktivieren Automatisches Netzwerk erkennen; (1) aktivieren Sie Automatisches Netzwerk erkennen | 1 | x | x | x |
| Komprimierung: i:value | Diese Einstellung bestimmt, ob Bulk-Komprimierung aktiviert ist, wenn sie auf den lokalen Computer von RDP übertragen wird.|(0) deaktivieren RDP Bulk-Komprimierung; (1) RDP Bulk Komprimierung aktivieren | 1 | x | x | x |
| Größe des Remotedesktop-Id: i:value | Gibt die Dimensionen des Desktops Remotesitzung aus einer Reihe von vordefinierten Optionen an. Diese Einstellung wird überschrieben, wenn Desktopheight oder Desktopwidth angegeben werden.| (0) 640 x 480; (1) 800 x 600; (2) 1024 x 768; (3) 1280 x 1024; (4) 1600 x 1200 | 0 | x | x | x |
| desktopheight:i:value | Diese Einstellung bestimmt die Höhe der Auflösung (in Pixel) auf dem Remotecomputer, wenn Sie eine Verbindung mit (Remote Desktop Connection, RDC). Diese Einstellung entspricht der Auswahl in TheDisplay Configurationslider auf TheDisplaytab UnderOptions in RDC. | Numerischen Wert zwischen 200 und 2048 | Der Standardwert ist auf die Auflösung auf dem lokalen Computer festgelegt. | x | x | x |
| desktopwidth:i:value | Diese Einstellung bestimmt die Auflösung Breite (in Pixel) auf dem Remotecomputer, wenn Sie eine Verbindung mit (Remote Desktop Connection, RDC). Diese Einstellung entspricht der Auswahl in TheDisplay Configurationslider auf TheDisplaytab UnderOptions in RDC. | Numerischen Wert zwischen 200 und 4096 | Der Standardwert ist auf die Auflösung auf dem lokalen Computer festgelegt. | x | x | x |
| disableclipboardredirection:i:value | Diese Einstellung bestimmt, ob die Umleitung der Zwischenablage bei der Verbindung mit dem Remotecomputer aktiviert ist. | Umleitung der Zwischenablage (0) ist aktiviert. (1) Umleitung der Zwischenablage ist nicht aktiviert. | x | x | x |
| disableconnectionsharing:i:value | Bestimmt, ob der Remotedesktop-Client erneut eine Verbindung her, um alle vorhandenen Verbindungen mit öffnen oder eine neue Verbindung zu initiieren, wenn ein RemoteApp oder Desktop gestartet wird | Wiederherstellung der Verbindung an alle vorhandenen Sitzung (0); (1) initiieren Sie neue Verbindung | 0 | x | x | x |
| disableprinterredirection:i:value | Diese Einstellung bestimmt, ob einfach drucken Drucker Umleitung bei der Verbindung mit dem Remotecomputer aktiviert ist. | (0) einfach drucken Drucker Umleitung ist aktiviert. (1) einfache drucken Drucker Umleitung ist deaktiviert. | x | x | x |
| Domäne: s:value | Diese Einstellung gibt den Namen der Domäne, in der sich das Benutzerkonto, das verwendet wird, um mit dem Remotecomputer mit (Remote Desktop Connection, RDC) anmelden befindet. Der Wert dieser Einstellung zusammen mit den Wert der Einstellung für den Benutzernamen wird im c Berichtname auf TheGeneraltab UnderOptionsin RDC angezeigt. | Ein gültiger Domänenname, z. B. "CONTOSO" | Kein Standardwert | x | x | x |
| drivestoredirect:s:value | Bestimmt, welche lokaler Laufwerke auf dem Clientcomputer umgeleitete und in der Remotesitzung verfügbar sein. | Kein Wert angegeben - leiten keine Laufwerke; * - Umleiten alle Laufwerke, einschließlich der Laufwerke, die später; verbunden sind DynamicDrives - umleiten Laufwerke, die später verbunden sind; Das Laufwerk, und Beschriftungen für ein oder mehrere Laufwerke - Umleiten der angegebenen Laufwerke.| Kein Wert angegeben - leiten keine Laufwerke | x | x    | |
| enablecredsspsupport:i:value | Diese Einstellung bestimmt, ob RDP Credential Security Support Provider (CredSSP) verwendet für die Authentifizierung, wenn es verfügbar ist. | (0) RDP verwenden nicht CredSSP, auch wenn das Betriebssystem CredSSP unterstützt. (1) RDP wird CredSSP verwenden, wenn das Betriebssystem CredSSP unterstützen | 1 | x | x | |
| vollständige Adresse: s:value | Diese Einstellung gibt an, den Namen oder die IP-Adresse des Remotecomputers, die Sie für eine Verbindung herstellen möchten | Ein gültiger Computername, IPv4-Adresse oder IPv6-Adresse - gibt dem Remotecomputer mit dem Sie eine Verbindung herstellen möchten. | | x | x | x |
| GatewayCredentialsSource:i:value | Gibt an, oder ruft die RD-Gateway-Authentifizierungsmethode. | Kennwort (NTLM); (0) anfordern (1) Smartcard verwenden; (4) zulassen, dass Benutzer später auswählen | 0 | x | x | x |
| gatewayhostname:s:value | Gibt den RD-Gateway-Hostnamen. | Gültige Gateway-Server-Adresse. ||x|x|x|
| gatewayprofileusagemethod:i:value | Gibt an, ob RD-Gateway-Standardeinstellungen | Die Verwendung Profil Standardmodus gemäß der Angabe durch den Administrator (0); (1) verwenden Sie explizite Einstellungen wie vom Benutzer angegeben. | 0 | x | x | x |
| gatewayusagemethod:i:value | Gibt an, wann der RD-Gateway-Server verwenden | (0) verwenden Sie keinen RD-Gateway-Server; (1) verwenden Sie immer einen RD-Gateway-Server; (2) verwenden Sie einen RD-Gateway-Server aus, wenn eine direkte Verbindung mit der RD-Sitzungshostserver hergestellt werden kann. (3) verwenden Sie die Standardeinstellungen für RD-Gateway-Server. (4) nicht RD-Gateway verwenden, Server für lokale Adressen umgehen; Festlegen dieser Eigenschaftswert auf 0 oder 4 sind effektiv äquivalent, aber diese Einstellung auf 4 aktiviert die Option für lokale Adressen umgehen. | | x | x | x |
| networkautodetect:i:value | Bestimmt, ob automatische Bandbreite-Netzwerke oder nicht verwenden. Erfordert die Optionbandwidthautodetectto festgelegt werden, und korreliert Withconnection Typ7. | (0) verwenden Sie keine automatische Bandbreite Netzwerke; (1) verwenden Sie die automatische Bandbreite-Netzwerke | 1 | x ||x|
| PromptCredentialOnce:i:value | Bestimmt, ob die Anmeldedaten eines Benutzers gespeichert und für die RD-Gateway und dem Remotecomputer verwendet werden.|(0) Remotesitzung wird nicht die gleichen Anmeldeinformationen verwenden; (1) Remotesitzung wird die gleichen Anmeldeinformationen verwenden.|1|x|x||
| redirectclipboard:i:value | Diese Einstellung bestimmt, ob die Zwischenablage auf dem lokalen Computer umgeleitete und in der Remotesitzung verfügbar sein. Diese Einstellung entspricht TheClipboardcheck Feld auf hinzu Resourcestab UnderOptionsin RDC. | (0) Zwischenablage auf lokalen Computer ist nicht verfügbar in der Remotesitzung. (1) Zwischenablage auf dem lokalen Computer ist verfügbar in Remotesitzung|1|x|x|x|
| redirectdrives:i:value | Diese Einstellung bestimmt, ob die Laufwerke auf dem Clientcomputer umgeleitete und in der Remotesitzung verfügbar sein. Diese Einstellung entspricht der Auswahl ForDrivesunderMoreon hinzu Resourcestab UnderOptionsin RDC.|(0) die Laufwerke auf dem lokalen Computer sind nicht verfügbar in der Remotesitzung; (1) die Laufwerke auf dem lokalen Computer stehen in der Remotesitzung|0|x|x| |
| redirectprinters:i:value | Diese Einstellung bestimmt, ob Drucker, die auf dem Clientcomputer konfiguriert werden, umgeleitete und in der Remotesitzung bei einem Remotecomputer herstellen einer Verbindung mit (Remote Desktop Connection, RDC) verfügbar. Diese Einstellung entspricht der Auswahl im ThePrinterscheck auf hinzu Resourcestab UnderOptionsin RDC. | (0) die Drucker auf dem lokalen Computer sind nicht verfügbar in der Remotesitzung; (1) die Drucker auf dem lokalen Computer stehen in der Remotesitzung|1|x|x|x|
| redirectsmartcards:i:value | Diese Einstellung bestimmt, ob Smartcard-Geräte auf dem Clientcomputer umgeleitete und in der Remotesitzung bei einem Remotecomputer herstellen einer Verbindung mit (Remote Desktop Connection, RDC) verfügbar ist. Diese Einstellung entspricht der Auswahl in TheSmart Cardscheck UnderMore auf hinzu Resourcestab UnderOptionsin RDC Feld.|(0) der Smartcard-Gerät, auf dem lokalen Computer ist nicht verfügbar in der Remotesitzung; (1) das Smartcard-Gerät, auf dem lokalen Computer ist verfügbar in der Remotesitzung|1|x|x||
| remoteapplicationcmdline:s:value | Optionale Befehlszeilenparameter für das RemoteApp.||x|x|x|
| remoteapplicationexpandcmdline:i:value| Bestimmt, ob in der RemoteApp-Befehlszeilenparameter enthaltenen Umgebungsvariablen lokal oder Remote erweitert werden sollen.|Umgebungsvariablen (0) sollten auf die Werte des lokalen Computers erweitert werden. (1) Umgebungsvariablen soll auf dem Remotecomputer auf die Werte des Remotecomputers erweitert werden||x|x|x|
| remoteapplicationexpandworkingdir | Bestimmt, ob die Umgebungsvariablen enthalten in der RemoteApp Arbeitsverzeichnisparameter lokal oder Remote erweitert werden sollen. | Umgebungsvariablen (0) sollten auf die Werte des lokalen Computers erweitert werden. (1) Umgebungsvariablen sollte auf dem Remotecomputer auf die Werte des Remotecomputers erweitert werden. Hinweis: Das Arbeitsverzeichnis RemoteApp wird über die Shell arbeiten Directory-Parameter angegeben.||x|x|x|
|remoteapplicationfile:s:value | Gibt eine Datei auf dem Remotecomputer mithilfe der RemoteApp geöffnet werden. Hinweis: Für lokale Dateien geöffnet werden soll, müssen Sie auch Laufwerk Umleitung für das Quelllaufwerk aktivieren.||x|x|x|
|remoteapplicationicon:s:value | Gibt die Symboldatei in die Client-Benutzeroberfläche angezeigt werden, während ein RemoteApp starten. Wenn kein Dateiname angegeben ist, wird der Client das standardmäßige Remotedesktop-Symbol verwenden. Nur "ICO" Dateien werden unterstützt.||x|x|x|
|remoteapplicationmode:i:value | Bestimmt, ob eine RemoteApp-Verbindung als RemoteApp Sitzung gestartet wird.| (0) nicht starten eine RemoteApp-Sitzung. (1) eine RemoteApp-Sitzung starten|1|x|x|x|
|remoteapplicationname:s:value | Gibt den Namen des der RemoteApp in der Client-Benutzeroberfläche beim Starten der RemoteApp.| z. B. "Excel 2016"|x|x|x|
|remoteapplicationprogram:s:value | Gibt den Alias oder ausführbare Datei Namen von der RemoteApp. | z. B. "EXCEL" |x|x|x|
|Bildschirm Modus-Id: i:value | Diese Einstellung bestimmt, ob der Remotesitzung Fenster im Vollbildmodus angezeigt wird, wenn Sie mit dem Remotecomputer eine Verbindung mit (Remote Desktop Connection, RDC). Diese Einstellung entspricht der Auswahl in TheDisplay Configurationslider auf TheDisplaytab UnderOptionsin RDC.|(1) die Remotesitzung wird in einem Fenster angezeigt. (2) die Remotesitzung wird im Vollbildmodus angezeigt.|2|x|x|x|
|Smart-Größe: i:value | Diese Einstellung legt fest, ob der Clientcomputer den Inhalt auf dem Remotecomputer an die Fenstergröße des Clientcomputers skalieren kann.|(0) die Anzeige im Client wird nicht skaliert werden, wenn angepasst. (1) die Anzeige im Client wird skaliert werden, beim Ändern der Größe|0|x|x||
| Verwenden Sie multimon:i:value | Diese Einstellung konfiguriert die Unterstützung für mehrere Monitore, wenn Sie mit dem Remotecomputer eine Verbindung mit (Remote Desktop Connection, RDC).|(0) Unterstützung für mehrere Monitore; nicht aktivieren (1) Aktivieren der Unterstützung für mehrere Monitore|0|x|x||
| UserName:s:value | Diese Einstellung gibt den Namen des Benutzerkontos, das verwendet wird, um mit dem Remotecomputer mit (Remote Desktop Connection, RDC) anmelden. Der Wert dieser Einstellung zusammen mit den Wert der Einstellung für die Domäne wird in c-Feld auf TheGeneraltab UnderOptionsin RDC angezeigt.| Alle gültigen Benutzernamen. ||x|x|x|
| videoplaybackmode:i:value| Diese Einstellung legt fest, ob (Remote Desktop Connection, RDC) verwendet RDP effizient multimedia streaming für die Videowiedergabe.|(0) verwenden Sie nicht RDP effizient multimedia streaming für die Videowiedergabe; (1) verwenden Sie RDP effizient multimedia streaming für die Videowiedergabe, wenn möglich|1|x|x||
| workspaceid:s:value | Mit dieser Einstellung wird der RemoteApp und Desktop-ID zugeordnet ist die RDP-Datei, die diese Einstellung enthält. | Einen gültigen RemoteApp und Desktop Verbindungs-ID|x|x||