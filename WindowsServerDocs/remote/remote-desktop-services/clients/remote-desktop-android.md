---
title: Erste Schritte mit Remotedesktop unter Android
description: Basic richten Sie die Schritte für den Remotedesktopclient für Android ein.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64f038e1-40ec-4c67-938b-72edea49e5d8
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 07/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 41f8b511453143bb6239de6cdb369ebe8a307aec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885851"
---
# <a name="get-started-with-remote-desktop-on-android"></a>Erste Schritte mit Remotedesktop unter Android

>Gilt für: Windows 10, Windows 8.1, Windows Server 2012 R2, WindowsServer 2016

Sie können den Remotedesktopclient für Android verwenden, zum Arbeiten mit Windows-apps und Desktops direkt über Ihr Android-Gerät.

Verwenden Sie die folgende Informationen, um zu beginnen. Achten Sie darauf, sehen Sie sich die [– häufig gestellte Fragen](remote-desktop-client-faq.md) , wenn Sie Fragen haben.

> [!NOTE]
> - Möchten Sie wissen zu den neuen Versionen für den Android-Client? Sehen Sie sich [Neuigkeiten für Remotedesktop unter Android?](android-whatsnew.md)
> Sie können den Client ausführen, unter Android 4.1 und neueren Geräten sowie auf Chromebooks mit ChromeOS 53 installiert. Weitere Informationen zu Android-Anwendungen in Chrome [hier](https://sites.google.com/a/chromium.org/dev/chromium-os/chrome-os-systems-supporting-android-apps).

## <a name="get-the-rd-client-and-start-using-it"></a>Abrufen der Remotedesktop-Client, und es verwenden

Um mit Remotedesktop auf Ihrem Android-Gerät zu beginnen, gehen Sie wie folgt vor:

1. Laden Sie die Remotedesktop-Client aus [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android). 
2. [Richten Sie Ihren PC, um Remoteverbindungen](remote-desktop-allow-access.md).
3. Fügen Sie eine Remotedesktopverbindung oder einer Remoteressource. Können Sie eine Verbindung direkt mit einem Windows-PC und einer Remoteressource, verwenden Sie ein RemoteApp-Programms, sitzungsbasierten Desktops herstellen, oder virtueller Desktop veröffentlicht lokal. 
4. Erstellen Sie ein Widget, sodass Sie schnell mit Remotedesktop zugreifen können.

> [!NOTE]
> Wenn Sie neue Features bereits flight möchten empfehlen wir die herunterladen unsere [Microsoft Remote Desktop Beta](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android.beta) Anwendung aus dem Google Play Store. 

### <a name="add-a-remote-desktop-connection"></a>Fügen Sie eine Remotedesktopverbindung

So erstellen Sie eine Remotedesktopverbindung hergestellt:

1. In das Connection Center Tap **+**, und tippen Sie dann auf **Desktop**.
2. Geben Sie die folgende Informationen für den Computer herstellen möchten:
  - **PC-Namen** – der Name des Computers. Dies kann es sich um einen Windows-Computernamen, einen Internet-Domänennamen oder eine IP-Adresse sein. Sie können auch die Portinformationen anfügen, auf den PC-Namen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**).
  - **Benutzername** – den Benutzernamen ein, die auf einem Remotecomputer verwenden. Sie können die folgenden Formate verwenden: *User_name*, *Domäne\Benutzername*, oder *user_name@domain.com*. Sie können auch angeben, ob Benutzername und Kennwort aufgefordert.
3. Sie können auch die folgenden zusätzlichen Optionen festlegen:
  - **Anzeigename des** – ein leicht zu merkenden Namen für den PC mit dem Sie eine Verbindung mit. Sie können eine beliebige Zeichenfolge verwenden, aber der PC-Name wird angezeigt, wenn Sie einen Anzeigenamen nicht angeben, aus.
  - **Gateway** – die Remotedesktop-Gateway, das Sie Verbindung mit virtuellen Desktops, RemoteApp-Programmen und sitzungsbasierten Desktops in einem internen Unternehmensnetzwerk herstellen möchten. Rufen Sie Informationen über das Gateway von Ihrem Systemadministrator an.
    Möchten Sie ein Remotedesktop-Gateway konfigurieren?
  - **Sound** – wählen Sie das Gerät für Audio während der Remotesitzung verwenden. Sie können auswählen, um auf den lokalen Geräten, dem Remotegerät oder überhaupt nicht Systemsound wiederzugeben.
  - **Anpassen der Bildschirmauflösung** -legen Sie eine benutzerdefinierte Lösung für eine Verbindung durch die Aktivierung dieser Einstellung. Wenn aus der Lösung angewendet wird die Sie in den globalen Einstellungen der app definiert haben.
  - **Austauschen der Maustasten** – mit dieser Option können Sie die linke Maustaste Tauschen der Schaltflächenfunktionen für die rechte Maustaste gedrückt. (Dies ist besonders nützlich, wenn der remote-PC für einen Benutzer für Linkshänder konfiguriert ist, aber Sie eine rechtshändige Maus verwenden.)
  - **Herstellen einer Verbindung administratorensitzung mit** -mit dieser Option können Sie die Verbindung mit einer konsolensitzung, um einen Windows-Server zu verwalten.
  - **In den lokalen Speicher umleiten** – hängt von Ihren lokalen Speicher als remote-Dateisystem auf dem remote-PC.
4. Tippen Sie auf **speichern**.

Möchten Sie diese Einstellungen zu bearbeiten? Tippen Sie auf das Menü "Überlauf" (**...** ) neben dem Namen der Desktop, und tippen Sie anschließend auf **bearbeiten**.

Möchten Sie die Verbindung löschen? Tippen Sie in diesem Fall auf das Menü "Überlauf" (**...** ), und tippen Sie dann auf **entfernen**.

>[!TIP]
> Wenn Sie 0xf07 Fehlermeldung zu ein falschen Kennworts ("Wir konnten nicht auf einem Remotecomputer Verbinden mit dem Benutzerkonto das Kennwort ist abgelaufen"), Ändern des Kennworts, und versuchen Sie es erneut.

### <a name="add-a-remote-resource"></a>Hinzufügen einer Remoteressource
Remote-Ressourcen sind die RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops mithilfe der RemoteApp- und Desktopverbindungen veröffentlicht.

So fügen Sie eine Remoteressource hinzu:

1. Tippen Sie auf dem Bildschirm "Connection Center" auf **+**, und tippen Sie dann auf **Remote Ressourcen Feed**. 
2. Geben Sie Informationen für die Remoteressource:
   - **E-Mail-Adresse oder URL** -die URL der Web Access für Remotedesktop-Server. Ihr Unternehmens-e-Mail-Konto auch in dieses Feld eingegeben werden können, weist diese den Client, suchen Sie für den RD-Web-Server Ihre e-Mail-Adresse zugeordnet.
   - **Benutzername** -den Benutzernamen ein, für den Web Access für Remotedesktop-Server verwenden Sie eine Verbindung herstellen.
   - **Kennwort** -das Kennwort für den Web Access für Remotedesktop-Server hergestellt.
3. Tippen Sie auf **speichern**.

Der remote-Ressourcen werden im Connection Center angezeigt.


So löschen Sie die remote-Ressourcen:

1. Tippen Sie in das Connection Center, auf das Überlaufmenü (**...** ) neben der Remoteressource.
2. Tippen Sie auf **entfernen**.
3. Bestätigen Sie den Vorgang.

### <a name="widgets--pin-a-saved-desktop-to-your-home-screen"></a>Widgets – Pin einen gespeicherten Desktop an den Startbildschirm

Die Remote Desktop-Anwendungen unterstützen feste Verbindungen an den Startbildschirm mit der Android-Widget-Funktion. Die Möglichkeit, dass Sie ein Widget hinzufügen, hängt von den Typ des verwendeten Android-Gerät und dem Betriebssystem ab. Hier ist die gängigste Methode zum Hinzufügen eines Gadgets: 

1. Tippen Sie auf **apps** um das Menü apps zu starten.
2. Tippen Sie auf **Widgets**.
3. Navigieren Sie über die Widgets, und suchen Sie nach der Remotedesktop-Symbol, mit der Beschreibung, "Pin Remote Desktop".
4. Tippen Sie auf halten Sie, Remote Desktop-Widget und verschieben Sie es auf dem Startbildschirm.
5. Wenn Sie das Symbol loslassen, sehen Sie die gespeicherten Remotedesktops. Wählen Sie die Verbindung, die an den Startbildschirm gespeichert werden soll.

Jetzt können Sie die Remotedesktopverbindung direkt auf dem Startbildschirm zunächst tippen.

> [!NOTE]
> Wenn Sie die Remotedesktop-Verbindung in der Remote Desktop-Anwendung umbenennen, wird die Bezeichnung des diesem angehefteten Remotedesktop nicht aktualisiert werden.

## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>Verbinden Sie mit einem RD-Gateway auf interne Ressourcen zugreifen

Ein Remotedesktopgateway (RD-Gateway) können Sie die Verbindung mit einem Remotecomputer in einem Unternehmensnetzwerk von überall aus im Internet. Sie können erstellen und verwalten Ihre Gateways mit dem Remotedesktop-Client.

So richten ein neues Gateway:

1. Tippen Sie in das Connection Center, auf **Einstellungen > Gateways**. Tippen Sie auf **+** zum Hinzufügen eines neuen Gateways.
2. Geben Sie die folgende Informationen ein:
  - **Servername** – der Name des Computers als Gateway verwenden möchten. Dies kann es sich um einen Windows-Computernamen, einen Internet-Domänennamen oder eine IP-Adresse sein. Sie können auch Informationen hinzufügen, um den Namen des Servers (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
  - **Benutzername** -den Benutzernamen und Kennwort ein, das für das Remotedesktopgateway hergestellt. Sie können auch auswählen, **Remotedesktop-Benutzerkonto verwenden** auf die gleichen Anmeldeinformationen wie für die Remotedesktopverbindung verwenden.

## <a name="manage-your-user-accounts"></a>Verwalten Sie Ihre Benutzerkonten

Wenn Sie auf einem Desktop- oder remote-Ressourcen verbinden, können Sie die Benutzerkonten erneut aus speichern. Sie können auch die Benutzerkonten definieren, auf dem Client selbst, im Gegensatz zu die Benutzerdaten speichern, bei der Herstellung einer Verbindung mit eines Desktops.

So erstellen Sie ein neues Benutzerkonto:

1. Tippen Sie in das Connection Center, auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Tippen Sie auf **+** ein neues Benutzerkonto hinzufügen.
3. Geben Sie die folgende Informationen ein:
   - **Benutzername** -der Name des Benutzers, der für die Verwendung mit einer remote-Verbindung zu speichern. Sie können den Benutzernamen eingeben, in einem der folgenden Formate: Domäne\Benutzername, User_name oder user_name@domain.com.
   - **Kennwort** -das Kennwort für den Benutzer, die Sie angegeben haben. Jedes Benutzerkonto, das Sie speichern, um für Remoteverbindungen verwenden möchten, muss ein Kennwort zugeordnet.
4. Tippen Sie auf **speichern**.

So löschen Sie ein Benutzerkonto

1. Tippen Sie in das Connection Center, auf **Einstellungen > Benutzerkonten**.
2. Tippen Sie und halten Sie ein Benutzerkonto in der Liste aus, um es auszuwählen. Sie können mehrere Benutzer auswählen.
3. Tippen Sie auf das Papierkorb-kann zum Löschen des ausgewählten Benutzers.

## <a name="navigate-the-remote-desktop-session"></a>Navigieren Sie von der Remotedesktopsitzung
Wenn Sie eine Remotedesktopverbindung starten, gibt es Tools zur Verfügung, Sie verwenden können, um die Sitzung zu navigieren.

### <a name="start-a-remote-desktop-connection"></a>Starten Sie eine Remotedesktopverbindung

1. Tippen Sie auf die Remotedesktop-Verbindung, um die Sitzung zu starten. 
2. Wenn Sie aufgefordert werden, um zu überprüfen, ob das Zertifikat für den Remotedesktop, tippen Sie auf **Connect**. Sie können auch auswählen, **nicht mehr nachfragen für Verbindungen mit diesem Computer** , immer das Zertifikat zu akzeptieren.

### <a name="manage-global-app-settings"></a>Globale app-Einstellungen verwalten

Sie können die folgenden globalen Einstellungen in Ihrer Android-Client festlegen:

- **Anzeigen der Vorschau von Desktop** -können Sie eine Vorschau der Desktop im Connection Center anzeigen, bevor Sie eine Verbindung damit herstellen. Standardmäßig ist dies festgelegt auf **auf**.
- **Zum Zoomen zusammendrücken** -können Sie die Pinch-Finger-Zoom-Gesten verwenden. Diese Einstellung aktivieren, wenn die app, die Sie über Remotedesktop verwenden Multitouch (eingeführt in Windows 8) unterstützt, **aus**.
- **Hilfe zur Verbesserung der Remotedesktop** -anonyme Daten an Microsoft gesendet. Wir verwenden diese Daten, um den Client zu verbessern. Sie können weitere Informationen dazu, wie wir diese anonyme, privaten Daten behandeln, finden Sie unter den [Remote Desktop-Client-Datenschutzbestimmungen](https://www.microsoft.com/privacystatement/RemoteApp/Default.aspx). Diese Einstellung ist standardmäßig **auf**.
- **Anzeige** – es gibt zwei globale Einstellungen für die Anzeige:
   - **Ausrichtung** -legt die bevorzugte Ausrichtung (Querformat oder Hochformat) für die Sitzung fest. 
   >[!NOTE]
   > Wenn Sie mit einem mit Windows 8 oder eine ältere Version von Windows-PC verbinden, wird die Sitzung wird nicht ordnungsgemäß skaliert. Die beste Lösung ist der PC trennen, und klicken Sie dann erneut eine Verbindung herzustellen, in die Ausrichtung, die Sie verwenden möchten. Eine noch bessere Möglichkeit ist auf den PC über mindestens ein upgrade von Windows 8.1.

   - **Auflösung** -bestimmt die Auflösung, die global für desktop-Verbindungen verwenden möchten. Wenn Sie eine benutzerdefinierte Lösung für eine einzelne app oder die Verbindung bereits eingerichtet haben, wird nicht mit dieser Einstellung, die nicht ändern.
   >[!NOTE]
   >Wenn Sie eine der Anzeigeeinstellungen ändern, gelten nur für neue Verbindungen von diesem Zeitpunkt auf. Damit die Änderung in einer Sitzung angezeigt, die Sie bereits verbunden sind, um zu trennen, und klicken Sie dann erneut eine Verbindung her.

### <a name="connection-bar"></a>Verbindungsleiste

Die Verbindung Leiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente. Standardmäßig wird die Symbolleiste Verbindung in der Mitte am oberen Rand des Bildschirms platziert. Doppeltippen Sie auf ein, und ziehen Sie die Leiste links oder rechts zu verschieben.

- **Schwenken-Steuerelement**: Das Schwenksteuerelement ermöglicht es sich um den Bildschirm vergrößert und verschoben werden. Beachten Sie, dass Pan-Steuerelement ist nur verfügbar, die mithilfe von direkten Touch.
   - Aktivieren Sie bzw. deaktivieren Sie die Pan-Steuerelement: Tippen Sie auf das schwenksymbol, in der Verbindungsleiste "zum Anzeigen des Steuerelements Schwenken und vergrößern den Bildschirm. Tippen Sie auf das schwenksymbol in die Symbolleiste für die Verbindung erneut aus, um das Steuerelement wird ausgeblendet, und den Bildschirm an seiner ursprünglichen Auflösung zurückgeben.
   - Verwenden Sie die Pan-Steuerelement: Tippen Sie auf halten Sie das Schwenken STRG gedrückt und ziehen Sie dann in die Richtung auf den Bildschirm verschoben werden soll.
   - Verschieben Sie die Pan-Steuerelement: Doppelte Tippen Sie und halten Sie die Pan-Steuerelement auf das Steuerelement auf dem Bildschirm verschoben werden.
- **Zusätzliche Optionen**: Tippen Sie auf das zusätzliche Optionen-Symbol, um die Sitzung-Auswahl und Balken (siehe unten) angezeigt.
- **Tastatur**: Tippen Sie auf das Symbol "Tastatur" zum Anzeigen oder Ausblenden der Tastaturfokus. Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur angezeigt wird.
- **Verschieben Sie die Symbolleiste Verbindung**: Tippen Sie auf und enthalten Verbindungsleiste, und klicken Sie dann Drag & drop an eine neue Position am oberen Rand des Bildschirms.


### <a name="command-bar"></a>Befehlsleiste

Tippen Sie auf die Symbolleiste für die Verbindung zum Anzeigen der Befehlsleiste auf der rechten Seite des Bildschirms. Sie können zwischen den Modi für Maus (Direct Touch und Mauszeiger) wechseln. Verwenden Sie die Schaltfläche "Start", um auf das Connection Center auf der Befehlsleiste zurückzugeben. Alternativ können Sie die Schaltfläche "zurück" für die gleiche Aktion verwenden. Ihre aktive Sitzung werden nicht getrennt werden. 


### <a name="use-direct-touch-gestures-and-mouse-modes-in-a-remote-session"></a>Verwenden von direkten touch-Gesten und Maus-Modi in einer Remotesitzung

Der Client verwendet die standard Touchgesten. Sie können auch Touchgesten verwenden, um Aktionen auf dem Remotedesktop zu replizieren. Die Mauszeiger-Modi zur Verfügung, werden in der folgenden Tabelle definiert.

> [!NOTE]
> Interaktion mit Windows 8 oder höher werden die systemeigenen Touchgesten in Direct Touch-Modus unterstützt. 

| Mausmodus    | Mausvorgang      | Geste                                                               |
|---------------|----------------------|-----------------------------------------------------------------------|
| Direct touch  | Linksklick           | 1 Finger tap                                                          |
| Direct touch  | Rechtsklick          | 1 Finger tippen und halten                                                 |
| Mauszeiger | Zoom                 | Verwenden Sie 2 Finger, und zwei-Finger-vergrößern oder verschieben Finger voneinander entfernt sind, können Sie das Objekt. |
| Mauszeiger | Linksklick           | 1 Finger tap                                                          |
| Mauszeiger | Linksklick und ziehen  | Doppeltippen 1 Finger, und halten, ziehen Sie dann                               |
| Mauszeiger | Rechtsklick          | 2 Finger tap                                                          |
| Mauszeiger | Rechtsklick und ziehen | 2 Finger Doppeltippen und halten, ziehen Sie dann                               |
| Mauszeiger | Mausrad          | 2 Finger tippen und halten, und ziehen Sie dann nach oben oder unten                           |

> [!TIP]
> Fragen und Kommentare sind immer Willkommen. Allerdings Supportfragen Sie keine Anforderung für die Hilfe zur Problembehandlung, indem Sie über die Kommentarfunktion am Ende dieses Artikels. Wechseln Sie stattdessen zu den [Remotedesktop-Client-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc) und einen neuen Thread starten. Haben Sie Vorschläge Feature? Teilen Sie uns in die [Client User Voice-Forum](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android).
