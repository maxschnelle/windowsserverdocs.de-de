---
title: Erste Schritte mit Remotedesktop für Windows
description: Basic, die Schritte für den Remotedesktop-Client für Windows einrichten.
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
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 20879507e13ac7da566c95db7b59d88e0b5d8ce8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873571"
---
# <a name="get-started-with-remote-desktop-on-windows"></a>Erste Schritte mit Remotedesktop für Windows

>Gilt für: Windows 10, Windows 8.1, Windows Server 2012 R2, WindowsServer 2016

Sie können die Remotedesktop-Client für Windows verwenden, zum Arbeiten mit Windows-apps und Desktops Remote von einem anderen Windows-Gerät.

Verwenden Sie die folgende Informationen, um zu beginnen. Achten Sie darauf, sehen Sie sich die [– häufig gestellte Fragen](remote-desktop-client-faq.md) , wenn Sie Fragen haben.

> [!NOTE]
> - Möchten Sie wissen zu den neuen Versionen der Windows-Client? Sehen Sie sich [Neuigkeiten für Remotedesktop für Windows?](windows-whatsnew.md)
> - Sie können den Client auf einer beliebigen Version von Windows 10 ausführen.

## <a name="get-the-rd-client-and-start-using-it"></a>Abrufen der Remotedesktop-Client, und es verwenden

Um mit Remotedesktop auf Ihrem Windows 10-Gerät zu beginnen, gehen Sie wie folgt vor:

1. Laden Sie die Remotedesktop-Client aus [Microsoft Store](https://www.microsoft.com/store/p/microsoft-remote-desktop/9wzdncrfj3ps). 
2. [Richten Sie Ihren PC, um Remoteverbindungen](remote-desktop-allow-access.md).
3. Fügen Sie eine Remotedesktopverbindung oder einer Remoteressource. Sie verwenden eine Verbindung aus, um direkt auf einem Windows-PC und einer Remoteressource, mit der RemoteApp-Programm, sitzungsbasierten Desktop oder virtuellen Desktops, die von Ihrem Administrator veröffentlicht eine Verbindung herstellen 
4. Heften Sie Elemente, sodass Sie schnell mit Remotedesktop zugreifen können.

### <a name="add-a-remote-desktop-connection"></a>Fügen Sie eine Remotedesktopverbindung

So erstellen Sie eine Remotedesktopverbindung hergestellt:

1. In das Connection Center Tap **+ Add**, und tippen Sie dann auf **Desktop**.
2. Geben Sie die folgende Informationen für den Computer herstellen möchten:
  - **PC-Namen** – der Name des Computers. Dies kann es sich um einen Windows-Computernamen, einen Internet-Domänennamen oder eine IP-Adresse sein. Sie können auch die Portinformationen anfügen, auf den PC-Namen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**).
  - **Benutzerkonto** – das Benutzerkonto auf einem Remotecomputer zugreifen. Tippen Sie auf **+** zum Hinzufügen eines neuen Kontos oder ein vorhandenes Konto auswählen. Sie können die folgenden Formate für den Benutzernamen verwenden: *User_name*, *Domäne\Benutzername*, oder *user_name@domain.com*. Sie können auch angeben, ob Benutzername und Kennwort beim Herstellen der Verbindung aufgefordert, dazu **Fragen jedes Mal**.
3. Sie können auch zusätzliche Optionen festlegen, durch Tippen auf **mehr anzeigen**:
  - **Anzeigename des** – ein leicht zu merkenden Namen für den PC mit dem Sie eine Verbindung mit. Sie können eine beliebige Zeichenfolge verwenden, aber der PC-Name wird angezeigt, wenn Sie einen Anzeigenamen nicht angeben, aus.
  - **Gruppe** – Geben Sie eine Gruppe aus, um Ihre Verbindungen sich später leichter wiederfinden zu erleichtern. Sie können eine neue Gruppe hinzufügen, durch Tippen auf **+** oder aus der Liste auswählen.
  - **Gateway** – die Remotedesktop-Gateway, das Sie Verbindung mit virtuellen Desktops, RemoteApp-Programmen und sitzungsbasierten Desktops in einem internen Unternehmensnetzwerk herstellen möchten. Rufen Sie Informationen über das Gateway von Ihrem Systemadministrator an.
  - **Herstellen einer Verbindung administratorensitzung mit** -mit dieser Option können Sie die Verbindung mit einer konsolensitzung, um einen Windows-Server zu verwalten.
  - **Austauschen der Maustasten** – mit dieser Option können Sie die linke Maustaste Tauschen der Schaltflächenfunktionen für die rechte Maustaste gedrückt. (Dies ist besonders nützlich, wenn der remote-PC für einen Benutzer für Linkshänder konfiguriert ist, aber Sie eine rechtshändige Maus verwenden.)
  - **Legen Sie auf meine Lösung Remotesitzung:** – wählen Sie die Auflösung, die Sie in der Sitzung verwenden möchten. **Wählen Sie für mich** wird die Auflösung basierend auf der Größe des Clients festgelegt.
  - **Ändern der Größe der Anzeige:** – Wenn Sie eine hohe statische Auflösung für die Sitzung auswählen, haben Sie die Möglichkeit, Elemente auf dem Bildschirm zur besseren Lesbarkeit größer angezeigt werden. Hinweis: Dies gilt nur, wenn Verbindungen mit Windows 8.1 oder höher herstellen.
  - **Aktualisieren Sie die Remotesitzung Auflösung beim Ändern der Größe** – Wenn aktiviert, wird der Client dynamisch die Sitzung Auflösung basierend auf der Größe des Clients aktualisieren. Hinweis: Dies gilt nur, wenn Verbindungen mit Windows 8.1 oder höher herstellen.
  - **Zwischenablage** – Wenn aktiviert, können Sie Text kopieren und Bilder in und aus dem remote-PC,.
  - **Audiowiedergabe** – wählen Sie das Gerät für Audio während der Remotesitzung verwenden. Sie können auswählen, um auf den lokalen Geräten, die remote-PC oder überhaupt nicht Systemsound wiederzugeben.
  - **Audio-Aufzeichnung** – Wenn aktiviert, können Sie mit einem lokalen Mikrofon mit Anwendungen auf einem Remotecomputer,.
4. Tippen Sie auf **speichern**.

Möchten Sie diese Einstellungen zu bearbeiten? Tippen Sie auf das Menü "Überlauf" (**...** ) neben dem Namen der Desktop, und tippen Sie anschließend auf **bearbeiten**.

Möchten Sie die Verbindung löschen? Tippen Sie in diesem Fall auf das Menü "Überlauf" (**...** ), und tippen Sie dann auf **entfernen**.

### <a name="add-a-remote-resource"></a>Hinzufügen einer Remoteressource
Remote-Ressourcen sind die RemoteApp-Programme, sitzungsbasierte Desktops und virtuellen Desktops, die von Ihrem Administrator mit Remote Desktop Services veröffentlicht.

So fügen Sie eine Remoteressource hinzu:

1. Tippen Sie auf dem Bildschirm "Connection Center" auf **+ Add**, und tippen Sie dann auf **Remoteressourcen**. 
2. Geben Sie die **Feed-URL** bereitgestellt werden, indem Sie Ihren Administrator, und tippen Sie auf **finden des Feeds**.
3. Geben Sie bei Aufforderung die Anmeldeinformationen zu verwenden, um den Feed abonnieren.

Der remote-Ressourcen werden im Connection Center angezeigt.


So löschen Sie die remote-Ressourcen:

1. Tippen Sie in das Connection Center, auf das Überlaufmenü (**...** ) neben der Remoteressource.
2. Tippen Sie auf **entfernen**.

### <a name="pin-a-saved-desktop-to-your-start-menu"></a>Einen gespeicherten Desktop an Ihr Startmenü anheften

Um eine Verbindung mit Ihrem Menü "Start" anheften möchten, tippen Sie auf das Überlaufmenü (**...** ) neben dem Namen der Desktop, und tippen Sie anschließend auf **an Startmenü anheften**.

Jetzt können Sie die Remotedesktopverbindung direkt vom Startmenü starten, durch Tippen.

## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>Verbinden Sie mit einem RD-Gateway auf interne Ressourcen zugreifen

Ein Remotedesktopgateway (RD-Gateway) können Sie die Verbindung mit einem Remotecomputer in einem Unternehmensnetzwerk von überall aus im Internet. Sie können erstellen und verwalten Ihre Gateways mit dem Remotedesktop-Client.

So richten ein neues Gateway:

1. Tippen Sie in das Connection Center, auf **Einstellungen**.
2. Tippen Sie neben dem Gateway auf **+** zum Hinzufügen eines neuen Gateways. Hinweis: Ein Gateway kann auch hinzugefügt werden, wenn Sie eine neue Verbindung hinzufügen.
3. Geben Sie die folgende Informationen ein:
  - **Servername** – der Name des Computers als Gateway verwenden möchten. Dies kann es sich um einen Windows-Computernamen, einen Internet-Domänennamen oder eine IP-Adresse sein. Sie können auch Informationen hinzufügen, um den Namen des Servers (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
  - **Benutzerkonto** – wählen oder ein Benutzerkonto mit dem Remotedesktop-Gateway verwenden Sie eine Verbindung mit hinzufügen. Sie können auch auswählen, **Remotedesktop-Benutzerkonto verwenden** auf die gleichen Anmeldeinformationen wie für die Remotedesktopverbindung verwenden.
4. Tippen Sie auf **speichern**.  

## <a name="global-app-settings"></a>Globale app-Einstellungen

Sie können die folgenden globalen Einstellungen in Ihrem Client festlegen, durch Tippen auf **Einstellungen**:

VERWALTET ELEMENTE
- **Benutzerkonto** – ermöglicht das Hinzufügen, bearbeiten und Löschen von Benutzerkonten, die auf dem Client gespeichert. Dies ist eine gute Möglichkeit, aktualisieren Sie das Kennwort für ein Konto aus, nachdem es geändert wurde.
- **Gateway** – ermöglicht das Hinzufügen, bearbeiten und Löschen von Gatewayservern, die auf dem Client gespeichert.
- **Gruppe** – ermöglicht das Hinzufügen, bearbeiten und Löschen von Gruppen, die auf dem Client gespeichert. Diese können Sie problemlos Verbindungen mit gruppieren.

SITZUNGSEINSTELLUNGEN
- **Starten Sie die Verbindungen im Vollbildmodus** – Wenn aktiviert, jedes Mal, wenn eine Verbindung gestartet wird, verwendet der Client den gesamten Bildschirm des aktuellen Bildschirms.
- **Starten Sie jede Verbindung in einem neuen Fenster** – Wenn aktiviert, jede Verbindung gestartet wird in einem separaten Fenster, sodass Sie auf unterschiedlichen Bildschirmen platzieren, und wechseln Sie zwischen der Taskleiste.
- **Wenn die app Ändern der Größe:** -können Sie steuern, was geschieht, wenn der Client-Fenster geändert wird. Standardmäßig **dehnen Sie den Inhalt unter Beibehaltung des Seitenverhältnisses**.
- **Verwenden von Tastenkombinationen mit:** -dient zum angeben, wo Tastaturbefehle *gewinnen* oder *ALT + TAB* verwendet werden. Der Standardwert ist für das nur für die Sitzung versenden Wenn sich die Verbindung im Vollbild befindet.
- **Verhindern, dass den Bildschirm Timeout** -können Sie verhindern, den Bildschirm ablaufen, wenn eine Sitzung aktiv ist. Dies ist hilfreich, wenn die Verbindung für längere Zeit keine Eingreifen erfordert.

APP-EINSTELLUNGEN
- **Anzeigen der Vorschau von Desktop** -können Sie eine Vorschau der Desktop im Connection Center anzeigen, bevor Sie eine Verbindung damit herstellen. Standardmäßig ist dies festgelegt auf **auf**.
- **Verbessern Sie Remotedesktop** -anonyme Daten an Microsoft gesendet. Wir verwenden diese Daten, um den Client zu verbessern. Informationen dazu, wie wir diese anonyme, privaten Daten behandeln, finden Sie unter den [Microsoft Privacy Statement](https://privacy.microsoft.com/en-us/privacystatement). Diese Einstellung ist standardmäßig **auf**.

### <a name="manage-your-user-accounts"></a>Verwalten Sie Ihre Benutzerkonten

Wenn Sie auf einem Desktop- oder remote-Ressourcen verbinden, können Sie die Benutzerkonten erneut aus speichern. Sie können auch die Benutzerkonten definieren, auf dem Client selbst, im Gegensatz zu die Benutzerdaten speichern, bei der Herstellung einer Verbindung mit eines Desktops.

So erstellen Sie ein neues Benutzerkonto:

1. Tippen Sie in das Connection Center, auf **Einstellungen**.
2. Tippen Sie neben dem Benutzerkonto an, auf **+** ein neues Benutzerkonto hinzufügen.
3. Geben Sie die folgende Informationen ein:
   - **Benutzername** -der Name des Benutzers, der für die Verwendung mit einer remote-Verbindung zu speichern. Sie können den Benutzernamen eingeben, in einem der folgenden Formate: Domäne\Benutzername, User_name oder user_name@domain.com.
   - **Kennwort** -das Kennwort für den Benutzer, die Sie angegeben haben. Dies kann zur Kennworteingabe aufgefordert werden, während der Verbindung leer sein.
4. Tippen Sie auf **speichern**.

So löschen Sie ein Benutzerkonto

1. Tippen Sie in das Connection Center, auf **Einstellungen**.
2. Wählen Sie das Konto aus der Liste unter dem Benutzerkonto zu löschen.
3. Tippen Sie neben dem Benutzerkonto an auf das Symbol "Bearbeiten".
4. Tippen Sie auf **dieses Konto entfernen** unten, um das Benutzerkonto zu löschen.
5. Sie können auch das Benutzerkonto, das Bearbeiten, und tippen Sie auf **speichern**.

## <a name="navigate-the-remote-desktop-session"></a>Navigieren Sie von der Remotedesktopsitzung
Wenn Sie eine Remotedesktopverbindung starten, gibt es Tools zur Verfügung, Sie verwenden können, um die Sitzung zu navigieren.

### <a name="start-a-remote-desktop-connection"></a>Starten Sie eine Remotedesktopverbindung

1. Tippen Sie auf die Remotedesktop-Verbindung, um die Sitzung zu starten.
2. Wenn Sie Anmeldeinformationen für die Verbindung nicht gespeichert haben, werden Sie aufgefordert, geben Sie einen **Benutzername** und **Kennwort**.
3. Wenn Sie aufgefordert werden, um zu überprüfen, ob das Zertifikat für den Remotedesktop, überprüfen Sie die Informationen und sicherzustellen, dass dies einen PC mit dem Sie vertrauen können, bevor auf **Connect**. Sie können auch auswählen, **nicht mehr nachfragen zu diesem Zertifikat** dieses Zertifikat immer akzeptieren.

### <a name="connection-bar"></a>Verbindungsleiste

Die Verbindung Leiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente. Standardmäßig wird die Symbolleiste Verbindung in der Mitte am oberen Rand des Bildschirms platziert. Tippen Sie auf, und ziehen Sie die Leiste links oder rechts zu verschieben.

- **Schwenken-Steuerelement** -das Pan-Steuerelement ermöglicht den Bildschirm vergrößert und verschoben werden. Beachten Sie, dass Pan-Steuerelement nur für Touch-fähigen Geräten und mit den direkten fingereingabemodus verfügbar ist.
   - Aktivieren Sie bzw. deaktivieren Sie die Pan-Steuerelement: Tippen Sie auf das schwenksymbol, in der Verbindungsleiste "zum Anzeigen des Steuerelements Schwenken und vergrößern den Bildschirm. Tippen Sie auf das schwenksymbol in die Symbolleiste für die Verbindung erneut aus, um das Steuerelement wird ausgeblendet, und den Bildschirm an seiner ursprünglichen Auflösung zurückgeben.
   - Verwenden Sie die Pan-Steuerelement - Tippen Sie auf halten Sie das Schwenken STRG gedrückt und ziehen Sie dann in die Richtung auf den Bildschirm verschoben werden soll.
   - Verschieben Sie die Pan-Steuerelement - Doppeltippen, und halten Sie die Pan-Steuerelement auf das Steuerelement auf dem Bildschirm verschoben werden.
- **Zusätzliche Optionen** – Tippen Sie auf das zusätzliche Optionen-Symbol, um die Sitzung-Auswahl und Balken (siehe unten) angezeigt.
- **Tastatur** – Tippen Sie auf das Symbol "Tastatur" zum Anzeigen oder Ausblenden der Tastatur auf dem Bildschirm. Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur angezeigt wird.

### <a name="command-bar"></a>Befehlsleiste

Tippen Sie auf die **...**  auf der Verbindungsleiste "auf die Befehlsleiste auf der rechten Seite des Bildschirms angezeigt.

- **Startseite** -mithilfe der Schaltfläche "Home" zum Connection Center auf der Befehlszeile zurück.
  - Alternativ können Sie die Schaltfläche "zurück" für die gleiche Aktion verwenden.
  - Ihre aktive Sitzung werden nicht getrennt werden.
  - Dadurch können Sie zusätzliche Verbindungen zu starten.
- **Disconnect** -verwenden Sie die Schaltfläche "Trennen", um die Verbindung zu beenden.
  - Ihre apps bleibt aktiv, solange die Sitzung nicht auf einem Remotecomputer beendet wird.
- **Vollbild-** : eingibt, oder den Vollbildmodus zu beenden.
- **Touch / mit der Maus** – Sie können zwischen den Modi für Maus (Direct Touch und Mauszeiger) wechseln.

### <a name="use-direct-touch-gestures-and-mouse-modes-in-a-remote-session"></a>Verwenden von direkten touch-Gesten und Maus-Modi in einer Remotesitzung

Zwei Modi der Maus sind für die Interaktion mit der Sitzung verfügbar.
- **Leiten Sie Touch**: Übergibt alle die Fingereingabekontakte für die Sitzung Remote interpretiert werden soll.
  - Wird verwendet, auf die gleiche Weise, die Sie Windows mit einem Touchscreen verwenden würden.
- **Mauszeiger**: Transformiert Ihre lokalen Touchscreen, in einer großen Touchpad ermöglicht, ein Mauszeiger in der Sitzung.
  - Wird verwendet, auf die gleiche Weise, die Sie nach Windows mit einem Touchpad verwenden würden.

> [!NOTE]
> Interaktion mit Windows 8 oder höher werden die systemeigenen Touchgesten in Direct Touch-Modus unterstützt. 

| Mausmodus    | Mausvorgang      | Geste                                                               |
|---------------|----------------------|-----------------------------------------------------------------------|
| Direct touch  | Linksklick           | 1 Finger tap                                                          |
| Direct touch  | Rechtsklick          | 1 Finger tippen und halten                                                 |
| Mauszeiger | Linksklick           | 1 Finger tap                                                          |
| Mauszeiger | Linksklick und ziehen  | Doppeltippen 1 Finger, und halten, ziehen Sie dann                               |
| Mauszeiger | Rechtsklick          | 2 Finger tap                                                          |
| Mauszeiger | Rechtsklick und ziehen | 2 Finger Doppeltippen und halten, ziehen Sie dann                               |
| Mauszeiger | Mausrad          | 2 Finger tippen und halten, und ziehen Sie dann nach oben oder unten                           |
| Mauszeiger | Zoom                 | Verwenden Sie 2 Finger, und zwei-Finger-vergrößern oder verschieben Finger voneinander entfernt sind, können Sie das Objekt. |

> [!TIP]
> Fragen und Kommentare sind immer Willkommen. Allerdings Supportfragen Sie keine Anforderung für die Hilfe zur Problembehandlung, indem Sie über die Kommentarfunktion am Ende dieses Artikels. Wechseln Sie stattdessen zu den [Remotedesktop-Client-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc) und einen neuen Thread starten. Haben Sie Vorschläge Feature? Teilen Sie uns mit den [Feedback Hub](feedback-hub://?tabid=2&contextid=605).
