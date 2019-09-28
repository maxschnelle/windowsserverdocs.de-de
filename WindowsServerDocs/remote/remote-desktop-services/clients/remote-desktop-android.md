---
title: Erste Schritte mit dem Android-Client
description: Allgemeine Informationen über den Android-Client.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64f038e1-40ec-4c67-938b-72edea49e5d8
author: heidilohr
manager: daveba
ms.author: helohr
ms.date: 09/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: d11e8ad0cac1f9cf024097450e90d9be95d950b0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387758"
---
# <a name="get-started-with-the-android-client"></a>Erste Schritte mit dem Android-Client

>Gilt für: Android 4.1 und höher

Du kannst den Remotedesktopclient für Android verwenden, um direkt mit Windows-Apps und -Desktops auf deinem Android-Gerät oder Chromebook zu arbeiten, das den Google Play Store unterstützt.

Verwenden Sie die folgenden Informationen für die ersten Schritte. Lesen Sie unbedingt die [häufig gestellten Fragen](remote-desktop-client-faq.md), wenn Sie Fragen haben.

> [!NOTE]
> - Möchten Sie mehr über die neuen Versionen für den Android-Client erfahren? Lies [Neues beim Android-Client](android-whatsnew.md).
> - Der Android-Client unterstützt Geräte unter Android 4.1 und höher sowie Chromebooks mit ChromeOS 53 und höher. Weitere Informationen zu Android-Anwendungen für Chrome finden Sie [hier](https://sites.google.com/a/chromium.org/dev/chromium-os/chrome-os-systems-supporting-android-apps).

## <a name="get-the-remote-desktop-client-and-start-using-it"></a>Abrufen des Remotedesktopclients und Ausführen der ersten Schritte

### <a name="download-the-remote-desktop-client-from-the-google-play-store"></a>Herunterladen des Remotedesktopclients aus dem Google Play Store

So richtest du den Remotedesktopclient auf deinem Android-Gerät ein:

1. Lade den Microsoft-Remotedesktopclient aus [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android) herunter.
2. Starte den **Remotedesktopclient** aus deiner Liste der Apps.
3. Füge eine [Remotedesktopverbindung](#add-a-remote-desktop-connection) oder [Remoteressource](#add-remote-resources) hinzu. Du verwendest eine Verbindung, um direkt eine Verbindung mit einem Windows-PC und mit Remoteressourcen herzustellen, um auf Apps und Desktops zuzugreifen, die ein Administrator für dich veröffentlicht hat.

> [!NOTE]
> Möchtest du neue Features früher (Flight) nutzen, empfehlen wir dir, unseren [Microsoft Remote Desktop Beta](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android.beta)-Client aus dem Google Play Store herunterzuladen.

### <a name="add-a-remote-desktop-connection"></a>Hinzufügen einer Remotedesktopverbindung

Sofern dies noch nicht geschehen ist, [richte deinen PC so ein, dass er Remoteverbindungen akzeptiert](remote-desktop-allow-access.md).

Gehe wie folgt vor, um eine Remotedesktopverbindung zu erstellen:

1. Tippe im Connection Center auf das Pluszeichen ( **+** ), und tippe dann auf **Desktop**.
2. Gib den Namen des Remotecomputers in **PC-Name** ein. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Du kannst auch Portinformationen an den PC-Namen anfügen (z. B. „MeinDesktop:3389“ oder „10.0.0.1:3389“). Dies ist das einzige erforderliche Feld.
3. Wähle den **Benutzernamen** aus, den du verwendest, um auf den Remotecomputer zuzugreifen.
   - Wähle **Jedes Mal eingeben** aus, wenn der Client bei jeder Anmeldung am Remotecomputer deine Anmeldeinformationen abfragen soll.
   - Wähle **Benutzerkonto hinzufügen** aus, um ein Konto zu speichern, das du häufig verwendest, damit du nicht bei jeder Anmeldung deine Anmeldeinformationen eingeben musst. Weitere Informationen findest du unter [Verwalten deiner Benutzerkonten](#manage-your-user-accounts).
4. Du kannst auch auf **Weitere Optionen anzeigen** tippen, um die folgenden optionalen Parameter festzulegen:
   - In **Anzeigename** kannst du einen leicht zu merkenden Namen für den PC eingeben, mit dem du die Verbindung herstellen möchtest. Wenn du keinen Anzeigenamen angibst, wird stattdessen der PC-Name angezeigt.
   - **Gateway** ist das Remotedesktopgateway, das Sie verwenden, um von einem externen Netzwerk aus eine Verbindung mit einem Computer herzustellen. Weitere Informationen erhalten Sie von Ihrem Systemadministrator.
   - **Sound** wählt das Gerät aus, das von der Remote Sitzung für die Audiowiedergabe verwendet wird. Sie können sich entscheiden, Audiosignale auf Ihrem lokalen Gerät, dem Remotegerät oder gar nicht wiederzugeben.
   - **Anzeigeauflösung anpassen** legt die Auflösung für die Remotesitzung fest. Ist diese Option deaktiviert, wird die Auflösung verwendet, die in den globalen Einstellungen angegeben ist.
   - **Maustasten tauschen** vertauscht die Befehle, die von der linken und der rechten Maustaste gesendet werden. Ideal für linkshändige Benutzer.
   - Über **Mit Administratorsitzung verbinden** kannst du eine Verbindung mit einer Administratorsitzung auf dem Remotecomputer herstellen.
   - **Lokalen Speicher umleiten** aktiviert die Umleitung des lokalen Speichers. Diese Einstellung ist standardmäßig deaktiviert.
5. Tippe auf **Speichern**, wenn du fertig bist.

Müssen Sie diese Einstellungen bearbeiten? Tippe auf das Überlaufmenü ( **...** ) neben dem Namen des Desktops und dann auf **Bearbeiten**.

Möchtest du die Verbindung entfernen? Tippe erneut auf das Überlaufmenü ( **...** ) und dann auf **Entfernen**.

>[!TIP]
> Wenn Sie den Fehler 0xf07 zu einem falschen Kennwort (die Fehlermeldung „Es konnte keine Verbindung mit dem Remote-PC hergestellt werden, da das dem Benutzerkonto zugeordnete Kennwort abgelaufen ist“) erhalten, ändern Sie das Kennwort, und versuchen Sie es erneut.

### <a name="add-remote-resources"></a>Hinzufügen von Remoteressourcen

Bei Remoteressourcen handelt es sich um RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops, die von Ihrem Administrator veröffentlicht werden. Der Android-Client unterstützt Ressourcen, die von Bereitstellungen von **Remotedesktopdienste** und **Windows Virtual Desktop** veröffentlicht werden. So fügen Sie Remoteressourcen hinzu:

1. Tippe im Connection Center auf **+** , und tippe dann auf **Remoteressourcenfeed**.
2. Geben Sie die **Feed-URL** ein. Dies kann eine URL oder eine E-Mail-Adresse sein:
   - Die **URL** ist der RD-Webzugriffsserver, der dir von deinem Administrator zur Verfügung gestellt wird. Wenn Sie auf Ressourcen von Windows Virtual Desktop zugreifen, können Sie `https://rdweb.wvd.microsoft.com` verwenden.
   - Wenn Sie **E-Mail** verwenden möchten, geben Sie in diesem Feld Ihre E-Mail-Adresse ein. Dies weist den Client an, nach einem RD-Webzugriffsserver zu suchen, der Ihrer E-Mail-Adresse zugeordnet ist, wenn dies von Ihrem Administrator konfiguriert wurde.
3. Tippen Sie auf **Weiter**.
4. Geben Sie auf Aufforderung Ihre Anmeldeinformationen ein. Diese können sich je nach Bereitstellung unterscheiden und können Folgendes beinhalten:
   - Der **Benutzername**, der die Berechtigung hat, auf die Ressourcen zuzugreifen.
   - Das **Kennwort**, das dem Benutzernamen zugeordnet ist.
   - **Zusätzlicher Faktor**, zu dessen Eingabe du ggf. aufgefordert wirst, wenn die Authentifizierung von deinem Administrator in dieser Weise konfiguriert wurde.
5. Tippe auf **Speichern**, wenn du fertig bist.

Die Remoteressourcen werden im Connection Center angezeigt.

Gehe wie folgt vor, um Remoteressourcen zu entfernen:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben der Remoteressource.
2. Tippe auf **Entfernen**.
3. Bestätige das Entfernen.

### <a name="widgets--pin-a-saved-desktop-to-your-home-screen"></a>Widgets – Anheften eines gespeicherten Desktops an Ihren Startbildschirm

Der Remotedesktopclient unterstützt das Anheften von Verbindungen an den Startbildschirm mithilfe der Android-Widget-Funktion. Die Art und Weise, wie Sie ein Widget hinzufügen, hängt vom Typ des verwendeten Android-Geräts und vom Betriebssystem ab. Nachfolgend wird die gängigste Methode zum Hinzufügen eines Widgets beschrieben:

1. Tippe auf **Apps**, um das Menü der Apps zu starten.
2. Tippe auf **Widgets**.
3. Navigieren Sie per Wischbewegung durch die Widgets, und suchen Sie nach dem Remotedesktopsymbol mit der Beschreibung „Remotedesktop anheften“.
4. Tippen Sie auf das Remotedesktop-Widget, halten Sie es gedrückt, und verschieben Sie es auf den Startbildschirm.
5. Wenn Sie das Symbol loslassen, werden die gespeicherten Remotedesktops angezeigt. Wählen Sie die Verbindung aus, die Sie auf dem Startbildschirm speichern möchten.

Jetzt können Sie die Remotedesktopverbindung direkt auf dem Startbildschirm starten, indem Sie darauf tippen.

> [!NOTE]
> Wenn du die Desktopverbindung im Remotedesktopclient umbenennst, wird deren angeheftete Bezeichnung nicht aktualisiert.

## <a name="manage-general-app-settings"></a>Verwalten allgemeiner App-Einstellungen

Um die allgemeinen App-Einstellungen zu ändern, tippe auf **Einstellungen**, und tippe dann im Connection Center auf **Allgemein**.

Du kannst die folgenden allgemeinen Einstellungen festlegen:

- **Show Desktop Previews** (Desktopvorschauen anzeigen): Mit dieser Option kannst du eine Vorschau des Desktops im Connection Center anzeigen, bevor du eine Verbindung damit herstellst. Die Einstellung ist standardmäßig aktiviert.
- **Pinch to zoom remote session** (Zwei-Finger-Zoom, um Remotesitzung zu zoomen): Diese Einstellung ermöglicht dir das Verwenden von Zwei-Finger-Zoom-Gesten. Wenn die von dir über Remotedesktop verwendete App Multitouch (eingeführt in Windows 8) unterstützt, deaktivierst du dieses Feature.
- Aktiviere **Use scancode input when available** (Scancodeeingabe verwenden, wenn verfügbar), wenn die Remote-App nicht ordnungsgemäß auf Tastatureingabe reagiert, die als Scancode gesendet wurde. Ist diese Option deaktiviert, wird Eingabe als Unicode gesendet.
- **Help improve Remote Desktop** (Zur Verbesserung von Remotedesktop beitragen): Sendet anonyme Daten an Microsoft. Wir verwenden diese Daten, um den Client zu verbessern. Weitere Informationen dazu, wie wir mit diesen anonymen privaten Daten umgehen, findest du in der [Datenschutzerklärung von Microsoft](https://privacy.microsoft.com/privacystatement). Die Einstellung ist standardmäßig aktiviert.

## <a name="manage-display-settings"></a>Verwalten von Anzeigeeinstellungen

Um die Anzeigeeinstellungen zu ändern, tippe auf **Einstellungen**, und tippe dann im Connection Center auf **Anzeige**.

Du kannst die folgenden Anzeigeeinstellungen festlegen:

- **Ausrichtung** legt die bevorzugte Ausrichtung (Querformat oder Hochformat) für die Sitzung fest.
  >[!NOTE]
  > Wenn du eine Verbindung mit einem PC unter Windows 8 oder einer älteren Version von Windows herstellst, wird die Sitzung nicht ordnungsgemäß skaliert, wenn die Ausrichtung des Geräts geändert wurde. Die beste Lösung besteht darin, die Verbindung mit dem PC zu trennen und dann die Verbindung in der gewünschten Ausrichtung wiederherzustellen. Eine noch bessere Option ist das Upgraden des PCs auf Windows 10.

- **Auflösung** legt die Remoteauflösung fest, die global für Desktopverbindungen verwendet werden soll. Wenn du bereits eine benutzerdefinierte Auflösung für eine einzelne Verbindung festgelegt hast, wird dies durch diese Einstellung nicht geändert.
  >[!NOTE]
  >Wenn Sie eine der Anzeigeeinstellungen ändern, gilt die entsprechende Einstellung nur für neue Verbindungen ab diesem Zeitpunkt. Wenn du die Änderung in einer bereits verbundenen Sitzung anzeigen möchtest, trennst du die Verbindung, und dann stellst du die Verbindung erneut her.

## <a name="manage-your-rd-gateways"></a>Verwalten von RD-Gateways

Mit einem Remotedesktopgateway (RD-Gateway) kannst du eine Verbindung mit einem Remotecomputer in einem privaten Netzwerk über das Internet herstellen. Sie können Ihre Gateways mit dem Remotedesktopclient erstellen und verwalten.

Gehen Sie wie folgt vor, um ein neues Gateway einzurichten:

1. Tippe im Connection Center auf **Einstellungen**, und tippe dann auf **Gateways**.
1. Tippen Sie auf das Pluszeichen ( **+** ), um ein neues Gateway hinzuzufügen.
1. Geben Sie die folgenden Informationen ein:
   - Gib in **Servername** den Namen des Computers ein, den du als Gateway verwenden möchtest. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können dem Servernamen auch Portinformationen hinzufügen (z. B.: „RDGateway:443“ oder „10.0.0.1:443“).
   - Wähle das **Benutzerkonto** aus, das du verwenden möchtest, um auf das RD-Gateway zuzugreifen.
     - Aktiviere **Desktopbenutzerkonto verwenden**, um die Anmeldeinformationen zu verwenden, die du für den Remotecomputer angegeben hast.
     - Wähle **Benutzerkonto hinzufügen** aus, um ein Konto zu speichern, das du häufig verwendest, damit du nicht bei jeder Anmeldung deine Anmeldeinformationen eingeben musst. Befolge diese Anweisungen, um [deine Benutzerkonten zu verwalten](#manage-your-user-accounts).

So löscht du ein Gateway

1. Tippe im Connection Center auf **Einstellungen**, und tippe dann auf **Gateways**.
2. Tippe auf und halte ein Gateway in der Liste, um es auszuwählen. Du kannst mehrere Gateways gleichzeitig auswählen.
3. Tippe auf den Papierkorb, um das ausgewählte Gateway zu löschen.

## <a name="manage-your-user-accounts"></a>Verwalten Ihrer Benutzerkonten

Wenn Sie eine Verbindung mit einem Desktop oder Remoteressourcen herstellen, können Sie die Benutzerkonten speichern, um sie erneut auswählen zu können.

Gehen Sie wie folgt vor, um ein neues Benutzerkonto zu erstellen:

1. Tippen Sie im Connection Center auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Tippen Sie auf das Pluszeichen ( **+** ), um ein neues Benutzerkonto hinzuzufügen.
3. Geben Sie die folgenden Informationen ein:
   - Der **Benutzername**, der zur Verwendung für eine Remoteverbindung gespeichert werden soll. Sie können den Benutzernamen in einem der folgenden Formate eingeben: Benutzername, Domäne\Benutzername oder user_name@domain.com.
   - Das **Kennwort** für den angegebenen Benutzer. Jedem Benutzerkonto, das Sie zur Verwendung für Remoteverbindungen speichern möchten, muss ein Kennwort zugeordnet sein.
4. Tippe auf **Speichern**, wenn du fertig bist.

Gehen Sie wie folgt vor, um ein Benutzerkonto zu löschen:

1. Tippen Sie im Connection Center auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Tippen Sie in der Liste auf ein Benutzerkonto, und halten Sie es gedrückt, um es auszuwählen. Sie können mehrere Benutzer auswählen.
3. Tippen Sie auf den Papierkorb, um den ausgewählten Benutzer zu löschen.

## <a name="navigate-the-remote-desktop-session"></a>Navigieren in der Remotedesktopsitzung

Wenn du eine Remotedesktopverbindung startest, stehen Tools zur Verfügung, die du für die Navigation in der Sitzung verwenden kannst.

### <a name="start-a-remote-desktop-connection"></a>Starten einer Remotedesktopverbindung

1. Tippe auf die Remotedesktopverbindung, um die Sitzung zu starten.
2. Wenn du zur Überprüfung des Zertifikats für den Remotedesktop aufgefordert wirst, tippe auf **Verbinden**. Sie können auch **Nicht erneut nach Verbindungen mit diesem Computer fragen** auswählen, um das Zertifikat immer zu akzeptieren.

### <a name="connection-bar"></a>Verbindungsleiste

Die Verbindungsleiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente. Standardmäßig befindet sich die Verbindungsleiste in der Mitte am oberen Rand des Bildschirms. Ziehe die Leiste nach links oder rechts, um sie zu verschieben.

- **Schwenken-Steuerelement**: Mit dem Schwenken-Steuerelement kann der Bildschirm vergrößert und verschoben werden. Das Schwenken-Steuerelement ist nur für direkte Berührung verfügbar.
  - Um das Schwenken-Steuerelement anzuzeigen, tippst du auf der Verbindungsleiste auf das Schwenksymbol, um das Schwenken-Steuerelement anzuzeigen und die Anzeige zu vergrößern. Tippe erneut auf das Schwenksymbol, um das Steuerelement auszublenden und die Anzeige wieder in ihre ursprüngliche Größe zu bringen.
  - Um das Schwenken-Steuerelement zu verwenden, drückst (tippen und halten) du auf das Steuerelement und ziehst es dann in die Richtung, in der die Anzeige verschoben werden soll.
  - Um das Schwenken-Steuerelements zu verschieben, doppeltippst du auf das Steuerelement, und drückst es danach, um es auf dem Bildschirm zu verschieben.
- **Zusätzliche Optionen**: Tippe auf das Symbol für zusätzliche Optionen, um die Auswahl- und die Befehlsleiste der Sitzung anzuzeigen.
- **Tastatur**: Tippen Sie auf das Tastatursymbol, um die Tastatur ein- oder auszublenden. Das Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur eingeblendet ist.

### <a name="session-selection-bar"></a>Sitzungsauswahlleiste

Es können mehrere Verbindungen mit verschiedenen PCs gleichzeitig geöffnet sein. Tippen Sie auf die Verbindungsleiste, um die Sitzungsauswahlleiste auf der linken Seite des Bildschirms anzuzeigen. Mit der Sitzungsauswahlleiste kannst du deine geöffneten Verbindungen anzeigen und zwischen diesen wechseln.

Wenn du Verbindungen mit Remoteressourcen hast, kannst du zwischen Apps innerhalb dieser Sitzung wechseln, indem du auf das Erweiterungsmenü **>** tippst und eine App in der Liste der verfügbaren Elemente auswählst.

Um eine neue Sitzung über deine aktuelle Verbindung zu starten, tippst du auf **Neu starten** und wählst dann ein Element in der Liste der verfügbaren Elemente aus.

Um eine Sitzung zu trennen, tippst du auf der linken Seite der Kachel für die Sitzung auf **X**.

### <a name="command-bar"></a>Befehlsleiste

Tippen Sie auf die Verbindungsleiste, um die Befehlsleiste auf der rechten Seite des Bildschirms anzuzeigen. In der Befehlsleiste kannst du zwischen den Mausmodi (direkte Touchbewegung und Mauszeiger) wechseln oder auf die Startseite-Schaltfläche tippen, um zum Connection Center zurückzukehren. Du kannst auch auf die Zurück-Schaltfläche tippen, um zum Connection Center zurückzukehren. Eine Rückkehr zum Connection Center bewirkt nicht, dass die Verbindung deiner aktiven Sitzung getrennt wird.

### <a name="use-touch-gestures-and-mouse-modes-in-a-remote-session"></a>Verwenden von Touchgesten und Mausmodi in einer Remotesitzung

Der Client verwendet Standardtouchgesten. Sie können auch Touchgesten verwenden, um Mausaktionen auf dem Remotedesktop zu replizieren. In der folgenden Tabelle wird erläutert, welche Gesten welchen Mausaktionen in jedem Mausmodus entspricht.

> [!NOTE]
> Die nativen Touchgesten werden in Windows 8 oder höher im Modus für die direkte Touchbewegung unterstützt.

| Mausmodus    | Mausaktion         | Geste                                                                 |
|---------------|----------------------|-------------------------------------------------------------------------|
| Direkte Touchbewegung  | Linksklick           | Mit einem Finger tippen                                                     |
| Direkte Touchbewegung  | Rechtsklick          | Mit einem Finger tippen und halten, dann loslassen                              |
| Mauszeiger | Zoom                 | Zwei Finger zusammenführen, um die Ansicht zu vergrößern, oder auseinander bewegen, um sie zu verkleinern |
| Mauszeiger | Linksklick           | Mit einem Finger tippen                                                     |
| Mauszeiger | Linksklick und ziehen  | Doppeltippen und mit einem Finger halten, dann ziehen                          |
| Mauszeiger | Rechtsklick          | Mit zwei Fingern tippen                                                    |
| Mauszeiger | Rechtsklick und ziehen | Doppeltippen und mit zwei Fingern halten, dann ziehen                         |
| Mauszeiger | Mausrad          | Tippen und mit zwei Fingern halten, dann nach oben oder unten ziehen                     |
