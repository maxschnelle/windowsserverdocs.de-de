---
title: Erste Schritte mit dem Android-Client
description: Allgemeine Informationen über den Android-Client.
ms.topic: article
ms.assetid: 64f038e1-40ec-4c67-938b-72edea49e5d8
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 09/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1f59c00e375ab142c4e3dadc480c648cdd8e2396
ms.sourcegitcommit: 877d6db73d9520e3a23738d6528016235493cff3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90779244"
---
# <a name="get-started-with-the-android-client"></a>Erste Schritte mit dem Android-Client

>Gilt für: Android 4.1 und höher

Du kannst den Remotedesktopclient für Android verwenden, um direkt mit Windows-Apps und -Desktops auf deinem Android-Gerät oder Chromebook zu arbeiten, das den Google Play Store unterstützt.

In diesem Artikel erfahren Sie, wie Sie in die Verwendung des Clients einsteigen. Sehen Sie bei weiteren Fragen unbedingt in unseren [Häufig gestellten Fragen (FAQ)](remote-desktop-client-faq.md) nach.

> [!NOTE]
> - Möchten Sie mehr über die neuen Versionen für den Android-Client erfahren? Lies [Neues beim Android-Client](android-whatsnew.md).
> - Der Android-Client unterstützt Geräte unter Android 4.1 und höher sowie Chromebooks mit ChromeOS 53 und höher. Mehr über Android-Anwendungen unter Chrome erfahren Sie unter [Chrome OS Systems Supporting Android Apps](https://sites.google.com/a/chromium.org/dev/chromium-os/chrome-os-systems-supporting-android-apps) (ChromeOS-Systeme, die Android-Apps unterstützen).

## <a name="download-the-remote-desktop-client"></a>Herunterladen des Remotedesktopclients

So richtest du den Remotedesktopclient auf deinem Android-Gerät ein:

1. [Download des Microsoft-Remotedesktopclients](https://play.google.com/store/apps/details?id=com.microsoft.rdc.androidx) von Google Play.
2. Starte den **Remotedesktopclient** aus deiner Liste der Apps.
3. Füge eine [Remotedesktopverbindung](#add-a-remote-desktop-connection) oder [Remoteressource](#add-remote-resources) hinzu. Mithilfe von Remotedesktopverbindungen können Sie direkt eine Verbindung mit einem Windows-PC und Remoteressourcen herstellen, um auf Apps und Desktops zuzugreifen, die ein Administrator für Sie veröffentlicht hat.

## <a name="add-a-remote-desktop-connection"></a>Hinzufügen einer Remotedesktopverbindung

Nachdem der Client nun auf Ihrem Gerät verfügbar ist, können Sie Remotedesktopverbindungen hinzufügen, um auf Ihre Remoteressourcen zuzugreifen.

Bevor Sie eine Verbindung hinzufügen, [richten Sie Ihren PC für das Annehmen von Remoteverbindungen ein](remote-desktop-allow-access.md), wenn dies noch nicht geschehen ist.

So fügen Sie eine Remotedesktopverbindung hinzu:

1. Tippe im Connection Center auf das Pluszeichen ( **+** ), und tippe dann auf **Desktop**.
2. Gib den Namen des Remotecomputers in **PC-Name** ein. Bei diesem -Namen kann es sich um den Namen eines Windows-Computers, einen Internetdomänenname oder eine IP-Adresse handeln. Du kannst auch Portinformationen an den PC-Namen anfügen (z. B. „MeinDesktop:3389“ oder „10.0.0.1:3389“). Dies ist das einzige Pflichtfeld.
3. Wähle den **Benutzernamen** aus, den du verwendest, um auf den Remotecomputer zuzugreifen.

   - Wähle **Jedes Mal eingeben** aus, wenn der Client bei jeder Anmeldung am Remotecomputer deine Anmeldeinformationen abfragen soll.
   - Wähle **Benutzerkonto hinzufügen** aus, um ein Konto zu speichern, das du häufig verwendest, damit du nicht bei jeder Anmeldung deine Anmeldeinformationen eingeben musst. Weitere Informationen zu Benutzerkonten finden Sie unter [Verwalten von Benutzerkonten](#manage-your-user-accounts).

4. Du kannst auch auf **Weitere Optionen anzeigen** tippen, um die folgenden optionalen Parameter festzulegen:

   - In **Anzeigename** kannst du einen leicht zu merkenden Namen für den PC eingeben, mit dem du die Verbindung herstellen möchtest. Wenn du keinen Anzeigenamen angibst, wird stattdessen der PC-Name angezeigt.
   - **Gateway** ist das Remotedesktopgateway, das Sie verwenden, um von einem externen Netzwerk aus eine Verbindung mit einem Computer herzustellen. Weitere Informationen erhalten Sie von Ihrem Systemadministrator.
   - **Sound** wählt das Gerät aus, das von der Remote Sitzung für die Audiowiedergabe verwendet wird. Sie können sich entscheiden, Audiosignale auf Ihrem lokalen Gerät, dem Remotegerät oder gar nicht wiederzugeben.
   - **Anzeigeauflösung anpassen** legt die Auflösung für die Remotesitzung fest. Ist diese Option deaktiviert, wird die Auflösung verwendet, die in den globalen Einstellungen angegeben ist.
   - **Maustasten tauschen** vertauscht die Befehle, die von der linken und der rechten Maustaste gesendet werden. Ideal für linkshändige Benutzer.
   - Über **Mit Administratorsitzung verbinden** kannst du eine Verbindung mit einer Administratorsitzung auf dem Remotecomputer herstellen.
   - **Lokalen Speicher umleiten** aktiviert die Umleitung des lokalen Speichers. Diese Einstellung ist standardmäßig deaktiviert.

5. Tippe auf **Speichern**, wenn du fertig bist.

Müssen Sie diese Einstellungen bearbeiten? Tippe auf das Menü **Weitere Optionen** ( **...** ) neben dem Namen des Desktops und dann auf **Bearbeiten**.

Möchtest du die Verbindung entfernen? Tippe erneut auf das Menü **Weitere Optionen** ( **...** ) und dann auf **Entfernen**.

>[!TIP]
> Wenn ein Fehlername „0xf07“ mit einer Aussage ähnlich „Wir konnten keine Verbindung mit dem Remote-PC herstellen, da das dem Benutzerkonto zugeordnete Kennwort abgelaufen ist“ angezeigt wird, versuchen Sie es noch einmal mit einem neuen Kennwort.

## <a name="add-remote-resources"></a>Hinzufügen von Remoteressourcen

Bei Remoteressourcen handelt es sich um RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops, die von Ihrem Administrator veröffentlicht werden. Der Android-Client unterstützt Ressourcen, die von Bereitstellungen von **Remotedesktopdienste** und **Windows Virtual Desktop** veröffentlicht werden.

So fügen Sie Remoteressourcen hinzu:

1. Tippe im Verbindungscenter auf **+** , und tippe dann auf **Remoteressourcenfeed**.
2. Geben Sie die **Feed-URL** ein. Bei dieser URL kann es sich um eine URL oder eine E-Mail-Adresse handeln:
   - Die **URL** ist der RD-Webzugriffsserver, der dir von deinem Administrator zur Verfügung gestellt wird. Wenn Sie auf Ressourcen von Windows Virtual Desktop zugreifen, können Sie eine der folgenden URLs verwenden, je nachdem, welche Version Sie verwenden:
     - Verwenden Sie `https://rdweb.wvd.microsoft.com/api/feeddiscovery/webfeeddiscovery.aspx` für Windows Virtual Desktop (klassisch).
     - Verwenden Sie `https://rdweb.wvd.microsoft.com/api/arm/feeddiscovery` für Windows Virtual Desktop.
   - Wenn Sie **E-Mail** verwenden möchten, geben Sie in diesem Feld Ihre E-Mail-Adresse ein. Durch das Ausfüllen dieses Felds wird der Client angewiesen, nach einem RD-Webzugriffsserver zu suchen, der Ihrer E-Mail-Adresse zugeordnet ist, wenn dies von Ihrem Administrator konfiguriert wurde.
3. Tippen Sie auf **Weiter**.
4. Geben Sie auf Aufforderung Ihre Anmeldeinformationen ein. Diese zu verwendenden Anmeldeinformationen können sich je nach Bereitstellung unterscheiden und Folgendes beinhalten:
   - Der **Benutzername**, der die Berechtigung hat, auf die Ressourcen zuzugreifen.
   - Das **Kennwort**, das dem Benutzernamen zugeordnet ist.
   - **Zusätzlicher Faktor**, zu dessen Eingabe du ggf. aufgefordert wirst, wenn die Authentifizierung von deinem Administrator in dieser Weise konfiguriert wurde.
5. Tippe auf **Speichern**, wenn du fertig bist.

Die Remoteressourcen werden im Connection Center angezeigt.

## <a name="remove-remote-resources"></a>Entfernen von Remoteressourcen

Gehe wie folgt vor, um Remoteressourcen zu entfernen:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben der Remoteressource.
2. Tippe auf **Entfernen**.
3. Vergewissern Sie sich, dass die Ressource entfernt wurde.

## <a name="pin-a-connection-to-your-home-screen"></a>Anheften einer Verbindung an Ihren Startbildschirm

Der Remotedesktopclient unterstützt die Verwendung der Android-Widget-Funktion zum Anheften von Verbindungen an den Startbildschirm. Der Vorgang zum Hinzufügen von Widgets hängt davon ab, welchen Typ von Android-Gerät und welche Android-Betriebssystemversion Sie verwenden.

So fügen Sie ein Widget hinzu:

1. Tippe auf **Apps**, um das Menü der Apps zu starten.
2. Tippe auf **Widgets**.
3. Navigieren Sie per Wischbewegung durch die Widgets, und suchen Sie nach dem Remotedesktopsymbol mit der Beschreibung „Remotedesktop anheften“.
4. Tippen Sie auf das Remotedesktop-Widget, halten Sie es gedrückt, und verschieben Sie es auf den Startbildschirm.
5. Wenn Sie das Symbol loslassen, werden die gespeicherten Remotedesktops angezeigt. Wählen Sie die Verbindung aus, die Sie auf dem Startbildschirm speichern möchten.

Jetzt können Sie die Remotedesktopverbindung direkt auf dem Startbildschirm starten, indem Sie darauf tippen.

> [!NOTE]
> Wenn du die Desktopverbindung im Remotedesktopclient umbenennst, wird deren angeheftete Bezeichnung nicht aktualisiert.

## <a name="manage-general-app-settings"></a>Verwalten allgemeiner App-Einstellungen

Um die allgemeinen App-Einstellungen zu ändern, wechsle zum Verbindungscenter, tippe auf **Einstellungen** und dann auf **Allgemein**.

Du kannst die folgenden allgemeinen Einstellungen festlegen:

- **Show Desktop Previews** (Desktopvorschauen anzeigen): Mit dieser Option kannst du eine Vorschau des Desktops im Connection Center anzeigen, bevor du eine Verbindung damit herstellst. Die Einstellung ist standardmäßig aktiviert.
- **Pinch to zoom remote session** (Zwei-Finger-Zoom, um Remotesitzung zu zoomen): Diese Einstellung ermöglicht dir das Verwenden von Zwei-Finger-Zoom-Gesten. Wenn die von dir über Remotedesktop verwendete App Multitouch (eingeführt in Windows 8) unterstützt, deaktivierst du dieses Feature.
- Aktiviere **Use scancode input when available** (Scancodeeingabe verwenden, wenn verfügbar), wenn die Remote-App nicht ordnungsgemäß auf Tastatureingabe reagiert, die als Scancode gesendet wurde. Ist diese Option deaktiviert, wird Eingabe als Unicode gesendet.
- **Bei der Verbesserung von Remotedesktop helfen** sendet anonyme Daten über deine Verwendung von Remotedesktop für Android an Microsoft. Wir verwenden diese Daten, um den Client zu verbessern. Weitere Informationen zu unserer Datenschutzrichtlinie und welche Arten von Daten wir erfassen, findest du in der [Microsoft-Datenschutzerklärung](https://privacy.microsoft.com/privacystatement). Die Einstellung ist standardmäßig aktiviert.

## <a name="manage-display-settings"></a>Verwalten von Anzeigeeinstellungen

Um die Anzeigeeinstellungen zu ändern, tippe auf **Einstellungen**, und tippe dann im Connection Center auf **Anzeige**.

Du kannst die folgenden Anzeigeeinstellungen festlegen:

- **Ausrichtung** legt die bevorzugte Ausrichtung (Querformat oder Hochformat) für die Sitzung fest.

  >[!NOTE]
  > Wenn du eine Verbindung mit einem PC unter Windows 8 oder früher herstellst, wird die Sitzung nicht ordnungsgemäß skaliert, wenn die Ausrichtung des Geräts geändert wurde. Damit der Client ordnungsgemäß skaliert wird, trenne die Verbindung mit dem PC, und stelle dann die Verbindung in der gewünschten Ausrichtung wieder her. Du kannst die richtige Skalierung auch sicherstellen, indem du stattdessen einen PC mit Windows 10 verwendest.

- **Auflösung** legt die Remoteauflösung fest, die global für Desktopverbindungen verwendet werden soll. Wenn du bereits eine benutzerdefinierte Auflösung für eine einzelne Verbindung festgelegt hast, wird dies durch diese Einstellung nicht geändert.

  >[!NOTE]
  >Wenn du die Anzeigeeinstellungen änderst, gelten die Änderungen nur für die neuen Verbindungen ab dem Zeitpunkt der Einstellungsänderung. Um deine Änderungen auf die Sitzung anzuwenden, mit der du zurzeit verbunden bist, aktualisiere deine Sitzung durch Trennen und erneutes Verbinden.

## <a name="manage-your-rd-gateways"></a>Verwalten von RD-Gateways

Mit einem Remotedesktopgateway (RD-Gateway) kannst du eine Verbindung mit einem Remotecomputer in einem privaten Netzwerk über das Internet herstellen. Sie können Ihre Gateways mit dem Remotedesktopclient erstellen und verwalten.

So richtest du ein neues RD-Gateway ein

1. Tippe im Connection Center auf **Einstellungen**, und tippe dann auf **Gateways**.
2. Tippen Sie auf das Pluszeichen ( **+** ), um ein neues Gateway hinzuzufügen.
3. Geben Sie die folgenden Informationen ein:
   - Gib in **Servername** den Namen des Computers ein, den du als Gateway verwenden möchtest. Bei diesem Namen kann es sich um den Namen eines Windows-Computers, einen Internetdomänenname oder eine IP-Adresse handeln. Sie können dem Servernamen auch Portinformationen hinzufügen (z. B.: „RDGateway:443“ oder „10.0.0.1:443“).
   - Wähle das **Benutzerkonto** aus, das du verwenden möchtest, um auf das RD-Gateway zuzugreifen.
     - Aktiviere **Desktopbenutzerkonto verwenden**, um die Anmeldeinformationen zu verwenden, die du für den Remotecomputer angegeben hast.
     - Wähle **Benutzerkonto hinzufügen** aus, um ein Konto zu speichern, das du häufig verwendest, damit du nicht bei jeder Anmeldung deine Anmeldeinformationen eingeben musst. Weitere Informationen findest du unter [Verwalten deiner Benutzerkonten](#manage-your-user-accounts).

So löschst du ein RD-Gateway

1. Tippe im Connection Center auf **Einstellungen**, und tippe dann auf **Gateways**.
2. Tippe auf und halte ein Gateway in der Liste, um es auszuwählen. Du kannst mehrere Gateways gleichzeitig auswählen.
3. Tippe auf den Papierkorb, um das ausgewählte Gateway zu löschen.

## <a name="manage-your-user-accounts"></a>Verwalten Ihrer Benutzerkonten

Du kannst Benutzerkonten speichern, um sie immer zu verwenden, wenn du eine Verbindung mit einem Remotedesktop oder Remoteressourcen herstellst.

So speicherst du ein Benutzerkonto

1. Tippen Sie im Connection Center auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Tippen Sie auf das Pluszeichen ( **+** ), um ein neues Benutzerkonto hinzuzufügen.
3. Geben Sie die folgenden Informationen ein:
   - Der **Benutzername**, der zur Verwendung für eine Remoteverbindung gespeichert werden soll. Sie können den Benutzernamen in einem der folgenden Formate eingeben: Benutzername, Domäne\Benutzername oder user_name@domain.com.
   - Das **Kennwort** für den angegebenen Benutzer. Jedem Benutzerkonto, das Sie zur Verwendung für Remoteverbindungen speichern möchten, muss ein Kennwort zugeordnet sein.
4. Tippe auf **Speichern**, wenn du fertig bist.

So löschst du ein gespeichertes Benutzerkonto

1. Tippen Sie im Connection Center auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Tippen Sie in der Liste auf ein Benutzerkonto, und halten Sie es gedrückt, um es auszuwählen. Du kannst mehrere Benutzer gleichzeitig auswählen.
3. Tippen Sie auf den Papierkorb, um den ausgewählten Benutzer zu löschen.

## <a name="start-a-remote-desktop-connection"></a>Starten einer Remotedesktopverbindung

Nachdem Sie jetzt Ihren Remotedesktop-Android-Client eingerichtet haben, sollten wir lernen, wie eine Remotedesktopsitzung gestartet wird.

So starten Sie eine Sitzung:

1. Tippe auf **den Namen deiner Remotedesktopverbindung**, um die Sitzung zu starten.
2. Wenn du zur Überprüfung des Zertifikats für den Remotedesktop aufgefordert wirst, tippe auf **Verbinden**. Du kannst auch **Nicht erneut nach Verbindungen mit diesem Computer fragen** auswählen, um das Zertifikat standardmäßig immer zu akzeptieren.

## <a name="use-the-connection-bar"></a>Verwenden der Verbindungsleiste

Die Verbindungsleiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente. Standardmäßig befindet sich die Verbindungsleiste in der Mitte am oberen Rand des Bildschirms. Ziehe die Leiste nach links oder rechts, um sie zu verschieben.

- **Schwenken-Steuerelement**: Mit dem Schwenken-Steuerelement kann der Bildschirm vergrößert und verschoben werden. Das Schwenken-Steuerelement ist nur für direkte Berührung verfügbar.
  - Um das Schwenken-Steuerelement anzuzeigen, tippst du auf der Verbindungsleiste auf das Schwenksymbol, um das Schwenken-Steuerelement anzuzeigen und die Anzeige zu vergrößern. Tippe erneut auf das Schwenksymbol, um das Steuerelement auszublenden und die Anzeige wieder in ihre ursprüngliche Größe zu bringen.
  - Um das Schwenken-Steuerelement zu verwenden, drückst (tippen und halten) du auf das Steuerelement und ziehst es dann in die Richtung, in der die Anzeige verschoben werden soll.
  - Um das Schwenken-Steuerelements zu verschieben, doppeltippst du auf das Steuerelement, und drückst es danach, um es auf dem Bildschirm zu verschieben.
- **Zusätzliche Optionen**: Tippe auf das Symbol für zusätzliche Optionen, um die Auswahl- und die Befehlsleiste der Sitzung anzuzeigen.
- **Tastatur**: Tippen Sie auf das Tastatursymbol, um die Tastatur ein- oder auszublenden. Das Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur eingeblendet ist.

## <a name="use-the-session-selection-bar"></a>Verwenden der Sitzungsauswahlleiste

Es können mehrere Verbindungen mit verschiedenen PCs gleichzeitig geöffnet sein. Tippen Sie auf die Verbindungsleiste, um die Sitzungsauswahlleiste auf der linken Bildschirmseite anzuzeigen. Mit der Sitzungsauswahlleiste kannst du deine geöffneten Verbindungen anzeigen und zwischen diesen wechseln.

Wenn du Verbindungen mit Remoteressourcen hast, kannst du zwischen Apps innerhalb dieser Sitzung wechseln, indem du auf das Erweiterungsmenü ( **>** ) tippst und eine App in der Liste der verfügbaren Elemente auswählst.

Um eine neue Sitzung über deine aktuelle Verbindung zu starten, tippst du auf **Neu starten** und wählst dann ein Element in der Liste der verfügbaren Elemente aus.

Tippen Sie zum Trennen einer Sitzung auf der linken Seite der Sitzungskachel auf **X**.

## <a name="use-the-command-bar"></a>Verwenden der Befehlsleiste

Tippen Sie auf die Verbindungsleiste, um die Befehlsleiste rechts auf dem Bildschirm anzuzeigen. In der Befehlsleiste kannst du zwischen den Mausmodi (direkte Touchbewegung und Mauszeiger) wechseln oder auf die Startseite-Schaltfläche tippen, um zum Connection Center zurückzukehren. Du kannst auch auf die Zurück-Schaltfläche tippen, um zum Connection Center zurückzukehren. Eine Rückkehr zum Connection Center bewirkt nicht, dass die Verbindung deiner aktiven Sitzung getrennt wird.

## <a name="touch-gestures-and-mouse-modes"></a>Touchgesten und Mausmodi

Der Remotedesktop für den Android-Client verwendet Standard-Touchgesten. Sie können auch Touchgesten verwenden, um Mausaktionen auf dem Remotedesktop zu replizieren. In der folgenden Tabelle wird erläutert, welche Gesten welchen Mausaktionen in jedem Mausmodus entspricht.

> [!NOTE]
> Die nativen Touchgesten werden in Windows 8 oder höher im Modus für die direkte Touchbewegung unterstützt.

| Mausmodus    | Mausaktion         | Geste                                                                 |
|---------------|----------------------|-------------------------------------------------------------------------|
| Direkte Touchbewegung  | Linksklick           | Mit einem Finger tippen                                                     |
| Direkte Touchbewegung  | Klicken Sie mit der rechten Maustaste auf          | Mit einem Finger tippen und halten, dann loslassen                              |
| Mauszeiger | Zoom                 | Zwei Finger zusammenführen, um die Ansicht zu verkleinern, oder auseinander bewegen, um sie zu vergrößern. |
| Mauszeiger | Linksklick           | Mit einem Finger tippen                                                     |
| Mauszeiger | Linksklick und ziehen  | Doppeltippen und mit einem Finger halten, dann ziehen                          |
| Mauszeiger | Klicken Sie mit der rechten Maustaste auf          | Mit zwei Fingern tippen                                                    |
| Mauszeiger | Rechtsklick und ziehen | Doppeltippen und mit zwei Fingern halten, dann ziehen                         |
| Mauszeiger | Mausrad          | Tippen und mit zwei Fingern halten, dann nach oben oder unten ziehen                     |

## <a name="join-the-beta-channel"></a>Dem Beta-Kanal beitreten

Wenn Sie uns helfen möchten, neue Builds zu testen oder Probleme in kommenden Versionsupdates zu finden, bevor sie veröffentlicht werden, sollten Sie unserem Beta-Kanal beitreten. Unternehmens-Administratoren können den Beta-Kanal verwenden, um neue Versionen des Android-Clients für ihre Benutzer zu überprüfen.

Zur Teilnahme an der Beta [laden Sie unseren Beta-Client herunter](https://play.google.com/apps/testing/com.microsoft.rdc.androidx), und erteilen Sie Ihr Einverständnis, auf Vorschauversionen zuzugreifen und den Client herunterzuladen. Du erhältst die Vorschauversionen direkt über den Google Play Store.
