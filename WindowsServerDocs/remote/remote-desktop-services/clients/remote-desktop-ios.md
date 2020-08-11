---
title: Erste Schritte mit dem iOS-Client
description: Informationen zum Einrichten des Remotedesktopclients für iOS
ms.topic: article
ms.assetid: 03ec5a3d-d3f2-4afd-9405-ae58b6ecc91c
author: Heidilohr
manager: lizross
ms.author: helohr
ms.date: 07/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 723fa40e1c2d446381b333eee1289a25adefd5d8
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997367"
---
# <a name="get-started-with-the-ios-client"></a>Erste Schritte mit dem iOS-Client

>Gilt für: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Sie können den Remotedesktopclient für iOS verwenden, um mit Windows-Apps, -Ressourcen und -Desktops auf Ihrem iOS-Gerät (auf iPhones und iPads) zu arbeiten.

Verwenden Sie die folgenden Informationen für die ersten Schritte. Lesen Sie unbedingt die [häufig gestellten Fragen](remote-desktop-client-faq.md), wenn Sie Fragen haben.

> [!NOTE]
> - Möchten Sie mehr über die neuen Versionen für den iOS-Client erfahren? Lesen Sie [Neuerungen bei Remotedesktop unter iOS](ios-whatsnew.md).
> - Der iOS-Client unterstützt Geräte unter iOS 6.x oder höher.

## <a name="get-the-remote-desktop-client-and-start-using-it"></a>Abrufen des Remotedesktopclients und Ausführen der ersten Schritte

In diesem Abschnitt erfahren Sie, wie Sie den Remotedesktopclient für iOS herunterladen und einrichten.

### <a name="download-the-remote-desktop-client-from-the-ios-store"></a>Herunterladen des Remotedesktopclients aus dem App Store für iOS-Geräte

Zuerst müssen Sie den Client herunterladen und Ihren PC für die Verbindung zu Remoteressourcen konfigurieren.

So laden Sie den Client herunter

1. Lade den Microsoft-Remotedesktopclient aus dem [iOS App Store](https://aka.ms/rdios) oder über [iTunes](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8) herunter.
2. [Richten Sie Ihren PC so ein, dass Remoteverbindungen zulässig sind](remote-desktop-client-faq.md#how-do-i-set-up-a-pc-for-remote-desktop).

### <a name="add-a-pc"></a>Hinzufügen eines PC

Nachdem Sie den Client heruntergeladen und Ihren PC für die Annahme von Remoteverbindungen konfiguriert haben, sind Sie bereit, einen PC hinzuzufügen.

So fügst du einen PC hinzu

1. Tippen Sie im Connection Center auf **+** und dann auf **PC hinzufügen**.
2. Geben Sie die folgenden Informationen ein:
   - **PC-Name**: Der Name des Computers. Der PC-Name kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können auch Portinformationen an den PC-Namen anfügen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**).
   - **Benutzername**: Der Benutzername, den Sie für den Zugriff auf den Remotecomputer verwenden. Sie können die folgenden Formate verwenden: *Benutzername*, *Domäne\Benutzername* oder `user_name@domain.com`. Du kannst auch **Ask when required** (Erfragen, wenn erforderlich) auswählen, um bei Bedarf zur Eingabe eines Benutzernamens und Kennworts aufzufordern.
3. Sie können auch die folgenden zusätzlichen Optionen festlegen:
   - **Anzeigename (optional):** ein einfach zu merkender Name für den PC, mit dem du eine Verbindung herstellst. Du kannst eine beliebige Zeichenfolge verwenden, aber wenn du keinen Anzeigenamen angibst, wird stattdessen der Name des PC angezeigt.
   - **Gateway (optional)** : Das Remotedesktopgateway, das Sie zum Herstellen einer Verbindung mit virtuellen Desktops, RemoteApp-Programmen und sitzungsbasierten Desktops in einem internen Unternehmensnetzwerk verwenden möchten. Sie erhalten die Informationen über das Gateway von Ihrem Systemadministrator.
   - **Sound**: Wählen Sie das während der Remotesitzung für Audio zu verwendende Gerät aus. Sie können auswählen, ob Sound auf den lokalen Geräten, auf dem Remotegerät oder überhaupt nicht wiedergegeben werden soll.
   - **Maustasten tauschen**: Wenn eine Mausbewegung einen Befehl mit der linken Maustaste senden würde, wird derselbe Befehl stattdessen mit der rechten Maustaste gesendet. Das Tauschen von Maustasten ist erforderlich, wenn der Remote-PC für den Linkshänder-Mausmodus konfiguriert ist.
   - **Administratormodus**: Stellen Sie eine Verbindung mit einer Verwaltungssitzung auf einem Server unter Windows Server 2003 oder höher her.
   - **Zwischenablage:** Wähle aus, ob Text und Bilder in der Zwischenablage an deinen PC umgeleitet werden sollen.
   - **Speicher:** Wähle aus, ob der Speicher an deinen PC umgeleitet werden soll.
4. Tippen Sie auf **Speichern**.

Müssen Sie diese Einstellungen bearbeiten? Drücken und halten Sie den Desktop, den Sie bearbeiten möchten, und tippen Sie dann auf das Symbol „Einstellungen“.

### <a name="add-a-workspace"></a>Hinzufügen eines Arbeitsbereichs

Zum Abrufen einer Liste verwalteter Ressourcen, auf die du auf deinem iOS-System zugreifen kannst, füge einen Arbeitsbereich hinzu, indem du den vom Administrator bereitgestellten Feed abonnierst.

So fügst du einen Arbeitsbereich hinzu

1. Tippe im Connection Center auf **+** und dann auf **Arbeitsbereich hinzufügen**.
2. Gib im Feld „Feed-URL“ die URL für den Feed ein, den du hinzufügen möchtest. Diese URL kann eine URL oder eine E-Mail-Adresse sein.
   - Verwende im Fall einer URL die vom Administrator erhaltene.
      - Diese URL ist normalerweise eine Windows Virtual Desktop-URL. Welche Sie verwenden, hängt davon ab, welche Version von Windows Virtual Desktop Sie verwenden.
        - Für die Fall 2019-Version verwenden Sie `https://rdweb.wvd.microsoft.com/api/feeddiscovery/webfeeddiscovery.aspx`.
        - Für die Spring 2020-Version verwenden Sie `https://rdweb.wvd.microsoft.com/api/arm/feeddiscovery`.
   - Gib im Fall einer E-Mail-Adresse deine E-Mail-Adresse ein. Durch Eingeben Ihrer E-Mail-Adresse wird der Client angewiesen, nach einer URL zu suchen, die Ihrer E-Mail-Adresse zugeordnet ist, sofern der Administrator dies entsprechend konfiguriert hat.
3. Tippen Sie auf **Weiter**.
4. Gib bei einer entsprechenden Aufforderung deine Anmeldeinformationen an.
   - Gib für **Benutzername** den Benutzernamen eines Kontos mit der Berechtigung zum Zugriff auf Ressourcen an.
   - Gib für **Kennwort** das Kennwort für das Konto an.
   - Abhängig von den Einstellungen, mit denen der Administrator die Authentifizierung konfiguriert hat, wirst du möglicherweise auch aufgefordert, zusätzliche Informationen anzugeben.
5. Tippen Sie auf **Speichern**.

Danach sollten die Remoteressourcen im Connection Center angezeigt werden.

Nachdem du einen Feed abonniert hast, wird der Inhalt dieses Feeds automatisch regelmäßig aktualisiert. Dabei können basierend auf Änderungen durch den Administrator Ressourcen hinzugefügt, geändert oder entfernt werden.

## <a name="manage-your-user-accounts"></a>Verwalten Ihrer Benutzerkonten

Wenn du eine Verbindung mit einem PC oder Arbeitsbereich herstellst, kannst du die Benutzerkonten speichern, um sie erneut auswählen zu können.

Gehen Sie wie folgt vor, um ein neues Benutzerkonto zu erstellen:

1. Tippen Sie im Connection Center auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Tippen Sie auf **Benutzerkonto hinzufügen**.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername**: Der Name des Benutzers, der zur Verwendung für eine Remoteverbindung gespeichert werden soll. Sie können den Benutzernamen in einem der folgenden Formate eingeben: `user_name`, `domain\user_name` oder `user_name@domain.com`.
   - **Kennwort**: Das Kennwort für den angegebenen Benutzer.
4. Tippen Sie auf **Speichern**.

Gehen Sie wie folgt vor, um ein Benutzerkonto zu löschen:

1. Tippen Sie im Connection Center auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Wählen Sie das Konto aus, das Sie löschen möchten.
3. Tippen Sie auf **Löschen**.

## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>Herstellen einer Verbindung mit einem Remotedesktopgateway zum Zugreifen auf interne Ressourcen

Mit einem Remotedesktopgateway (RD-Gateway) können Sie eine Verbindung mit einem Remotecomputer in einem Unternehmensnetzwerk über das Internet herstellen. Sie können Ihre Gateways mit dem Remotedesktopclient erstellen und verwalten.

Gehen Sie wie folgt vor, um ein neues Gateway einzurichten:

1. Tippen Sie im Connection Center auf **Einstellungen** > **Gateways**.
2. Tippe auf **Gateway hinzufügen**.
3. Geben Sie die folgenden Informationen ein:
   - **Gatewayname:** der Name des Computers, den du als Gateway verwenden möchtest. Das Gateway kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können dem Servernamen auch Portinformationen hinzufügen (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
   - **Benutzername:** der Benutzername und das Kennwort für das Remotedesktop-Gateway, mit dem du eine Verbindung herstellst. Sie können auch **Anmeldeinformationen für die Verbindung verwenden** auswählen, damit derselbe Benutzername und dasselbe Kennwort wie für die Remotedesktopverbindung verwendet werden.

## <a name="navigate-the-remote-desktop-session"></a>Navigieren in der Remotedesktopsitzung

In diesem Abschnitt werden Tools beschrieben, die die Navigation durch Ihre Remotedesktopsitzung vereinfachen.

### <a name="start-a-remote-desktop-connection"></a>Starten einer Remotedesktopverbindung

1. Tippen Sie auf die Remotedesktopverbindung, um die Remotedesktopsitzung zu starten.
2. Wenn Sie zur Überprüfung des Zertifikats für den Remotedesktop aufgefordert werden, tippen Sie auf **Annehmen**. Um die Standardeinstellung zu übernehmen, legen Sie **Nicht mehr nach Verbindungen mit diesem Computer fragen** auf **Ein** fest.

### <a name="connection-bar"></a>Verbindungsleiste

Die Verbindungsleiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente.

- **Schwenken-Steuerelement**: Mit dem Schwenken-Steuerelement kann der Bildschirm vergrößert und verschoben werden. Das Schwenken-Steuerelement ist nur mithilfe direkter Touchbewegung verfügbar.
   - Um das Schwenken-Steuerelement zu aktivieren oder zu deaktivieren, tippen Sie auf der Verbindungsleiste auf das Schwenksymbol, um das Schwenken-Steuerelement anzuzeigen. Die Anzeige wird vergrößert, während das Schwenken-Steuerelement aktiv ist. Tippen Sie auf der Verbindungsleiste erneut auf das Schwenksymbol, um das Steuerelement auszublenden und die ursprüngliche Auflösung des Bildschirms wiederherzustellen.
   - Zum Verwenden tippen und halten Sie das Schwenken-Steuerelement, und ziehen Sie gleichzeitig Ihre Finger in die Richtung, in die Sie den Bildschirm verschieben möchten.
   - Zum Verschieben des Schwenken-Steuerelements doppeltippen Sie auf das Schwenken-Steuerelement, und halten Sie es gedrückt, um es auf dem Bildschirm zu verschieben.
- **Verbindungsname**: Der aktuelle Verbindungsname wird angezeigt. Tippen Sie auf den Verbindungsnamen, um die Sitzungsauswahlleiste anzuzeigen.
- **Tastatur**: Tippen Sie auf das Tastatursymbol, um die Tastatur ein- oder auszublenden. Das Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur eingeblendet ist.
- **Verschieben der Verbindungsleiste**: Tippen und halten Sie die Verbindungsleiste, und ziehen Sie sie gleichzeitig an die neue Position. Lassen Sie die Verbindungsleiste los, um sie an der neuen Position zu platzieren.

### <a name="session-selection"></a>Sitzungsauswahl

Es können mehrere Verbindungen mit verschiedenen PCs gleichzeitig geöffnet sein. Tippen Sie auf die Verbindungsleiste, um die Sitzungsauswahlleiste auf der linken Seite des Bildschirms anzuzeigen. Mit der Sitzungsauswahlleiste können Sie Ihre geöffneten Verbindungen anzeigen und zwischen diesen wechseln.

Mit der Sitzungsauswahlleiste können Sie folgende Aktionen ausführen:

- Um zwischen Apps in einer geöffneten Remoteressourcensitzung zu wechseln, tippen Sie auf das Expander-Menü, und wählen Sie eine App aus der Liste aus.
- Tippen Sie auf **Neue Sitzung starten**, um eine neue Sitzung zu starten, und wählen Sie dann eine Sitzung aus der Liste der verfügbaren Sitzungen aus.
- Tippen Sie auf das **X**-Symbol auf der linken Seite der Sitzungskachel, um die Verbindung mit der Sitzung zu trennen.

### <a name="command-bar"></a>Befehlsleiste

Ab Version 8.0.1 wird die Utility-Leiste durch die Befehlsleiste ersetzt. Über die Befehlsleiste können Sie zwischen den Mausmodi wechseln und zum Connection Center zurückkehren.

## <a name="use-touch-gestures-and-mouse-modes-in-a-remote-session"></a>Verwenden von Touchgesten und Mausmodi in einer Remotesitzung

Der Client verwendet Standardtouchgesten. Sie können auch Touchgesten verwenden, um Mausaktionen auf dem Remotedesktop zu replizieren. Die verfügbaren Mausmodi sind in der folgenden Tabelle aufgeführt.

> [!NOTE]
> In Windows 8 oder höher werden die nativen Touchgesten im Modus für die direkte Touchbewegung unterstützt. Weitere Informationen zu Windows 8-Gesten finden Sie unter [Touchbewegung: Wischen, Tippen und vieles mehr](https://windows.microsoft.com/windows-8/touch-swipe-tap-beyond).

| Mausmodus    | Mausvorgang      | Geste                                                    |
|---------------|----------------------|------------------------------------------------------------|
| Direkte Touchbewegung  | Linksklick           | Mit einem Finger tippen                                               |
| Direkte Touchbewegung  | Klicken Sie mit der rechten Maustaste auf          | Tippen und mit einem Finger halten                                      |
| Mauszeiger | Linksklick           | Mit einem Finger tippen                                               |
| Mauszeiger | Linksklick und ziehen  | Tippen und mit einem Finger halten, dann ziehen                   |
| Mauszeiger | Klicken Sie mit der rechten Maustaste auf          | Mit zwei Fingern tippen                                              |
| Mauszeiger | Rechtsklick und ziehen | Doppeltippen und mit zwei Fingern halten, dann ziehen                    |
| Mauszeiger | Mausrad          | Doppeltippen und mit zwei Fingern halten, dann nach oben oder unten ziehen                |
| Mauszeiger | Zoom                 | Zwei Finger auseinander bewegen, um die Ansicht zu vergrößern, oder zusammenführen, um sie zu verkleinern |

## <a name="supported-input-devices"></a>Unterstützte Eingabegeräte

Der Client verfügt über [Bluetooth-Mausunterstützung](https://support.apple.com/HT210546) für iOS 13 und iPadOS als Barrierefreiheitsfeature. Für eine tiefere Integration der Maus können Sie Swiftpoint GT- oder ProPoint-Mäuse verwenden. Der Client unterstützt außerdem externe Tastaturen, die mit iOS und iPadOS kompatibel sind.

Weitere Informationen zur Geräteunterstützung findest du unter [Neuerungen beim iOS-Client](ios-whatsnew.md) und im [iOS App Store](https://aka.ms/rdios).

> [!TIP]
> Swiftpoint bietet Benutzern des iOS-Clients einen [exklusiven Rabatt für die ProPoint-Maus](https://www.swiftpoint.com/microsoft).

## <a name="use-a-keyboard-in-a-remote-session"></a>Verwenden einer Tastatur in einer Remotesitzung

Sie können in Ihrer Remotesitzung entweder eine Bildschirmtastatur oder eine physische Tastatur verwenden.

Verwenden Sie bei Bildschirmtastaturen die Schaltfläche am rechten Rand der Leiste über der Tastatur, um zwischen der Standardtastatur und der zusätzlichen Tastatur zu wechseln.

Wenn für Ihr iOS-Gerät Bluetooth aktiviert ist, wird die Bluetooth-Tastatur vom Client automatisch erkannt.

Obwohl bestimmte Tastenkombinationen in einer Remotesitzung möglicherweise nicht wie erwartet funktionieren, funktionieren viele der üblichen Windows-Tastenkombinationen, z. B. STRG+C, STRG+V und ALT+TAB.

> [!TIP]
> Fragen und Kommentare sind immer willkommen. Wenn Sie Supportanfragen oder Produktfeedback jedoch im Kommentarbereich dieses Artikels posten, können wir nicht auf Ihr Feedback reagieren. Wenn Sie Hilfe benötigen oder Probleme mit Ihrem Client beheben möchten, empfehlen wir Ihnen dringend, das [Remotedesktopclient-Forum](/answers/topics/windows-remote-desktop-client.html) zu besuchen und einen neuen Thread zu starten. Wenn Sie eine Featureempfehlung geben möchten, können Sie uns dies im [UserVoice-Forum für den Client](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android) mitteilen.