---
title: Erste Schritte mit dem Android-Client
description: Hier finden Sie grundlegende Einrichtungsschritte für den Remotedesktopclient für Android.
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
ms.date: 08/27/2019
ms.localizationpriority: medium
ms.openlocfilehash: ccc96013efb71a2403f9be2df03461eba5ff1fc1
ms.sourcegitcommit: 51eaab0f860312d97293fd90f3e632e7caee3df1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/29/2019
ms.locfileid: "70151010"
---
# <a name="get-started-with-the-android-client"></a>Erste Schritte mit dem Android-Client

>Gilt für: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Sie können den Remotedesktopclient für Android verwenden, um direkt mit Windows-Apps und -Desktops auf Ihrem Android-Gerät zu arbeiten.

Verwenden Sie die folgenden Informationen für die ersten Schritte. Lesen Sie unbedingt die [häufig gestellten Fragen](remote-desktop-client-faq.md), wenn Sie Fragen haben.

> [!NOTE]
> - Möchten Sie mehr über die neuen Versionen für den Android-Client erfahren? Lesen Sie [Neuerungen bei Remotedesktop unter Android](android-whatsnew.md).
> Sie können den Client auf Geräten unter Android 4.1 und höher sowie auf Chromebooks unter Chrome OS 53 ausführen. Weitere Informationen zu Android-Anwendungen für Chrome finden Sie [hier](https://sites.google.com/a/chromium.org/dev/chromium-os/chrome-os-systems-supporting-android-apps).

## <a name="get-the-rd-client-and-start-using-it"></a>Abrufen des Remotedesktopclients und Ausführen der ersten Schritte

Führen Sie die folgenden Schritte für den Einstieg in Remotedesktop auf Ihrem Android-Gerät aus:

1. Laden Sie den Remotedesktopclient von [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android) herunter. 
2. [Richten Sie Ihren PC so ein, dass Remoteverbindungen zulässig sind](remote-desktop-allow-access.md).
3. Fügen Sie eine Remotedesktopverbindung oder eine Remoteressource hinzu. Mit einer Verbindung können Sie eine direkte Verbindung mit einem Windows-PC herstellen, und mit einer Remoteressource können Sie ein RemoteApp-Programm, einen sitzungsbasierten Desktop oder einen virtuellen Desktop (lokale Veröffentlichung) verwenden. 
4. Erstellen Sie ein Widget, damit Sie schnell auf Remotedesktop zugreifen können.

> [!NOTE]
> Wenn Sie neue Features früher (Flight) nutzen möchten, empfehlen wir Ihnen, unsere Anwendung [Microsoft Remote Desktop Beta](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android.beta) aus dem Google Play Store herunterzuladen. 

### <a name="add-a-remote-desktop-connection"></a>Hinzufügen einer Remotedesktopverbindung

Gehen Sie wie folgt vor, um eine Remotedesktopverbindung zu erstellen:

1. Tippen Sie im Connection Center auf das Pluszeichen ( **+** ), und tippen Sie dann auf **Desktop**.
2. Geben Sie die folgenden Informationen für den Computer ein, mit dem Sie eine Verbindung herstellen möchten:
   - **PC-Name**: Der Name des Computers. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können auch Portinformationen an den PC-Namen anfügen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**).
   - **Benutzername**: Der Benutzername, der für den Zugriff auf den Remotecomputer verwendet werden soll. Sie können die folgenden Formate verwenden: *Benutzername*, *Domäne\Benutzername* oder <em>user_name@domain.com</em>. Sie können auch angeben, ob der Benutzer zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden soll.
3. Sie können auch die folgenden zusätzlichen Optionen festlegen:
   - **Anzeigename**: Ein leicht zu merkender Name für den PC, mit dem Sie eine Verbindung herstellen. Sie können eine beliebige Zeichenfolge verwenden, aber wenn Sie keinen Anzeigenamen angeben, wird der PC-Name angezeigt.
   - **Gateway**: Das Remotedesktopgateway, das Sie zum Herstellen einer Verbindung mit virtuellen Desktops, RemoteApp-Programmen und sitzungsbasierten Desktops in einem internen Unternehmensnetzwerk verwenden möchten. Sie erhalten die Informationen über das Gateway von Ihrem Systemadministrator.
    Müssen Sie ein Remotedesktopgateway konfigurieren?
   - **Sound**: Wählen Sie das während der Remotesitzung für Audio zu verwendende Gerät aus. Sie können auswählen, ob Sound auf den lokalen Geräten, auf dem Remotegerät oder überhaupt nicht wiedergegeben werden soll.
   - **Bildschirmauflösung anpassen**: Legen Sie eine benutzerdefinierte Auflösung für eine Verbindung durch Aktivieren dieser Einstellung fest. Wenn diese Einstellung deaktiviert ist, wird die Auflösung angewendet, die Sie in den globalen Einstellungen der App festgelegt haben.
   - **Maustasten tauschen**: Verwenden Sie diese Option, um die Funktionen der linken Maustaste gegen die rechte Maustaste zu tauschen. (Dies ist besonders nützlich, wenn der Remote-PC für einen Linkshänder konfiguriert ist, Sie aber eine Rechtshändermaus verwenden.)
   - **Mit Administratorsitzung verbinden**: Verwenden Sie diese Option, um eine Verbindung mit einer Konsolensitzung zum Verwalten eines Windows-Servers herzustellen.
   - **An lokalen Speicher umleiten**: Stellt Ihren lokalen Speicher als Remotedateisystem auf dem Remote-PC bereit.
4. Tippen Sie auf **Speichern**.

Müssen Sie diese Einstellungen bearbeiten? Tippen Sie auf das Überlaufmenü ( **...** ) neben dem Namen des Desktops, und tippen Sie dann auf **Bearbeiten**.

Möchten Sie die Verbindung löschen? Tippen Sie wieder auf das Überlaufmenü ( **...** ), und tippen Sie dann auf **Entfernen**.

>[!TIP]
> Wenn Sie den Fehler 0xf07 zu einem falschen Kennwort (die Fehlermeldung „Es konnte keine Verbindung mit dem Remote-PC hergestellt werden, da das dem Benutzerkonto zugeordnete Kennwort abgelaufen ist“) erhalten, ändern Sie das Kennwort, und versuchen Sie es erneut.

### <a name="add-a-remote-resource"></a>Hinzufügen einer Remoteressource
Bei Remoteressourcen handelt es sich um RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops, die mithilfe von RemoteApp- und Desktopverbindungen veröffentlicht werden.

Gehen Sie wie folgt vor, um eine Remoteressource hinzuzufügen:

1. Tippen Sie auf dem Bildschirm „Connection Center“ auf das Pluszeichen ( **+** ), und tippen Sie dann auf **Remoteressourcenfeed**. 
2. Geben Sie Informationen für die Remoteressource ein:
   - **E-Mail-Adresse oder URL**: Die URL des Servers mit Web Access für Remotedesktop. In dieses Feld können Sie auch Ihr geschäftliches E-Mail-Konto eingeben. Dies weist den Client an, nach dem Ihrer E-Mail-Adresse zugeordneten Server mit Web Access für Remotedesktop zu suchen.
   - **Benutzername**: Der Benutzername, der für den Server mit Web Access für Remotedesktop verwendet werden soll, mit dem Sie eine Verbindung herstellen.
   - **Kennwort**: Das Kennwort, das für den Server mit Web Access für Remotedesktop verwendet werden soll, mit dem Sie eine Verbindung herstellen.
3. Tippen Sie auf **Speichern**.

Die Remoteressourcen werden im Connection Center angezeigt.


Gehe wie folgt vor, um Remoteressourcen zu löschen:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben der Remoteressource.
2. Tippen Sie auf **Entfernen**.
3. Bestätigen Sie den Löschvorgang.

### <a name="widgets--pin-a-saved-desktop-to-your-home-screen"></a>Widgets – Anheften eines gespeicherten Desktops an Ihren Startbildschirm

Die Remotedesktopanwendungen unterstützen das Anheften von Verbindungen an den Startbildschirm mithilfe der Android-Widget-Funktion. Die Art und Weise, wie Sie ein Widget hinzufügen, hängt vom Typ des verwendeten Android-Geräts und vom Betriebssystem ab. Nachfolgend wird die gängigste Methode zum Hinzufügen eines Widgets beschrieben: 

1. Tippen Sie auf **Apps**, um das Menü „Apps“ zu starten.
2. Tippen Sie auf **Widgets**.
3. Navigieren Sie per Wischbewegung durch die Widgets, und suchen Sie nach dem Remotedesktopsymbol mit der Beschreibung „Remotedesktop anheften“.
4. Tippen Sie auf das Remotedesktop-Widget, halten Sie es gedrückt, und verschieben Sie es auf den Startbildschirm.
5. Wenn Sie das Symbol loslassen, werden die gespeicherten Remotedesktops angezeigt. Wählen Sie die Verbindung aus, die Sie auf dem Startbildschirm speichern möchten.

Jetzt können Sie die Remotedesktopverbindung direkt auf dem Startbildschirm starten, indem Sie darauf tippen.

> [!NOTE]
> Wenn Sie die Desktopverbindung in der Remotedesktopanwendung umbenennen, wird die Bezeichnung dieses angehefteten Remotedesktops nicht aktualisiert.

## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>Herstellen einer Verbindung mit einem Remotedesktopgateway zum Zugreifen auf interne Ressourcen

Mit einem Remotedesktopgateway (RD-Gateway) können Sie eine Verbindung mit einem Remotecomputer in einem Unternehmensnetzwerk über das Internet herstellen. Sie können Ihre Gateways mit dem Remotedesktopclient erstellen und verwalten.

Gehen Sie wie folgt vor, um ein neues Gateway einzurichten:

1. Tippen Sie im Connection Center auf **Einstellungen > Gateways**. Tippen Sie auf das Pluszeichen ( **+** ), um ein neues Gateway hinzuzufügen.
2. Geben Sie die folgenden Informationen ein:
   - **Servername**: Der Name des Computers, den Sie als Gateway verwenden möchten. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können dem Servernamen auch Portinformationen hinzufügen (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
   - **Benutzername**: Der Benutzername und das Kennwort für das Remotedesktopgateway, mit dem Sie eine Verbindung herstellen. Sie können auch **Desktopbenutzerkonto verwenden** auswählen, damit die gleichen Anmeldeinformationen wie für die Remotedesktopverbindung verwendet werden.

## <a name="manage-your-user-accounts"></a>Verwalten Ihrer Benutzerkonten

Wenn du eine Verbindung mit einem Desktop oder mit Remoteressourcen herstellst, kannst du die Benutzerkonten speichern, um sie erneut auswählen zu können. Du kannst auch Benutzerkonten auf dem Client selbst definieren, anstatt die Benutzerdaten zu speichern, wenn du eine Verbindung mit einem Desktop herstellst.

Gehen Sie wie folgt vor, um ein neues Benutzerkonto zu erstellen:

1. Tippen Sie im Connection Center auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Tippen Sie auf das Pluszeichen ( **+** ), um ein neues Benutzerkonto hinzuzufügen.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername**: Der Name des Benutzers, der zur Verwendung für eine Remoteverbindung gespeichert werden soll. Sie können den Benutzernamen in einem der folgenden Formate eingeben: Benutzername, Domäne\Benutzername oder user_name@domain.com.
   - **Kennwort**: Das Kennwort für den angegebenen Benutzer. Jedem Benutzerkonto, das Sie zur Verwendung für Remoteverbindungen speichern möchten, muss ein Kennwort zugeordnet sein.
4. Tippen Sie auf **Speichern**.

Gehen Sie wie folgt vor, um ein Benutzerkonto zu löschen:

1. Tippen Sie im Connection Center auf **Einstellungen > Benutzerkonten**.
2. Tippen Sie in der Liste auf ein Benutzerkonto, und halten Sie es gedrückt, um es auszuwählen. Sie können mehrere Benutzer auswählen.
3. Tippen Sie auf den Papierkorb, um den ausgewählten Benutzer zu löschen.

## <a name="navigate-the-remote-desktop-session"></a>Navigieren in der Remotedesktopsitzung
Wenn du eine Remotedesktopverbindung startest, stehen Tools zur Verfügung, die du für die Navigation in der Sitzung verwenden kannst.

### <a name="start-a-remote-desktop-connection"></a>Starten einer Remotedesktopverbindung

1. Tippen Sie auf die Remotedesktopverbindung, um die Sitzung zu starten. 
2. Wenn Sie zur Überprüfung des Zertifikats für den Remotedesktop aufgefordert werden, tippen Sie auf **Verbinden**. Sie können auch **Nicht erneut nach Verbindungen mit diesem Computer fragen** auswählen, um das Zertifikat immer zu akzeptieren.

### <a name="manage-global-app-settings"></a>Verwalten globaler App-Einstellungen

Sie können die folgenden globalen Einstellungen auf Ihrem Android-Client festlegen:

- **Desktopvorschauen anzeigen**: Mit dieser Option können Sie eine Vorschau des Desktops im Connection Center anzeigen, bevor Sie eine Verbindung damit herstellen. Diese Option ist standardmäßig **aktiviert**.
- **Zwei-Finger-Zoom**: Diese Einstellung ermöglicht Ihnen das Verwenden von Zwei-Finger-Zoomgesten. Wenn die von Ihnen über Remotedesktop verwendete App Multitouch (eingeführt in Windows 8) unterstützt, **deaktivieren** Sie diese Einstellung.
- **Zur Verbesserung von Remotedesktop beitragen**: Sendet anonyme Daten an Microsoft. Wir verwenden diese Daten, um den Client zu verbessern. Weitere Informationen dazu, wie wir diese anonymen, privaten Daten behandeln, finden Sie in der [Datenschutzerklärung zum Remotedesktopclient](https://www.microsoft.com/privacystatement/RemoteApp/Default.aspx). Diese Einstellung ist standardmäßig **aktiviert**.
- **Anzeige**: Es sind zwei globale Einstellungen für die Anzeige verfügbar:
  - **Ausrichtung**: Legt die bevorzugte Ausrichtung (Querformat oder Hochformat) für die Sitzung fest. 
    >[!NOTE]
    > Wenn Sie eine Verbindung mit einem PC unter Windows 8 oder einer älteren Version von Windows herstellen, wird die Sitzung nicht ordnungsgemäß skaliert. Die beste Lösung besteht darin, die Verbindung mit dem PC zu trennen und dann die Verbindung in der gewünschten Ausrichtung wiederherzustellen. Eine noch bessere Option ist das Upgraden des PCs auf mindestens Windows 8.1.

  - **Auflösung**: Legt die Auflösung fest, die global für Desktopverbindungen verwendet werden soll. Wenn Sie bereits eine benutzerdefinierte Auflösung für eine einzelne App oder Verbindung festgelegt haben, wird dies durch diese Einstellung nicht geändert.
    >[!NOTE]
    >Wenn Sie eine der Anzeigeeinstellungen ändern, gilt die entsprechende Einstellung nur für neue Verbindungen ab diesem Zeitpunkt. Wenn Sie die Änderung in einer bereits verbundenen Sitzung anzeigen möchten, trennen Sie die Verbindung, und stellen Sie dann die Verbindung erneut her.

### <a name="connection-bar"></a>Verbindungsleiste

Die Verbindungsleiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente. Die Verbindungsleiste befindet sich standardmäßig in der Mitte am oberen Rand des Bildschirms. Doppeltippen Sie auf die Leiste, und ziehen Sie die Leiste nach links oder rechts, um sie zu verschieben.

- **Schwenken-Steuerelement**: Mit dem Schwenken-Steuerelement kann der Bildschirm vergrößert und verschoben werden. Beachten Sie, dass das Schwenken-Steuerelement nur mithilfe direkter Touchbewegung verfügbar ist.
   - Aktivieren/Deaktivieren des Schwenken-Steuerelements: Tippen Sie auf der Verbindungsleiste auf das Schwenksymbol, um das Schwenken-Steuerelement anzuzeigen und den Bildschirm zu vergrößern. Tippen Sie auf der Verbindungsleiste erneut auf das Schwenksymbol, um das Steuerelement auszublenden und die ursprüngliche Auflösung des Bildschirms wiederherzustellen.
   - Verwenden des Schwenken-Steuerelements: Tippen Sie auf das Schwenken-Steuerelement, halten Sie es gedrückt, und ziehen Sie es dann in die Richtung, in der Sie den Bildschirm verschieben möchten.
   - Verschieben des Schwenken-Steuerelements: Doppeltippen Sie auf das Schwenken-Steuerelement, und halten Sie das Steuerelement gedrückt, um es auf dem Bildschirm zu verschieben.
- **Zusätzliche Optionen**: Tippen Sie auf das Symbol für zusätzliche Optionen, um die Auswahl- und die Befehlsleiste (siehe unten) der Sitzung anzuzeigen.
- **Tastatur**: Tippen Sie auf das Tastatursymbol, um die Tastatur ein- oder auszublenden. Das Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur eingeblendet ist.
- **Verschieben der Verbindungsleiste**: Tippen Sie auf die Verbindungsleiste, halten Sie die Leiste gedrückt, und ziehen Sie sie dann per Drag & Drop an eine neue Position am oberen Rand des Bildschirms.


### <a name="command-bar"></a>Befehlsleiste

Tippen Sie auf die Verbindungsleiste, um die Befehlsleiste auf der rechten Seite des Bildschirms anzuzeigen. Sie können zwischen den Mausmodi (direkte Touchbewegung und Mauszeiger) wechseln. Verwenden Sie die Schaltfläche „Startseite“, um von der Befehlsleiste zurück zum Connection Center zu wechseln. Alternativ können Sie für die gleiche Aktion auch die Schaltfläche „Zurück“ verwenden. Die Verbindung der aktiven Sitzung wird nicht getrennt. 


### <a name="use-direct-touch-gestures-and-mouse-modes-in-a-remote-session"></a>Verwenden von direkten Touchgesten und Mausmodi in einer Remotesitzung

Der Client verwendet Standardtouchgesten. Sie können auch Touchgesten verwenden, um Mausaktionen auf dem Remotedesktop zu replizieren. Die verfügbaren Mausmodi sind in der folgenden Tabelle aufgeführt.

> [!NOTE]
> Bei der Interaktion mit Windows 8 oder höher werden die nativen Touchgesten im Modus für die direkte Touchbewegung unterstützt. 

| Mausmodus    | Mausvorgang      | Geste                                                               |
|---------------|----------------------|-----------------------------------------------------------------------|
| Direkte Touchbewegung  | Linksklick           | Mit einem Finger tippen                                                          |
| Direkte Touchbewegung  | Rechtsklick          | Mit einem Finger tippen und halten                                                 |
| Mauszeiger | Zoom                 | Zwei Finger zusammenführen, um die Ansicht zu vergrößern, oder auseinander, um sie zu verkleinern. |
| Mauszeiger | Linksklick           | Mit einem Finger tippen                                                          |
| Mauszeiger | Linksklick und ziehen  | Mit einem Finger doppeltippen und halten, dann ziehen                               |
| Mauszeiger | Rechtsklick          | Mit zwei Fingern tippen                                                          |
| Mauszeiger | Rechtsklick und ziehen | Mit zwei Fingern doppeltippen und halten, dann ziehen                               |
| Mauszeiger | Mausrad          | Mit zwei Fingern tippen und halten, dann nach oben oder unten ziehen                           |

> [!TIP]
> Fragen und Kommentare sind immer willkommen. Verwenden Sie jedoch NICHT die Kommentarfunktion am Ende dieses Artikels, um Hilfe bei der Problembehandlung anzufordern. Verwenden Sie stattdessen das [Remotedesktopclient-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc), und erstellen Sie einen neuen Thread. Haben Sie einen Vorschlag für ein Feature? Teilen Sie uns dies im [UserVoice-Forum für den Client](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android) mit.
