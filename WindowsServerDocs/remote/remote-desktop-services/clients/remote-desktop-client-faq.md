---
title: 'Remotedesktopclients: Häufig gestellte Fragen'
description: Häufig gestellte Fragen zu Remotedesktopclients
ms.topic: article
ms.assetid: 785a18cf-a5d0-4bc2-95e4-9ef53ee8f65a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 07/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 420cedebcfc71a5ba78908d244d1f8ca651bee4c
ms.sourcegitcommit: 0b3d6661c44aa1a697087e644437279142726d84
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083671"
---
# <a name="frequently-asked-questions-about-the-remote-desktop-clients"></a>Häufig gestellte Fragen zu Remotedesktopclients

>Gilt für: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Es kann sein, dass Fragen auftauchen, nachdem du den Remotedesktopclient auf deinem Gerät (Android, Mac, iOS oder Windows) eingerichtet hast. Hier erhältst du Antworten auf die am häufigsten gestellten Fragen zu Remotedesktopclients.

- [Einrichten](#setting-up)
- [Verbindungen, Gateway und Netzwerke](#connection-gateway-and-networks)
- [Webclient](#web-client)
- [Monitore, Audio und Maus](#monitors-audio-and-mouse)
- [Macintosh-Hardware](#mac-client---hardware-questions)
- [Spezifische Fehlermeldungen](#specific-errors)

Die meisten dieser Fragen gelten für alle Clients, aber es sind auch einige clientspezifische Punkte enthalten.

Falls du weitere Fragen hast, für die du Antworten von uns benötigst, kannst du diese als Feedback zu diesem Artikel hinterlassen.

## <a name="setting-up"></a>Einrichten

### <a name="which-pcs-can-i-connect-to"></a>Mit welchen PCs kann ich eine Verbindung herstellen?

Informationen dazu, mit welchen PCs du eine Verbindung herstellen kannst, findest du im Artikel zur [unterstützten Konfiguration](remote-desktop-supported-config.md).

### <a name="how-do-i-set-up-a-pc-for-remote-desktop"></a>Wie richte ich einen PC für Remotedesktop ein?

Ich habe mein Gerät eingerichtet, aber ich glaube, der PC ist noch nicht bereit. Hilfe?

Kennst du den Setup-Assistenten für Remotedesktop? Darin wird Schritt für Schritt beschrieben, wie du deinen PC für den Remotezugriff einrichtest. Lade dieses Tool herunter, und führe es auf deinem PC aus, um alles einzurichten.

Lies weiter, falls du manuell vorgehen möchtest.

Führe für Windows 10 folgende Schritte aus:

1. Öffne auf dem Gerät, mit dem du eine Verbindung herstellen möchtest, die **Einstellungen**.
2. Wähle **System** und dann **Remotedesktop**.
3. Verwende den Schieberegler, um Remotedesktop zu aktivieren.
4. Im Allgemeinen ist es am besten, den PC eingeschaltet zu lassen und sichtbar zu machen, um die Verbindungsherstellung zu vereinfachen. Klicke auf **Einstellungen anzeigen**, um zu den Energieeinstellungen für deinen PC zu navigieren und diese Einstellung zu ändern.
   > [!NOTE]
   > Du kannst keine Verbindung mit einem PC herstellen, der sich im Standbymodus oder Ruhezustand befindet. Stelle daher sicher, dass die Einstellung für den Standbymodus und Ruhezustand auf dem Remote-PC jeweils auf **Nie** festgelegt ist. (Der Ruhezustand ist nicht auf allen PCs verfügbar.)


Notiere dir den Namen dieses Computers unter **Herstellen einer Verbindung mit diesem PC**. Du benötigst diese Angabe zum Konfigurieren der Clients.

Du kannst für bestimmte Benutzer Zugriff auf diesen PC gewähren. Klicke hierzu auf **Select users that can remotely access this PC** (Benutzer auswählen, die remote auf diesen PC zugreifen können).
Mitglieder der Gruppe „Administratoren“ verfügen automatisch über Zugriff.

Befolge für Windows 8.1 die Anleitung zum Zulassen von Remoteverbindungen unter [Eine Verbindung mit einem anderen Computer mithilfe der Remotedesktopverbindung herstellen](https://support.microsoft.com/help/17463/windows-7-connect-to-another-computer-remote-desktop-connection#1TC=windows-8).



## <a name="connection-gateway-and-networks"></a>Verbindungen, Gateway und Netzwerke

### <a name="why-cant-i-connect-using-remote-desktop"></a>Warum kann ich keine Verbindung per Remotedesktop herstellen?

Hier sind einige mögliche Lösungen für häufige Probleme angegeben, die ggf. auftreten, wenn du versuchst, eine Verbindung mit einem Remote-PC herzustellen. Wenn diese Lösungen nicht funktionieren, helfen die Informationen auf der [Website der Microsoft-Community](https://go.microsoft.com/fwlink/p/?LinkId=242079) weiter.

- **Der Remote-PC kann nicht gefunden werden.** Stelle sicher, dass du über den richtigen PC-Namen verfügst. Prüfe anschließend, ob du den Namen richtig eingegeben hast. Versuche, anstelle des PC-Namens die IP-Adresse des Remote-PC zu verwenden, falls die Verbindungsherstellung immer noch nicht möglich ist.
- **Es liegt ein Netzwerkproblem vor.** Stelle sicher, dass du über eine Internetverbindung verfügst.
- **Unter Umständen wird der Remotedesktopport von der Firewall blockiert.** Führe diese Schritte aus, wenn du die Windows-Firewall verwendest:

  1. Öffnen Sie Windows-Firewall.
  2. Klicke auf **Eine App oder ein Feature durch die Windows-Firewall zulassen** .
  3. Klicke auf **Einstellungen ändern**. Unter Umständen wirst du aufgefordert, ein Administratorkennwort einzugeben oder deine Auswahl zu bestätigen.
  4. Wähle unter **Zugelassene Apps und Features** die Option **Remotedesktop**, und tippe oder klicke dann auf **OK**.

     Stelle bei Verwendung einer anderen Firewall sicher, dass der Port für Remotedesktop geöffnet ist (normalerweise 3389).
- **Unter Umständen können auf dem Remote-PC keine Remoteverbindungen eingerichtet werden.** Scrolle in diesem Thema zurück zur Frage [Wie richte ich einen PC für Remotedesktop ein?](#how-do-i-set-up-a-pc-for-remote-desktop), um Informationen zur Behebung zu erhalten.
- **Der Remote-PC lässt die Verbindungsherstellung ggf. nur für PCs zu, für die die Authentifizierung auf Netzwerkebene eingerichtet ist.**
- **Unter Umständen ist der Remote-PC ausgeschaltet.** Du kannst keine Verbindung mit einem PC herstellen, der ausgeschaltet ist oder sich im Standbymodus oder Ruhezustand befindet. Stelle daher sicher, dass die Einstellung für den Standbymodus und Ruhezustand auf dem Remote-PC jeweils auf **Nie** festgelegt ist (Ruhezustand ist nicht auf allen PCs verfügbar).

### <a name="why-cant-i-find-or-connect-to-my-pc"></a>Warum kann ich meinen PC nicht finden oder eine Verbindung damit herstellen?

Überprüfen Sie Folgendes:

- Ist der PC eingeschaltet und aktiv?
- Hast du den richtigen Namen bzw. die richtige IP-Adresse eingegeben?

   > [!IMPORTANT]
   > Für die Verwendung des PC-Namens muss dein Netzwerk den Namen per DNS richtig auflösen. In vielen Heimnetzwerken musst du für die Verbindungsherstellung anstelle des Hostnamens die IP-Adresse verwenden.
- Befindet sich der PC in einem anderen Netzwerk? Hast du den PC so konfiguriert, dass externe Verbindungen zulässig sind?  Hilfreiche Informationen findest du unter [Zulassen des Zugriffs auf den PC von außerhalb des Netzwerks](remote-desktop-allow-outside-access.md).
- Stellst du eine Verbindung mit einer unterstützten Windows-Version her?

   > [!NOTE]
   > Windows XP Home, Windows Media Center Edition, Windows Vista Home und Windows 7 Home oder Starter werden ohne Drittanbietersoftware nicht unterstützt.

### <a name="why-cant-i-sign-in-to-a-remote-pc"></a>Warum kann ich mich nicht an einem Remote-PC anmelden?

Wenn du den Anmeldebildschirm des Remote-PC siehst, aber dich nicht anmelden kannst, wurdest du ggf. nicht der Gruppe der Remotedesktopbenutzer oder einer anderen Gruppe mit Administratorrechten auf dem Remote-PC hinzugefügt. Bitte deinen Systemadministrator, dies für dich durchzuführen.

### <a name="which-connection-methods-are-supported-for-company-networks"></a>Welche Verbindungsmethoden werden für Unternehmensnetzwerke unterstützt?

Wenn du von außerhalb des Unternehmensnetzwerks auf den Desktopcomputer in deinem Büro zugreifen möchtest, muss dein Unternehmen dir den Remotezugriff ermöglichen. Der RD-Client unterstützt derzeit Folgendes:

- Terminalservergateway oder Remotedesktopgateway
- Remotedesktop-Webzugriff
- VPN (über integrierte iOS-VPN-Optionen)

### <a name="vpn-doesnt-work"></a>VPN funktioniert nicht

VPN-Probleme können unterschiedliche Ursachen haben. Der erste Schritt ist die Überprüfung, ob das VPN in demselben Netzwerk wie dein PC oder Macintosh-Computer ausgeführt werden kann. Falls das Testen mit einem PC oder Macintosh nicht möglich ist, kannst du versuchen, mit dem Browser deines Geräts auf die Webseite des Unternehmensintranets zuzugreifen.

Weitere Dinge, die überprüft werden sollten:
- **Das VPN wird durch das 3G-Netz blockiert oder beschädigt:** Es gibt weltweit mehrere 3G-Anbieter, von denen 3G-Datenverkehr blockiert oder beschädigt wird. Überprüfe, ob die VPN-Konnektivität mehr als eine Minute lang richtig funktioniert.
- **L2TP- oder PPTP-VPNs:** Wenn du L2TP oder PPTP in deinem VPN verwendest, ist es ratsam, in der VPN-Konfiguration die Option „Jeden Datenverkehr übermitteln“ auf „EIN“ festzulegen.
- **VPN ist falsch konfiguriert:** Ein falsch konfigurierter VPN-Server kann der Grund dafür sein, warum die VPN-Verbindungen nie bzw. nach einiger Zeit nicht mehr funktioniert haben. Teste mit dem Webbrowser des iOS-Geräts oder einem PC oder Macintosh in demselben Netzwerk, ob dies der Fall ist.

### <a name="how-can-i-test-if-vpn-is-working-properly"></a>Wie kann ich testen, ob das VPN richtig funktioniert?

Vergewissere dich, dass das VPN auf deinem Gerät aktiviert ist. Du kannst deine VPN-Verbindung testen, indem du zu einer Webseite in deinem internen Netzwerk navigierst oder einen Webdienst verwendest, der nur per VPN verfügbar ist.

### <a name="how-do-i-configure-l2tp-or-pptp-vpn-connections"></a>Wie konfiguriere ich L2TP- oder PPTP-VPN-Verbindungen?

Wenn du L2TP oder PPTP in deinem VPN verwendest, musst du in der VPN-Konfiguration die Option **Jeden Datenverkehr übermitteln** auf **EIN** festlegen.

## <a name="web-client"></a>Webclient

### <a name="which-browsers-can-i-use"></a>Welche Browser kann ich verwenden?

Der Webclient unterstützt Microsoft Edge, Internet Explorer 11, Mozilla Firefox (v55.0 und höher), Safari und Google Chrome.

### <a name="what-pcs-can-i-use-to-access-the-web-client"></a>Welche PCs kann ich verwenden, um auf den Webclient zuzugreifen?

Der Webclient unterstützt Windows, macOS, Linux und ChromeOS. Mobile Geräte werden derzeit nicht unterstützt.

### <a name="can-i-use-the-web-client-in-a-remote-desktop-deployment-without-a-gateway"></a>Kann ich den Webclient in einer Remotedesktopbereitstellung ohne Gateway verwenden?

Nein Der Client benötigt für die Verbindungsherstellung ein Remotedesktopgateway. Weißt du nicht, was dies bedeutet? Frage bei deinem Administrator nach.

### <a name="does-the-remote-desktop-web-client-replace-the-remote-desktop-web-access-page"></a>Ersetzt der Remotedesktop-Webclient die Seite für den Remotedesktop-Webzugriff?

Nein Der Remotedesktop-Webclient wird unter einer anderen URL als die Seite für den Remotedesktop-Webzugriff gehostet. Du kannst entweder den Webclient oder die Seite für den Webzugriff verwenden, um die Remoteressourcen in einem Browser anzuzeigen.

### <a name="can-i-embed-the-web-client-in-another-web-page"></a>Kann ich den Webclient in eine andere Webseite einbetten?

Dieses Feature wird derzeit nicht unterstützt.

## <a name="monitors-audio-and-mouse"></a>Monitore, Audio und Maus

### <a name="how-do-i-use-all-of-my-monitors"></a>Wie kann ich alle meine Monitore nutzen?
Gehe wie folgt vor, um zwei oder mehr Bildschirme zu nutzen:

1. Klicke mit der rechten Maustaste auf den Remotedesktop, für den du mehrere Bildschirme aktivieren möchtest, und klicke dann auf **Bearbeiten**.
2. Aktiviere die Optionen **Alle Monitore verwenden** und **Vollbild**.

### <a name="is-bi-directional-sound-supported"></a>Wird bidirektionaler Sound unterstützt?
Bidirektionaler Sound kann im Windows-Client auf Verbindungsbasis konfiguriert werden. Auf die relevanten Einstellungen kann auf der Registerkarte **Lokale Ressourcen** im Bereich **Remoteaudio** zugegriffen werden.

### <a name="what-can-i-do-if-the-sound-wont-play"></a>Was kann ich tun, wenn der Sound nicht wiedergegeben wird?
Melde dich von der Sitzung ab und dann wieder an. (Trenne hierbei nicht nur die Verbindung, sondern melde dich vollständig ab.)

## <a name="mac-client---hardware-questions"></a>Macintosh-Client: Hardwarefragen
### <a name="is-retina-resolution-supported"></a>Wird die Netzhautauflösung unterstützt?
Ja. Der Remotedesktopclient unterstützt die Netzhautauflösung.

### <a name="how-do-i-enable-secondary-right-click"></a>Wie aktiviere ich den sekundären Rechtsklick?
Du hast drei Optionen, um den Rechtsklick in einer geöffneten Sitzung zu verwenden:

- USB-Standardmaus mit zwei Tasten für PCs
- Apple Magic Mouse: Klicke zum Aktivieren des Rechtsklicks im Dock auf **Systemeinstellungen** und dann auf **Maus**. Aktiviere anschließend die Option **Secondary click** (Sekundärer Klick).
- Apple Magic Trackpad oder MacBook Trackpad: Klicken Sie zum Aktivieren des Rechtsklicks im Dock auf **Systemeinstellungen** und dann auf **Trackpad**. Aktivieren Sie anschließend die Option **Secondary click** (Sekundärer Klick).

### <a name="is-airprint-supported"></a>Wird AirPrint unterstützt?
Nein. AirPrint wird vom Remotedesktopclient nicht unterstützt. (Dies gilt sowohl für Mac- als auch für iOS-Clients.)

### <a name="why-do-incorrect-characters-appear-in-the-session"></a>Warum werden in der Sitzung fehlerhafte Zeichen angezeigt?
Bei Verwendung einer internationalen Tastatur tritt ggf. ein Problem auf, bei dem die in der Sitzung angezeigten Zeichen nicht mit den Zeichen übereinstimmen, die du auf der Macintosh-Tastatur eingegeben hast.

Dies kann in den folgenden Situationen passieren:

- Du verwendest eine Tastatur, die von der Remotesitzung nicht erkannt wird. Wenn die Tastatur vom Remotedesktop nicht erkannt wird, wird standardmäßig die Sprache verwendet, die zuletzt mit dem Remote-PC verwendet wurde.
- Du stellst eine Verbindung mit einer zuvor getrennten Sitzung auf einem Remote-PC her, für den eine andere Tastatursprache als die verwendet wird, die du gerade nutzen möchtest.

Du kannst dieses Problem beheben, indem du die Tastatursprache für die Remotesitzung manuell festlegst. Siehe die Schritte im nächsten Abschnitt.

### <a name="how-do-language-settings-affect-keyboards-in-a-remote-session"></a>Wie wirken sich Spracheinstellungen auf Tastaturen in einer Remotesitzung aus?
Es gibt viele Arten von Macintosh-Tastaturlayouts. Bei einigen davon handelt es sich um Mac-spezifische oder benutzerdefinierte Layouts, für die unter der Windows-Version, mit der du eine Remoteverbindung herstellst, ggf. keine genaue Übereinstimmung vorhanden ist. Von der Remotesitzung wird deine Tastatur der am ehesten übereinstimmenden Tastatursprache zugeordnet, die auf dem Remote-PC verfügbar ist.

Wenn dein Macintosh-Tastaturlayout auf die PC-Version der Tastatursprache festgelegt ist (z. B. Französisch – PC), sollten alle Tasten richtig zugeordnet sein, und die Tastatur sollte normal funktionieren.

Wenn dein Macintosh-Tastaturlayout auf die Macintosh-Version einer Tastatur festgelegt ist (z. B. Französisch), führt die Remotesitzung für dich eine Zuordnung zur PC-Version der Sprache „Französisch“ durch. Einige Tastenkombination der Macintosh-Tastatur, die du von OSX kennst, funktionieren in der Windows-Remotesitzung nicht.

Wenn dein Tastaturlayout auf eine Variante einer Sprache festgelegt ist (z. B. Französisch (Kanada)) und die Remotesitzung dich nicht der genauen Variante zuordnen kann, wird eine Zuordnung zur am besten geeigneten Sprache durchgeführt (z. B. Französisch). Einige Tastenkombination der Macintosh-Tastatur, die du von OSX kennst, funktionieren in der Windows-Remotesitzung nicht.

Falls dein Tastaturlayout auf ein Layout festgelegt ist, für das die Remotesitzung keine Übereinstimmung findet, wird für die Remotesitzung standardmäßig die Sprache verwendet, die du für den PC zuletzt genutzt hast. In diesem Fall oder in Fällen, in denen du die Sprache deiner Remotesitzung an deine Macintosh-Tastatur anpassen musst, kannst du die Tastatursprache in der Remotesitzung wie unten angegeben manuell auf die am besten passende Sprache festlegen.

Befolge diese Anleitung, um das Tastaturlayout in der Remotedesktopsitzung zu ändern:

**Unter Windows 10 oder Windows 8:**

1. Öffne in der Remotesitzung die Option „Region und Sprache“. Klicke auf **Start > Einstellungen > Zeit und Sprache**. Öffne die Option **Region und Sprache**.
2. Füge die Sprache hinzu, die du verwenden möchtest. Schließe dann das Fenster „Region und Sprache“.
3. In der Remotesitzung wird jetzt die Option zum Umschalten zwischen den Sprachen angezeigt. (In der Remotesitzung rechts in der Nähe der Uhr.) Klicke auf die Sprache, zu der du umschalten möchtest (z. B. **Eng**).

Unter Umständen musst du die derzeit genutzte Anwendung schließen und neu starten, damit die Tastaturänderungen wirksam werden.


## <a name="specific-errors"></a>Spezifische Fehler

### <a name="why-do-i-get-an-insufficient-privileges-error"></a>Warum erhalte ich den Fehler „Unzureichende Berechtigungen“?
Du hast keine Berechtigung für den Zugriff auf die Sitzung, mit der du eine Verbindung herstellen möchtest. Die wahrscheinlichste Ursache ist, dass du versuchst, eine Verbindung mit einer Administratorsitzung herzustellen. Nur Administratoren dürfen eine Verbindung mit der Konsole herstellen. Stelle sicher, dass der Umschalter für die Konsole in den erweiterten Einstellungen des Remotedesktops auf „Aus“ festgelegt ist. Wende dich an den Systemadministrator, um weitere Hilfe zu erhalten, wenn dies nicht die Ursache des Problems ist.

### <a name="why-does-the-client-say-that-there-is-no-cal"></a>Warum kommt vom Client die Meldung, dass keine Clientzugriffslizenz vorhanden ist?
Wenn ein Remotedesktopclient eine Verbindung mit einem Remotedesktopserver herstellt, stellt der Server eine Clientzugriffslizenz für Remotedesktopdienste (RDS-CAL) aus, die vom Client gespeichert wird. Bei jeder erneuten Verbindungsherstellung nutzt der Client seine RDS-CAL, und der Server stellt keine weitere Lizenz aus. Der Server stellt nur dann eine weitere Lizenz aus, wenn die RDS-CAL auf dem Gerät fehlt oder beschädigt ist. Wenn die maximale Anzahl von lizenzierten Geräten erreicht ist, stellt der Server keine neuen RDS-CALs mehr aus. Wende dich an deinen Netzwerkadministrator, um weitere Unterstützung zu erhalten.

### <a name="why-did-i-get-an-access-denied-error"></a>Warum erhalte ich den Fehler „Zugriff verweigert“?
Der Fehler „Zugriff verweigert“ wird vom Remotedesktopgateway generiert und ist das Ergebnis von fehlerhaften Anmeldeinformationen, die während des Verbindungsversuchs verwendet wurden. Überprüfe deinen Benutzernamen und das zugehörige Kennwort. Falls die Verbindung vorher funktioniert hat und der Fehler vor Kurzem aufgetreten ist, hast du unter Umständen das Kennwort deines Windows-Benutzerkontos geändert und es in den Einstellungen für den Remotedesktop noch nicht aktualisiert.

### <a name="what-does-rpc-error-23014-or-error-0x59e6-mean"></a>Was bedeutet „RPC-Fehler 23014“ oder „Fehler 0x59e6“?
Bei **RPC-Fehler 23014** oder **Fehler 0x59E6 Nach einigen Minuten noch einmal versuchen** hat der Remotedesktopgateway-Server die maximale Anzahl von aktiven Verbindungen erreicht. Die maximale Anzahl von Verbindungen variiert je nach Windows-Version, die auf dem Remotedesktopgateway ausgeführt wird: Bei der Windows Server 2008 R2 Standard-Implementierung ist die Anzahl von Verbindungen auf 250 beschränkt. Bei der Windows Server 2008 R2 Foundation-Implementierung ist die Anzahl von Verbindungen auf 50 beschränkt. Für alle anderen Windows-Implementierungen ist eine unbegrenzte Anzahl von Verbindungen zulässig.

### <a name="what-does-the-failed-to-parse-ntlm-challenge-error-mean"></a>Was bedeutet der Fehler „Failed to parse NTLM challenge“ (Fehler beim Analysieren der NTLM-Abfrage)?
Die Ursache dieses Fehlers ist eine fehlerhafte Konfiguration auf dem Remote-PC. Stelle sicher, dass die Einstellung für die RDP-Sicherheitsstufe auf dem Remote-PC auf „Client-kompatibel“ festgelegt ist. (Wende dich an deinen Systemadministrator, falls du hierbei Hilfe benötigst.)

### <a name="what-does-ts_rap-you-are-not-allowed-to-connect-to-the-given-host-mean"></a>Was bedeutet „TS_RAP You are not allowed to connect to the given host“ (TS_RAP: Du bist nicht berechtigt, eine Verbindung mit dem angegebenen Host herzustellen)?
Dieser Fehler tritt auf, wenn durch eine Ressourcenautorisierungsrichtlinie auf dem Gatewayserver verhindert wird, dass über deinen Benutzernamen eine Verbindung mit dem Remote-PC hergestellt wird. Dies kann in den folgenden Fällen passieren:

- Der Name des Remote-PC ist mit dem Namen des Gateways identisch. Wenn du dann versuchst, eine Verbindung mit dem Remote-PC herzustellen, wechselt die Verbindung stattdessen zum Gateway. Hierfür hast du wahrscheinlich keine Zugriffsberechtigung. Falls du eine Verbindung mit dem Gateway herstellen musst, solltest du den Namen des externen Gateways nicht als PC-Name verwenden. Verwende stattdessen „localhost“ bzw. die IP-Adresse (127.0.0.1) oder den Namen des internen Servers.
- Dein Benutzerkonto ist kein Mitglied der Benutzergruppe für den Remotezugriff.
