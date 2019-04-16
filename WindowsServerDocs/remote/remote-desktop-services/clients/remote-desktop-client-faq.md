---
title: Remotedesktopclients – häufig gestellte Fragen
description: Häufig gestellte Fragen zu den Remotedesktop-clients
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
ms.sourcegitcommit: d5f10c0c98a9976a86be9f4fa8866650c7fcfc1a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2019
ms.locfileid: "9065947"
---
# Häufig gestellte Fragen zu den Remotedesktop-clients

>Gilt für: Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2016

Nun, da Sie den Remotedesktop-Client auf Ihrem Gerät (Android, Mac, iOS oder Windows) eingerichtet haben, können Sie Fragen haben. Hier erhalten Sie Antworten auf die am häufigsten gestellten Fragen zu den Remotedesktop-Clients. 

- [Einrichten von](#Setting-up)
- [Verbindungen, Gateway und Netzwerke](#connection-gateway-and-networks)
- [WebClient](#web-client)
- [Monitore, Audio und Maus](#monitors-audio-and-mouse)
- [Mac-hardware](#mac-client---hardware-questions)
- [Fehlermeldungen](#specific-errors)

Die meisten dieser Fragen gelten für alle Clients, aber es gibt einige bestimmte Client-Elemente.

Wenn Sie weitere Fragen, die Sie uns haben beantworten möchten, lassen sie als Feedback in diesem Artikel.

## Einrichten von

### Welche PCs kann ich mit verbinden?

Sehen Sie sich im Artikel über [unterstützte Konfiguration](remote-desktop-supported-config.md) Informationen über welche PCs, die Sie eine Verbindung herstellen können.

### Wie richte ich einen PC für Remotedesktop ein?

Ich habe mein Gerät einrichten, denken Sie ich nicht der PC bereit. Hilfe?

Zunächst haben Sie gesehen, der Remote Desktop-Setup-Assistent? Es führt Sie durch die Umstellung von Ihrem PCs für den Remotezugriff. Herunterladen und ausführen, die auf Ihrem PC, alles zu tool festgelegt werden. 

Andernfalls, wenn Sie Schritte manuell ausführen möchten, lesen Sie.

Gehen Sie für Windows 10 wie folgt:

1. Öffnen Sie auf dem Gerät, die, dem Sie für eine Verbindung herstellen möchten die **Einstellungen**.
2. Wählen Sie **System** und **Remotedesktop**.
3. Verwenden Sie den Schieberegler, um Remote Desktop zu aktivieren.
4. Im Allgemeinen empfiehlt es sich um den PC länger aktiviert und für Verbindungen zu erleichtern sichtbar zu schützen. Klicken Sie auf **Einstellungen anzeigen** , fahren Sie mit der ein/aus-Einstellungen für Ihren PC, in dem Sie diese Einstellung ändern können.
   > [!NOTE]
   > Nicht schließen an einen PC, der sich im Standbymodus oder Ruhezustand befindet, stellen Sie daher sicher, dass die Einstellungen für Standbymodus und Ruhezustand auf dem remote-PC auf **nie**festgelegt sind. (Ruhezustand nicht auf alle PCs verfügbar.)


Notieren Sie den Namen eines dieser PC unter **diesem PC Herstellen einer Verbindung**. Sie benötigen diese Option, um die Clients konfiguriert werden.

Sie können die Berechtigung für bestimmte Benutzer auf diesem PC - hierzu klicken Sie auf **auswählen, die diesen PC Remotezugriff können, Benutzer**zugreifen.
Mitglieder der Gruppe der Administratoren haben automatisch Zugriff.

Folgen Sie für Windows 8.1 den Anweisungen zum Zulassen von Remoteverbindungen in [Verbindung mit einem anderen Remotedesktopverbindungen mit Desktop](https://support.microsoft.com/en-us/help/17463/windows-7-connect-to-another-computer-remote-desktop-connection#1TC=windows-8).



## Verbindung, Gateway und Netzwerke

### Warum kann ich keine Verbindung herstellen mithilfe von Remotedesktop?

Hier sind einige möglichen Lösungen für allgemeine Probleme, die auftreten können, wenn einem remote-PC eine Verbindung herstellen möchten. Wenn diese Lösungen nicht geeignet sind, finden Sie weitere Hilfe auf der [Microsoft-Community-Website](https://go.microsoft.com/fwlink/p/?LinkId=242079).

- **Remote-PC kann nicht gefunden werden.** Stellen Sie sicher, dass Sie den richtigen PC-Namen haben, und um festzustellen, ob Sie den Namen richtig eingegeben haben. Wenn Sie noch keine Verbindung herstellen können, versuchen Sie die IP-Adresse des remote-PC anstelle der PC-Name.
- **Es ist ein Problem mit dem Netzwerk.** Stellen Sie sicher, dass Sie die Verbindung mit dem Internet haben. 
- **Der Remotedesktop-Port möglicherweise durch eine Firewall blockiert werden.** Wenn Sie Windows-Firewall verwenden, gehen Sie folgendermaßen vor:

   1. Öffnen Sie Windows-Firewall. 
   2. Klicken Sie auf **eine app oder Feature zulassen über Windows-Firewall**. 
   3. Klicken Sie auf **Einstellungen ändern**.  Möglicherweise werden Sie aufgefordert, ein Administratorkennwort einzugeben oder Ihre Auswahl zu bestätigen.
   4. **Zugelassenen apps und Features**wählen Sie **Remote Desktop**, und tippen Sie dann auf oder klicken Sie auf **OK**.

   Wenn Sie eine andere Firewall verwenden, stellen Sie sicher, dass der Port für Remotedesktop (normalerweise Port 3389) geöffnet ist.
- **Remoteverbindungen möglicherweise nicht auf die remote-PC eingerichtet werden.** Um dieses Problem zu beheben, führen Sie einen Bildlauf zurück nach oben [Wie richte ich einen PC für Remotedesktop?](#how-do-i-set-up-a-pc-for-remote-desktop) Frage in diesem Thema.
- **Remote-PC möglicherweise nur PCs Verbindung ermöglichen, die Authentifizierung auf Netzwerkebene eingerichtet haben.** 
- **Remote-PC ist möglicherweise deaktiviert.** Nicht verbinden mit einem PC, der im Ruhezustand deaktiviert ist, oder im Ruhezustand, um sicherzustellen, die Einstellungen für Standbymodus und Ruhezustand auf dem remote-PC auf **nie** festgelegt sind (Ruhezustand nicht auf alle PCs verfügbar.).

### Warum kann ich nicht finden oder PC herstellen?
Überprüfen Sie Folgendes:
- Ist der PC und sich im Normalzustand?
- Eingeben Sie die richtigen Namen oder IP-Adresse?

   > [!IMPORTANT]
   > Der PC-Name muss das Netzwerk für den Namen ordnungsgemäß durch DNS aufzulösen. In vielen privaten Netzwerken müssen Sie die IP-Adresse anstelle der Hostname verwenden, um eine Verbindung herstellen.
- Ist der PC in einem anderen Netzwerk? Haben Sie den PC außerhalb Verbindungen über lassen konfiguriert?  Entdecken Sie [Zugriff auf Ihren PC vor außerhalb Ihres Netzwerks zulassen](remote-desktop-allow-outside-access.md) für Hilfe.
- Verbinden Sie auf eine unterstützte Version von Windows? 

   > [!NOTE]
   > Windows XP Home, Windows Media Center Edition, Windows Vista Home und Windows 7 Home oder Starter werden ohne 3rd Party-Software nicht unterstützt.

### Warum anmelden kann nicht Bereiche auf einem remote-PC?
Wenn der Anmeldebildschirm von remote-PC angezeigt wird, aber Sie können anmelden, können Sie nicht Remote Desktop Benutzergruppe oder einer anderen Gruppe mit Administratorrechten auf dem remote-PC hinzugefügt wurden. Bitten Sie Ihr Systemadministrator für Sie.

### Welche Verbindungsmethoden für Unternehmensnetzwerke unterstützt werden?
Wenn Sie auf Ihrem Desktop Office von außerhalb Ihres Unternehmens-Netzwerks zugreifen möchten, müssen Sie Ihr Unternehmen mit dem remote-Zugriff bereitstellen. Den Remotedesktopclient unterstützt derzeit die folgenden:

- Terminal-Server-Gateway oder Remotedesktopgateway
- Web Access für Remotedesktop
- VPN (über iOS integrierte VPN-Optionen)

### VPN nicht geeignet.

VPN-Probleme können verschiedene Ursachen haben. Der erste Schritt wird sichergestellt, dass das VPN im selben Netzwerk wie der PC oder Mac-Computer funktioniert. Wenn Sie nicht mit einem PC oder Mac testen können, können Sie versuchen, eine Unternehmens-Intranet-Webseite mit den Browser Ihres Geräts zugreifen.

Weitere Dinge überprüfen:
- **Das Netzwerk 3G blockiert oder beschädigt VPN.** Es gibt mehrere 3G-Anbietern in der Welt zusammen, die scheinen beschädigt 3 G-Datenverkehr zu blockieren. Stellen Sie sicher, dass die VPN-Konnektivität für über eine Minute ordnungsgemäß funktioniert.
- **L2TP oder PPTP VPNs.** Wenn Sie in einer VPN L2TP oder PPTP verwenden, legen Sie senden der gesamte Datenverkehr auf ON in der VPN-Konfiguration.
- **VPN ist falsch konfiguriert.** Falsch konfigurierten VPN-Server kann der Grund, warum gearbeitet die VPN-Verbindungen nie oder mehr funktioniert nach einiger Zeit. Stellen Sie sicher, mit der iOS des Geräts Webbrowser oder einem PC oder Mac im gleichen Netzwerk testen, in diesem Fall.

### Wie kann ich testen, ob VPN ordnungsgemäß funktioniert?
Stellen Sie sicher, dass VPN auf Ihrem Gerät aktiviert ist. Sie können die VPN-Verbindung testen, indem Sie eine Webseite im internen Netzwerk soll oder einen Webdienst, der nur über das VPN verfügbar ist.

### Wie konfiguriere ich L2TP oder PPTP VPN-Verbindungen?
Wenn Sie in einer VPN L2TP oder PPTP verwenden, stellen Sie sicher, dass **der gesamte Datenverkehr zu senden** , die auf **ON** in der VPN-Konfiguration festgelegt.

## WebClient

### Welche Browser kann ich verwenden?

Der Webclient unterstützt Microsoft Edge, Internet Explorer 11 Mozilla Firefox (v55.0 und höher), Safari und Google Chrome.

### Welche PCs kann für den Clientzugriff Web verwenden?

Der Webclient unterstützt Windows, MacOS, Linux und ChromeOS. Mobile Geräte werden zu diesem Zeitpunkt nicht unterstützt.

### Kann ich den Webclient in einer Remotedesktop-Bereitstellung ohne ein Gateway verwenden?

Nein. Der Client erfordert eine Remotedesktopgateway, eine Verbindung herzustellen. Nicht wissen, was bedeutet, dass? Informieren Sie den Administrator.

### Ersetzt der Remotedesktop-Webclient der Seite "Web Access für Remotedesktop"?

Nein. Der Remotedesktop-Webclient wird an eine andere URL als die Web Access für Remotedesktop-Seite gehostet. Sie können dem Webclient oder auf der Seite "Web Access" verwenden, die remote-Ressourcen in einem Browser anzeigen.

### Können den Webclient in einer anderen Webseite werden eingebettet?

Diese Funktion wird derzeit nicht unterstützt.

## Monitore, Audio und Maus

### Wie werden alle Monitore verwendet?
Wenn zwei oder mehr Bildschirme verwenden möchten, führen Sie folgende Schritte aus:

1. Mit der rechten Maustaste in des Remotedesktops, dem Sie mehrere Bildschirme für aktivieren möchten, und klicken Sie dann auf **Bearbeiten**.
2. Aktivieren Sie **Alle Monitore verwenden** und als **Vollbild**.

### Werden bidirektionale Sound wird unterstützt?
Sound upstream (vom Client an den Server, Mikrofon) wird von der Remotedesktop-Client nicht unterstützt.

### Was kann ich tun, wenn der Sound wiedergegeben wird?
Melden Sie sich die Sitzung (nicht nur trennen, melden Sie sich ganz ab), und melden Sie sich anschließend erneut.

## Mac-Client - Hardware Fragen
### Werden Netzhaut Auflösung wird unterstützt?
Ja, unterstützt die Remotedesktopclient Netzhaut Auflösung.

### Wie aktiviere ich sekundäre mit der rechten Maustaste?
Um machen mit der rechten Maustaste in eine offene Sitzung verfügen Sie über drei Optionen verwenden:

- Standard PC zwei Schaltfläche USB-Maus
- Apple Magic Maus: Mit der rechten Maustaste klicken Sie auf **Den Systemeinstellungen** im Dock, klicken Sie auf **Maus**, und aktivieren Sie dann die **sekundäre klicken Sie auf**.
- Apple Magic Trackpad oder MacBook Trackpad: Aktivieren mit der rechten Maustaste, klicken Sie auf **Den Systemeinstellungen** im Dock, klicken mit **Maus**und dann aktivieren **sekundäre klicken Sie auf**.

### Werden AirPrint wird unterstützt?
Nein, nicht der Remotedesktopclient AirPrint unterstützt. (Dies gilt für sowohl Mac- und iOS-Clients.)

### Warum werden falsche Zeichen in der Sitzung angezeigt?
Wenn Sie eine internationale Tastatur verwenden, möglicherweise angezeigt, ein Problem, in denen die Zeichen, die in der Sitzung angezeigt werden die Zeichen, passen Sie auf der Mac-Tastatur eingegeben haben.

Dies kann in den folgenden Szenarien auftreten:

- Verwenden Sie eine Tastatur, die die Remotesitzung nicht erkennt. Wenn Remotedesktop die Tastatur nicht erkannt wird, wird standardmäßig die letzten mit dem remote-PC verwendete Sprache.
- Beim Verbinden mit einer zuvor getrennten Sitzung auf einem remote-PC und remote-PC eine andere Sprache als die Sprache verwendet möchten Sie derzeit verwenden.

Sie können dieses Problem beheben, manuell durch Festlegen der Sprache für die Remotesitzung. Lesen Sie die Schritte im nächsten Abschnitt.

### Wie wirken eingestellte Anzeigesprache Tastaturen in einer Remotesitzung?
Es gibt viele Arten von Mac-Tastaturlayouts. Einige dieser Elemente sind bestimmte Mac-Layouts oder benutzerdefinierte Layouts für die eine genaue Übereinstimmung auf die Version von Windows u. u. nicht verfügbar, die Sie in Remoting. Die Remotesitzung ordnet die Tastatur die am besten passende Tastatursprache auf remote-PCs verfügbar. 

Wenn das Tastaturlayout Mac gesetzt ist, sollte die PC-Version von der Sprache-Tastatur (z. B. Französisch – PC), die alle Ihre Schlüssel richtig zugeordnet werden soll und die Tastatur nur funktionieren.

Wenn das Mac-Tastaturlayout auf die Mac-Version der Tastatur (z. B. Französisch) festgelegt ist ordnen die Remotesitzung auf die PC-Version von Französisch Sie. Einige der Mac-Tastenkombinationen, die Sie werden, verwendet um auf OSX funktioniert nicht in der Windows-Remotesitzung.

Wenn das Tastaturlayout auf eine Variante einer Sprache (z. B. Französisch (Kanada)) festgelegt ist und die Remotesitzung Sie diese genaue Variante zuordnen kann nicht, ordnen die Remotesitzung auf die nächste Sprache (z. B. Französisch) Sie. Einige der Mac-Tastenkombinationen, die Sie werden, verwendet um auf OSX funktioniert nicht in der Windows-Remotesitzung.

Wenn das Tastaturlayout zu einem Layout, die die Remotesitzung keinerlei Übereinstimmung kann nicht festgelegt ist, wird der Remotesitzung standardmäßig, damit die Sprache, die Sie zuletzt mit diesem PC verwendet werden kann. In diesem Fall oder in Fällen, in denen müssen Sie die Sprache für Ihre Remotesitzung entsprechend die Mac-Tastatur, können Sie die Tastatursprachen manuell in der Remotesitzung auf die Sprache festlegen, die der größten Übereinstimmung mit der Sie wie folgt verwenden möchten.

Verwenden Sie die folgenden Anweisungen, um das Tastaturlayout innerhalb der Remotedesktopsitzung ändern:

**Für Windows 10 oder Windows 8:**

1. Öffnen Sie in innerhalb der Remotesitzung, Region und Sprache aus. Klicken Sie auf **> Einstellungen > Zeit und Sprache**. Öffnen Sie die **Region und Sprache**.
2. Fügen Sie die Sprache, die Sie verwenden möchten. Schließen Sie das Fenster Region und Sprache.
3. In der Remotesitzung, wird jetzt die Möglichkeit zum Wechseln zwischen Sprachen angezeigt. (In der rechten Seite der Remotesitzung, in der Nähe der Uhr.) Klicken Sie auf die Sprache, die, der Sie in den (z. B. **Eng**) wechseln möchten.

Sie müssen zu schließen, starten Sie die Anwendung, die Sie derzeit für die Tastatur Änderungen verwenden wirksam wird.


## Spezifischen Fehler

### Warum wird die Fehlermeldung "Keine ausreichenden Berechtigungen"?
Sie sind nicht zulässig, auf die Sitzung zuzugreifen, die, der Sie für eine Verbindung herstellen möchten. Der wahrscheinlichste Grund ist, dass Sie zu einer Admin-Sitzung eine Verbindung herstellen möchten. Nur Administratoren dürfen auf der Konsole eine Verbindung herstellen. Überprüfen Sie, ob der Console Switch in den erweiterten Einstellungen von der Remotedesktop deaktiviert ist. Ist dies nicht die Ursache des Problems, wenden Sie sich an Ihr Systemadministrator, um Hilfe zu erhalten.

### Warum sagen der Client, dass es keine CAL ist?
Wenn Remotedesktopclients eine Verbindung mit einem Remotedesktop-Server herstellt, sendet der Server eine Remote Desktop Services-Clientzugriffslizenz (RDS-CALs) vom Client gespeichert. Wenn der Client eine Verbindung herstellt wird erneut seine RDS-CAL verwendet, und der Server wird eine andere Lizenz nicht ausgeben. Der Server wird eine andere Lizenz ausstellen, wenn der RDS-CALs auf dem Gerät fehlt oder beschädigt ist. Wenn die maximale Anzahl von lizenzierten Geräten erreicht ist wird der Server nicht neue RDS-CALs ausstellen. Wenden Sie sich an den Netzwerkadministrator, um Unterstützung zu erhalten.

### Warum habe ich einen Fehler "Zugriff verweigert" erhalten?
Der Fehler "Zugriff verweigert" ist während der Verbindungsversuch einer generierten durch den Remotedesktopgateway und das Ergebnis der falsche Anmeldeinformationen. Überprüfen Sie Ihren Benutzernamen und Kennwort. Wenn die Verbindung funktioniert, und der Fehler aufgetreten, vor kurzem ist, Sie möglicherweise das Kennwort für Ihr Windows-Benutzerkonto geändert und noch nicht aktualisiert es noch nicht in der Remotedesktop-Einstellungen.

### Was geschieht bei "RPC-Fehler 23014" oder "Error 0x59e6" Mean?
Bei einer **RPC-Fehler 23014** oder **Fehler 0x59E6 versuchen Sie es erneut einige Minuten warten**hat der RD-Gateway-Server die maximale Anzahl der aktiven Verbindungen erreicht. Abhängig von der Windows-Version unterscheidet die maximale Anzahl von Verbindungen auf die RD-Gateway ausgeführt: die Windows Server 2008 R2 Standard-Implementierung wird die Anzahl der Verbindungen zu 250 beschränkt. Die Implementierung von Windows Server 2008 R2 Foundation wird die Anzahl der Verbindungen zu 50 beschränkt. Alle anderen Windows-Implementierungen ermöglichen eine unbegrenzte Anzahl von Verbindungen.

### Was bedeutet, dass der Fehler "Fehler beim Analysieren von NTLM-Anfrage"?
Dieser Fehler wird durch eine Fehlkonfiguration auf dem remote-PC verursacht. Stellen Sie sicher, dass die RDP-Sicherheitsstufe auf dem remote-PC auf festgelegt ist "Kompatibel mit dem Client." (Wenden Sie sich an Ihr Systemadministrator, wenn Sie auf diese Weise Hilfe benötigen.)

### Was ist "TS_RAP Sie dürfen keine Verbindung mit dem angegebenen Host" bedeutet?
Dieser Fehler tritt bei einer Ressource Autorisierungsrichtlinie auf dem Gatewayserver Ihren Benutzernamen Herstellen einer Verbindung mit dem remote-PC beendet. Dies kann passieren, in den folgenden Fällen:

- Der remote-PC-Name ist identisch mit den Namen des Gateways. Dann, wenn Sie versuchen, mit dem remote-PC verbinden, wird die Verbindung mit dem Gateway stattdessen haben Sie wahrscheinlich nicht über die Berechtigung zum zugreifen. Wenn Sie für die Verbindung mit dem Gateway müssen, verwenden Sie den externen Gateway-Namen nicht als PC-Namen. Verwenden Sie stattdessen "Localhost" oder die IP-Adresse (127.0.0.1) oder den internen Servernamen.
- Das Benutzerkonto ist ein Mitglied der Gruppe für den Remotezugriff nicht.