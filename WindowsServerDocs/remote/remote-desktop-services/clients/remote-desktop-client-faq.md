---
title: Remotedesktopclients – häufig gestellte Fragen
description: Häufig gestellte Fragen zu den Remotedesktopclients
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 785a18cf-a5d0-4bc2-95e4-9ef53ee8f65a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 07/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: ec1b0a17c578f2d8ac55d1704af6b267b6bb8e5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865931"
---
# <a name="frequently-asked-questions-about-the-remote-desktop-clients"></a>Häufig gestellte Fragen zu den Remotedesktopclients

>Gilt für: Windows 10, Windows 8.1, Windows Server 2012 R2, WindowsServer 2016

Nun, da Sie den Remotedesktopclient auf Ihrem Gerät (Android, Mac, iOS oder Windows) eingerichtet haben, können Sie Fragen haben. Hier erhalten Sie Antworten auf die am häufigsten gestellten Fragen zu den Remotedesktop-Clients an. 

- [Einrichten](#Setting-up)
- [Verbindungen, Gateways und Netzwerke](#connection-gateway-and-networks)
- [WebClient](#web-client)
- [Überwacht, Audio und Maus](#monitors-audio-and-mouse)
- [Mac-hardware](#mac-client---hardware-questions)
- [Fehlermeldungen](#specific-errors)

Die meisten dieser Fragen beziehen sich auf alle Clients, aber es gibt einige bestimmte Client-Elemente.

Wenn Sie weitere Fragen, die wir beantworten soll haben, lassen Sie sie als Feedback zu diesem Artikel.

## <a name="setting-up"></a>Einrichten

### <a name="which-pcs-can-i-connect-to"></a>Welche PCs kann ich mit verbinden?

Sehen Sie sich die [unterstützt Configuration](remote-desktop-supported-config.md) Weitere Informationen zum welche PCs können Sie mit verbinden.

### <a name="how-do-i-set-up-a-pc-for-remote-desktop"></a>Wie richte ich ein PC für Remotedesktop ein?

Ich habe mein Gerät einrichten, aber ich glaube nicht, dass die PCs bereit. Hilfe?

Zunächst haben Sie die Setup-Assistenten von Remote Desktop gesehen? Es führt Sie durch die Vorbereitung für den Remotezugriff auf Ihrem PC. Herunterladen und ausführen, die auf Ihrem PC, alles tool festgelegt. 

Andernfalls, wenn Sie Aufgaben manuell ausführen möchten, lesen Sie weiter.

Führen Sie für Windows 10 folgende Schritte aus:

1. Öffnen Sie auf dem Gerät, um eine Verbindung herstellen möchten, **Einstellungen**.
2. Wählen Sie **System** und dann **Remotedesktop**.
3. Verwenden Sie den Schieberegler, um Remotedesktop zu aktivieren.
4. Im Allgemeinen empfiehlt es sich, den PC zu halten, aktiv und sichtbar ist, um Verbindungen zu ermöglichen. Klicken Sie auf **Einstellungen anzeigen** , um die energieeinstellungen für Ihren PC aufzurufen, in dem Sie diese Einstellung ändern können.
   > [!NOTE]
   > Sie können nicht verbinden mit einem PC im Standbymodus oder Ruhezustand befindet, achten Sie also die Einstellungen für Standbymodus und Ruhezustand auf dem Remotecomputer, um festgelegt werden **nie**. (Den Ruhezustand nicht auf allen PCs verfügbar.)


Notieren Sie sich den Namen des diesem PC unter **Herstellen einer Verbindung mit diesem PC**. Sie benötigen diese Option, um die Clients konfigurieren.

Sie können Berechtigungen für bestimmte Benutzer auf diesem PC - klicken Sie zum Ausführen, die erteilen **wählen Benutzer, die Remotezugriff auf diesen PC können**.
Mitglieder der Gruppe "Administratoren" haben automatisch Zugriff auf.

Für Windows 8.1, befolgen Sie die Anweisungen, um Remoteverbindungen in [Herstellen einer Verbindung mit einem anderen Desktop mithilfe von Remotedesktopverbindungen](https://support.microsoft.com/en-us/help/17463/windows-7-connect-to-another-computer-remote-desktop-connection#1TC=windows-8).



## <a name="connection-gateway-and-networks"></a>Verbindung, Gateways und Netzwerke

### <a name="why-cant-i-connect-using-remote-desktop"></a>Warum verbinden kann nicht ich per Remotedesktop?

Hier sind einige möglichen Lösungen für häufiger auftretende Probleme, die auftreten können, wenn auf einem Remotecomputer eine Verbindung herstellen möchten. Wenn diese Lösungen nicht funktionieren, finden Sie weitere Unterstützung für die [Microsoft Community-Website](https://go.microsoft.com/fwlink/p/?LinkId=242079).

- **Der remote-PC kann nicht gefunden werden.** Stellen Sie sicher, dass Sie den richtigen PC-Namen aufweisen, und klicken Sie dann überprüfen, wenn Sie diesen Namen richtig eingegeben haben. Wenn Sie noch keine Verbindung herstellen können, versuchen Sie es der PC-Name anstelle der IP-Adresse des remote-PC.
- **Es liegt ein Problem mit dem Netzwerk.** Stellen Sie sicher, dass Sie über Internetzugang verfügen. 
- **Der Remotedesktop-Port möglicherweise durch eine Firewall blockiert werden.** Wenn Sie Windows-Firewall verwenden, gehen Sie wie folgt vor:

   1. Öffnen Sie Windows-Firewall. 
   2. Klicken Sie auf **können Sie eine app oder ein Feature durch die Windows-Firewall**. 
   3. Klicken Sie auf **Ändern der Einstellungen**. Sie können für ein Administratorkennwort oder zur Bestätigung Ihrer Auswahl aufgefordert werden.
   4. Unter **zugelassene apps und Features**Option **Remotedesktop**, und klicken oder tippen Sie anschließend **OK**.

   Wenn Sie eine andere Firewall verwenden, stellen Sie sicher, dass der Port für Remote Desktop (in der Regel 3389) geöffnet ist.
- **Remoteverbindungen können nicht auf dem Remotecomputer eingerichtet werden.** Um dieses Problem zu beheben, scrollen Sie zurück zum [wie richte ich ein PC für Remotedesktop?](#how-do-i-set-up-a-pc-for-remote-desktop) Frage in diesem Thema.
- **Remote-PC kann nur PCs eine Verbindung herstellen können, die Authentifizierung auf Netzwerkebene eingerichtet haben.** 
- **Der remote-PC kann deaktiviert werden.** Sie können nicht auf einem PC, der ausgeschaltet, im Energiesparmodus ist verbunden oder Ruhezustand befindet, achten Sie also die Einstellungen für Standbymodus und Ruhezustand auf dem Remotecomputer, um festgelegt werden **nie** (Ruhezustand nicht auf allen PCs verfügbar.).

### <a name="why-cant-i-find-or-connect-to-my-pc"></a>Warum kann ich nicht finden oder eine Verbindung mit meinem PC herstellen?
Überprüfen Sie Folgendes:
- Ist der PC auf und aktiv?
- Haben Sie den richtigen Namen oder die IP-Adresse eingegeben?

   > [!IMPORTANT]
   > Mit dem PC-Namen muss das Netzwerk für die namensauflösung über DNS ordnungsgemäß. In vielen Heimnetzwerken müssen Sie die IP-Adresse nicht des Hostnamens zu verwenden, um eine Verbindung herstellen.
- Ist der PC in einem anderen Netzwerk? Konfiguriert Sie können außerhalb von Verbindungen über den PC haben?  Sehen Sie sich [zulassen des Zugriffs auf Ihren PC von außerhalb Ihres Netzwerks](remote-desktop-allow-outside-access.md) um Hilfe zu erhalten.
- Herstellen Sie auf eine unterstützte Version von Windows eine Verbindung? 

   > [!NOTE]
   > Windows XP Home, Windows Media Center Edition, Windows Vista Home und Windows 7 Home oder Starter werden ohne 3rd Party Software nicht unterstützt.

### <a name="why-cant-i-sign-in-to-a-remote-pc"></a>Warum anmelden kann nicht ich auf einem remote-PC?
Wenn Sie den Anmeldebildschirm des remote-PC sehen, aber Sie nicht anmelden, können Sie nicht auf eine beliebige Gruppe mit Administratorrechten auf einem Remotecomputer oder der Gruppe "Remotedesktopbenutzer" hinzugefügt wurden. Bitten Sie den Systemadministrator dies für Sie tun.

### <a name="which-connection-methods-are-supported-for-company-networks"></a>Welche Verbindungsmethoden für Unternehmensnetzwerken unterstützt werden?
Wenn Sie Ihre Office-Desktop aus außerhalb des Firmennetzwerks zugreifen möchten, müssen Sie Ihr Unternehmen eine Möglichkeit des Remotezugriffs angeben. Der Remotedesktop-Client unterstützt derzeit Folgendes:

- Terminal Server-Gateway oder Remotedesktopgateway
- Web Access für Remotedesktop
- VPN (über integrierte iOS-VPN-Optionen)

### <a name="vpn-doesnt-work"></a>VPN funktioniert nicht

VPN-Probleme können mehrere Ursachen haben. Der erste Schritt besteht, stellen Sie sicher, dass das VPN im gleichen Netzwerk wie Ihr PC oder Mac-Computer funktioniert. Wenn Sie nicht mit einem PC oder Mac testen können, können Sie versuchen, auf eine Unternehmens-Intranet-Webseite mit den Browser Ihres Geräts zuzugreifen.

A. überprüfen:
- **Das Netzwerk 3G blockiert oder VPN beschädigt.** Es gibt mehrere 3G-Anbieter in der ganzen Welt, die anscheinend beschädigt 3 G-Datenverkehr zu blockieren. Stellen Sie sicher, dass die VPN-Konnektivität für eine Minute ordnungsgemäß funktioniert.
- **PPTP-VPNs, oder L2TP.** Wenn Sie L2TP und PPTP in Ihr VPN verwenden, legen Sie sämtlichen Datenverkehr senden auf ON in der VPN-Konfiguration.
- **VPN ist falsch konfiguriert.** Falsch konfigurierte VPN-Server kann die Ursache sein, warum gearbeitet VPN-Verbindungen nicht oder nicht mehr nach einiger Zeit. Stellen Sie sicher, Testen mit dem Webbrowser des Geräts oder einem PC oder Mac iOS im selben Netzwerk, wenn dies der Fall.

### <a name="how-can-i-test-if-vpn-is-working-properly"></a>Wie kann ich testen, ob VPN ordnungsgemäß funktioniert?
Stellen Sie sicher, dass das VPN auf Ihrem Gerät aktiviert ist. Sie können Ihre VPN-Verbindung testen, indem Sie soll eine Webseite in Ihrem internen Netzwerk oder mithilfe eines Webdiensts, das nur über das VPN verfügbar ist.

### <a name="how-do-i-configure-l2tp-or-pptp-vpn-connections"></a>Wie konfiguriere ich die L2TP oder PPTP-VPN-Verbindungen?
Wenn Sie L2TP und PPTP in Ihr VPN verwenden, stellen Sie sicher, dass **senden sämtlicher Datenverkehr** zu **ON** in der VPN-Konfiguration.

## <a name="web-client"></a>WebClient

### <a name="which-browsers-can-i-use"></a>Welche Browser kann ich verwenden?

Der Webclient unterstützt Microsoft Edge, Internet Explorer 11, Mozilla Firefox (v55.0 und höher), Google Chrome und Safari.

### <a name="what-pcs-can-i-use-to-access-the-web-client"></a>Den WebClient den Zugriff auf welche PCs kann ich verwenden?

Der Webclient unterstützt Windows, MacOS, Linux und ChromeOS. Mobile Geräte werden zurzeit nicht unterstützt.

### <a name="can-i-use-the-web-client-in-a-remote-desktop-deployment-without-a-gateway"></a>Kann ich den Webclient in einer Remotedesktop-Bereitstellung ohne Gateway verwenden?

Nein. Der Client benötigt ein Remotedesktop-Gateway eine Verbindung herstellen. Nicht wissen, was das bedeutet, dass? Bitten Sie Ihren Administrator, darüber.

### <a name="does-the-remote-desktop-web-client-replace-the-remote-desktop-web-access-page"></a>Ersetzt die Remotedesktop-Web-Client die Seite "Web Access für Remotedesktop"?

Nein. Der Remotedesktop-Webclient wird an einer anderen URL als die Seite "Web Access für Remotedesktop" gehostet. Sie können entweder "Webclient" oder "Web Access-Seite verwenden, um die remote-Ressourcen in einem Browser anzuzeigen.

### <a name="can-i-embed-the-web-client-in-another-web-page"></a>Kann ich den Webclient in einer anderen Webseite einbetten?

Dieses Feature wird zurzeit nicht unterstützt.

## <a name="monitors-audio-and-mouse"></a>Überwacht, Audio und Maus

### <a name="how-do-i-use-all-of-my-monitors"></a>Wie verwende ich alle meine überwacht?
Wenn zwei oder mehrere Bildschirme verwenden möchten, führen Sie folgende Schritte aus:

1. Mit der rechten Maustaste, die Sie verwenden möchten, Aktivieren mehrerer Bildschirme für, und klicken Sie dann auf Remotedesktop **bearbeiten**.
2. Aktivieren Sie **verwenden alle Monitore** und **Vollbild**.

### <a name="is-bi-directional-sound-supported"></a>Werden bidirektionale Sound wird unterstützt?
Sound upstream (vom Client zum Server, für die Mikrofone) wird von Remote Desktop-Client nicht unterstützt.

### <a name="what-can-i-do-if-the-sound-wont-play"></a>Was kann ich tun, wenn der Sound wiedergegeben wird nicht?
Melden Sie sich die Sitzung (nicht nur trennen, melden Sie sich ganz ab), und melden Sie sich dann erneut.

## <a name="mac-client---hardware-questions"></a>Macintosh-Client - Hardware-Fragen
### <a name="is-retina-resolution-supported"></a>Werden Retina-Auflösung wird unterstützt?
Ja, unterstützt der Remotedesktopclient Retina-Auflösung.

### <a name="how-do-i-enable-secondary-right-click"></a>Wie aktiviere ich die sekundäre mit der rechten Maustaste?
Um stellen die mit der rechten Maustaste in eine geöffnete Sitzung Sie drei Möglichkeiten haben nutzen:

- Standard PC zwei Tasten USB-Maus
- Apple-Magic-Maus: Um mit der rechten Maustaste zu aktivieren, klicken Sie auf **Systemeinstellungen** im Dock, klicken Sie auf **Maus**, und aktivieren Sie dann **sekundären auf**.
- Apple-Magic-Trackpad oder MacBook Trackpad: Um mit der rechten Maustaste zu aktivieren, klicken Sie auf **Systemeinstellungen** im Dock, klicken Sie auf **Maus**, und aktivieren Sie dann **sekundären auf**.

### <a name="is-airprint-supported"></a>Werden AirPrint wird unterstützt?
Nein, nicht der Remotedesktopclient AirPrint unterstützt. (Dies gilt für sowohl Mac- und iOS-Clients.)

### <a name="why-do-incorrect-characters-appear-in-the-session"></a>Warum werden ungültige Zeichen in der Sitzung werden angezeigt?
Wenn Sie eine internationale Tastatur verwenden, wird unter Umständen ein Problem die Zeichen, die in der Sitzung angezeigt, bei denen die Zeichen übereinstimmen. Sie haben auf der Mac-Tastatur eingegeben.

Dies kann in den folgenden Szenarien auftreten:

- Sie werden eine Tastatur verwenden, die die remote-Sitzung nicht erkannt wird. Wenn Remotedesktop die Tastatur nicht erkannt wird, wird standardmäßig die zuletzt mit dem remote-PC verwendete Sprache.
- Sie die Verbindung mit einer bereits getrennten Sitzung auf einem Remotecomputer herstellen, und dass remote-PC eine andere Sprache als Sprache verwendet möchten Sie derzeit verwenden.

Sie können dieses Problem beheben, indem Sie die Tastatursprache manuell festlegen, für die Remotesitzung. Lesen Sie die Schritte im nächsten Abschnitt aus.

### <a name="how-do-language-settings-affect-keyboards-in-a-remote-session"></a>Wie wirken spracheinstellungen Tastaturen in einer Remotesitzung?
Es gibt viele Arten von Tastaturlayouts für Mac. Einige davon sind bestimmte Mac-Layouts oder benutzerdefinierte Layouts, die für die eine genaue Übereinstimmung für die Version von Windows sind möglicherweise nicht verfügbar, die Sie Remoting in. Die Remotesitzung ordnet die Tastatur, die am besten geeignete Tastatursprache auf einem Remotecomputer verfügbar. 

Wenn es sich bei Ihrem Mac Tastaturlayout festgelegt ist, auf die PC-Version von der Sprachtastatur (z. B. Französisch – PC), die alle Ihre Schlüssel ordnungsgemäß zugeordnet werden soll, und der Tastatur sollte funktionieren.

Wenn das Tastaturlayout Mac, auf die Mac-Version von einer Tastatur (z. B. Französisch festgelegt ist) wird die Remotesitzung Sie die PC-Version, der die französische Sprache zuordnen. Einige der Mac-Tastenkombinationen, die Sie mit dem unter OSX mithilfe funktioniert nicht in der Remotesitzung von Windows.

Wenn das Tastaturlayout auf eine Variante einer Sprache (z. B. Französisch (Kanada)) festgelegt ist und die Remotesitzung auf diese genaue Variation zugeordnet werden kann, wird die Remotesitzung Sie die nächsten Sprache (z. B. Französisch) zuordnen. Einige der Mac-Tastenkombinationen, die Sie mit dem unter OSX mithilfe funktioniert nicht in der Remotesitzung von Windows.

Wenn das Tastaturlayout zu einem Layout festgelegt ist, die die Remotesitzung überhaupt nicht zuordnen kann, wird die Remotesitzung standardmäßig, um die Sprache zu erhalten, die Sie zuletzt verwendet haben, mit dem PC. In diesem Fall oder in Fällen, in denen Sie zum Ändern der Sprache von der Remotesitzung entsprechend die Mac-Tastatur müssen, können Sie manuell die Tastatursprache in der Remotesitzung in die Sprache festlegen, die die am ehesten dem entspricht, die Sie wie folgt verwenden möchten.

Verwenden Sie die folgenden Anweisungen, um das Tastaturlayout in der Remotedesktopsitzung ändern:

**Auf Windows 10 oder Windows 8:**

1. Öffnen Sie von innerhalb der Remotesitzung die Standardregion und Sprache aus. Klicken Sie auf **Start > Einstellungen > Zeit und Sprache**. Open **Regions- und Spracheinstellungen**.
2. Fügen Sie die Sprache, die Sie verwenden möchten. Schließen Sie das Fenster Regions- und Spracheinstellungen.
3. In der Remotesitzung wird jetzt die Möglichkeit, wechseln Sie zwischen verschiedenen Sprachen angezeigt. (In der rechten Seite der Remotesitzung, in der Nähe der Uhr.) Klicken Sie auf die Sprache, die Sie zum wechseln möchten (z. B. **Eng**).

Sie müssen möglicherweise schließen und neu starten der Anwendung verwendeten derzeit für die Tastatur Änderungen wirksam werden.


## <a name="specific-errors"></a>Bestimmte Fehler

### <a name="why-do-i-get-an-insufficient-privileges-error"></a>Warum erhalte ich Fehler "Nicht genügend Berechtigungen"?
Sie sind nicht zulässig, um die Sitzung zuzugreifen, die, der Sie herstellen möchten. Die wahrscheinlichste Ursache ist, dass Sie in einer administratorsitzung herstellen möchten. Nur Administratoren dürfen auf der Konsole eine Verbindung herstellen. Stellen Sie sicher, dass die Konsole wechseln in den erweiterten Einstellungen des Remotedesktops deaktiviert ist. Wenn dies nicht die Ursache des Problems ist, wenden Sie sich an Ihren Systemadministrator, um Hilfe zu erhalten.

### <a name="why-does-the-client-say-that-there-is-no-cal"></a>Warum also der Client ohne CAL ist?
Wenn ein Remotedesktop-Client auf einem Remotedesktop-Server verbunden ist, gibt der Server eine Remote Desktop Services Client Access License (RDS-CAL) gespeichert, die vom Client an. Wenn der Client die Verbindung erneut wird verwendet, die RDS-CAL und der Server gibt eine weitere Lizenz nicht. Der Server wird eine weitere Lizenz ausstellen, wenn die RDS-CAL auf dem Gerät fehlt oder beschädigt ist. Wenn die maximale Anzahl von lizenzierten Geräte erreicht ist wird der Server keine neue RDS-CALs ausstellen. Wenden Sie sich an Ihren Netzwerkadministrator, um Unterstützung zu erhalten.

### <a name="why-did-i-get-an-access-denied-error"></a>Warum erhalte ich einen Fehler "Zugriff verweigert"?
Der Fehler "Zugriff verweigert" ist während des Verbindungsversuchs einer von der Remotedesktop-Gateway und das Ergebnis der falsche Anmeldeinformationen generiert. Überprüfen Sie Ihren Benutzernamen und Ihr Kennwort ein. Wenn die Verbindung, bevor funktioniert der Fehler aufgetreten, vor kurzem ist und das Kennwort Ihres Windows-Benutzerkontos geändert Sie möglicherweise an und noch nicht aktualisiert, noch in den Einstellungen für Remotedesktop.

### <a name="what-does-rpc-error-23014-or-error-0x59e6-mean"></a>Was bedeutet "RPC-Fehler 23014" oder "Error 0x59e6" Mean?
Im Fall von einem **RPC-Fehlers 23014** oder **Fehler 0x59E6 und wiederholen Sie dann einige Minuten warten**, der RD-Gateway-Server hat die maximale Anzahl der aktiven Verbindungen erreicht. Abhängig von der Windows-Version unterscheidet sich in die maximale Anzahl von Verbindungen auf dem RD-Gateway ausgeführt wird: Die Windows Server 2008 R2 Standard Implementierung beschränkt die Anzahl der Verbindungen auf 250. Die Implementierung von Windows Server 2008 R2 Foundation schränkt die Anzahl der Verbindungen auf 50. Alle anderen Windows-Implementierungen können eine unbegrenzte Anzahl von Verbindungen.

### <a name="what-does-the-failed-to-parse-ntlm-challenge-error-mean"></a>Was bedeutet, dass der Fehler "Fehler beim Analysieren von NTLM Challenge"?
Dieser Fehler wird durch eine fehlerhafte Konfiguration auf einem Remotecomputer verursacht. Stellen Sie sicher, dass die RDP-Sicherheitsstufe auf einem Remotecomputer festgelegt ist "Client-kompatibel." (Wenden Sie sich an Ihren Systemadministrator, wenn Sie hierzu Unterstützung benötigen.)

### <a name="what-does-tsrap-you-are-not-allowed-to-connect-to-the-given-host-mean"></a>Was ist "TS_RAP sind Sie nicht berechtigt, Verbindung mit dem angegebenen Host" bedeuten?
Dieser Fehler tritt beim Beenden von einer Autorisierungsrichtlinie für Ressourcen, auf dem Gatewayserver Ihren Benutzernamen, eine Verbindung mit einem Remotecomputer herstellen. Dies kann in den folgenden Fällen geschehen:

- Der remote-PC-Name ist identisch mit den Namen des Gateways. Klicken Sie dann, wenn Sie versuchen, eine Verbindung mit dem remote-PC, wird die Verbindung an das Gateway stattdessen, die Sie wahrscheinlich haben keine Berechtigung zum Zugriff auf. Wenn Sie eine Verbindung mit dem Gateway herstellen müssen, verwenden Sie nicht der Name des externen Gateways als PC-Namen auf. Verwenden Sie "Localhost" oder die IP-Adresse (127.0.0.1) oder den internen Servernamen an.
- Ihr Benutzerkonto ist nicht Mitglied der Benutzergruppe für den Remotezugriff.