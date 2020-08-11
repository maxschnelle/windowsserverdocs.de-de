---
title: Erste Schritte mit dem Windows Store-Client
description: Enthält grundlegende Einrichtungsschritte für den Remotedesktopclient für Windows Store.
ms.topic: article
ms.assetid: 64f038e1-40ec-4c67-938b-72edea49e5d8
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: 05e32c05aaafb941958e025253e67c856d81257d
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990365"
---
# <a name="get-started-with-the-windows-store-client"></a>Erste Schritte mit dem Windows Store-Client

>Gilt für: Windows 10

Du kannst den Remotedesktopclient für Windows verwenden, um Windows-Apps und -Desktops über ein anderes Windows-Gerät per Remotezugriff zu nutzen.

Verwende die folgenden Informationen für die ersten Schritte. Lesen Sie unbedingt die [häufig gestellten Fragen](remote-desktop-client-faq.md), wenn Sie Fragen haben.

> [!NOTE]
> - Möchtest du mehr über die neuen Versionen für den Windows-Client erfahren? [Neuigkeiten im Windows Store-Client](windows-whatsnew.md) ansehen
> - Du kannst den Client unter jeder unterstützten Version von Windows 10 ausführen.

## <a name="get-the-rd-client-and-start-using-it"></a>Abrufen des Remotedesktopclients und Ausführen der ersten Schritte

Führe die folgenden Schritte für den Einstieg in Remotedesktop auf deinem Windows 10-Gerät aus:

1. Lade den Remotedesktopclient aus dem [Microsoft Store](https://www.microsoft.com/store/p/microsoft-remote-desktop/9wzdncrfj3ps) herunter.
2. [Richte deinen PC so ein, dass Remoteverbindungen zulässig sind](remote-desktop-allow-access.md).
3. Füge eine Remotedesktopverbindung oder eine Remoteressource hinzu. Mit einer Verbindung kannst du eine direkte Verbindung mit einem Windows-PC herstellen, und mit einer Remoteressource kannst du ein RemoteApp-Programm, einen sitzungsbasierten Desktop oder einen virtuellen Desktop (von deinem Administrator veröffentlicht) verwenden.
4. Hefte Elemente an, damit du schnell auf Remotedesktop zugreifen kannst.

### <a name="add-a-remote-desktop-connection"></a>Hinzufügen einer Remotedesktopverbindung

Gehe wie folgt vor, um eine Remotedesktopverbindung zu erstellen:

1. Tippen Sie im Connection Center auf **+ Hinzufügen** und dann auf **Desktop**.
2. Gib die folgenden Informationen für den Computer ein, mit dem du eine Verbindung herstellen möchtest:
   - **PC-Name**: Der Name des Computers. Der PC-Name kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können auch Portinformationen an den PC-Namen anfügen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**).
   - **Benutzerkonto**: Das Benutzerkonto zum Zugreifen auf den Remote-PC. Tippe auf **+** , um ein neues Konto hinzuzufügen oder ein vorhandenes Konto auszuwählen. Du kannst die folgenden Formate für den Benutzernamen verwenden: *user_name*, *domain\user_name* oder <em>user_name@domain.com</em>. Darüber hinaus können Sie festlegen, ob während der Verbindungsherstellung Anmeldeinformationen abgefragt werden, indem Sie die Option **Jedes Mal nachfragen**  auswählen.
3. Du kannst auch zusätzliche Optionen festlegen, indem du auf **Mehr anzeigen** tippst:
   - **Anzeigename**: Ein leicht zu merkender Name für den PC, mit dem Sie eine Verbindung herstellen. Sie können eine beliebige Zeichenfolge verwenden, aber wenn Sie keinen Anzeigenamen angeben, wird der Name des PC angezeigt.
   - **Gruppe**: Gib eine Gruppe an, damit deine Verbindungen später leichter auffindbar sind. Du kannst eine neue Gruppe hinzufügen, indem du auf **+** tippst oder einen Eintrag aus der Liste auswählst.
   - **Gateway**: Das Remotedesktopgateway, das du zum Herstellen einer Verbindung mit virtuellen Desktops, RemoteApp-Programmen und sitzungsbasierten Desktops in einem internen Unternehmensnetzwerk verwenden möchtest. Du erhältst die Informationen über das Gateway von deinem Systemadministrator.
   - **Mit Administratorsitzung verbinden**: Verwende diese Option, um eine Verbindung mit einer Konsolensitzung zum Verwalten eines Windows-Servers herzustellen.
   - **Maustasten tauschen**: Verwende diese Option, um die Funktionen der linken Maustaste und der rechten Maustaste zu tauschen. Das Tauschen der Maustasten ist erforderlich, wenn Sie einen PC verwenden, der für einen Linkshänder konfiguriert ist, Sie aber nur über eine Maus für Rechtshänder verfügen.
   - **Set my remote session resolution to** (Auflösung für Remotesitzung festlegen auf): Wähle die Auflösung aus, die du in der Sitzung verwenden möchtest. Mit **Choose for me** (Für mich auswählen) wird die Auflösung anhand der Größe des Clients festgelegt.
   - **Größe der Anzeige ändern**: Beim Auswählen einer hohen statischen Auflösung für die Sitzung können Sie diese Einstellung verwenden, um Elemente auf dem Bildschirm größer darzustellen und so die Lesbarkeit zu verbessern. Diese Einstellung gilt nur bei einer Verbindungsherstellung mit Windows 8.1 oder höher.
   - **Update the remote session resolution on resize** (Auflösung der Remotesitzung bei Größenänderung aktualisieren): Wenn diese Option aktiviert ist, aktualisiert der Client die Sitzungsauflösung dynamisch basierend auf der Größe des Clients. Diese Einstellung gilt nur bei einer Verbindungsherstellung mit Windows 8.1 oder höher.
   - **Zwischenablage**: Wenn diese Option aktiviert ist, kannst du Text und Bilder auf den bzw. vom Remote-PC kopieren.
   - **Audiowiedergabe**: Wähle das Gerät aus, das während der Remotesitzung für Audiodaten verwendet werden soll. Du kannst auswählen, ob Sound auf den lokalen Geräten, auf dem Remote-PC oder überhaupt nicht wiedergegeben werden soll.
   - **Audioaufzeichnung**: Wenn diese Option aktiviert ist, kannst du für Anwendungen auf dem Remote-PC ein lokales Mikrofon nutzen.
4. Tippen Sie auf **Speichern**.

Musst du diese Einstellungen bearbeiten? Tippe auf das Überlaufmenü ( **...** ) neben dem Namen des Desktops und dann auf **Bearbeiten**.

Möchtest du die Verbindung löschen? Tippe erneut auf das Überlaufmenü ( **...** ) und dann auf **Entfernen**.

### <a name="add-a-remote-resource"></a>Hinzufügen einer Remoteressource

Bei Remoteressourcen handelt es sich um RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops, die mithilfe von Remotedesktopdiensten von deinem Administrator veröffentlicht werden.

Gehe wie folgt vor, um eine Remoteressource hinzuzufügen:

1. Tippe auf dem Bildschirm „Connection Center“ auf **+ Hinzufügen** und dann auf **Remoteressourcen**.
2. Gib die **Feed-URL** ein, die du von deinem Administrator erhalten hast, und tippe auf **Find feeds** (Feeds suchen).
3. Geben Sie bei entsprechender Aufforderung die Anmeldeinformationen zum Abonnieren des Feeds an.

Die Remoteressourcen werden im Connection Center angezeigt.

Gehe wie folgt vor, um Remoteressourcen zu löschen:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben der Remoteressource.
2. Tippe auf **Entfernen**.

### <a name="pin-a-saved-desktop-to-your-start-menu"></a>Anheften eines gespeicherten Desktops an dein Startmenü

Tippe zum Anheften einer Verbindung an das Startmenü auf das Überlaufmenü ( **...** ) neben dem Namen des Desktops und dann auf **An „Start“ anheften**.

Jetzt kannst du die Remotedesktopverbindung direkt über das Startmenü starten, indem du darauf tippst.

## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>Herstellen einer Verbindung mit einem Remotedesktopgateway zum Zugreifen auf interne Ressourcen

Mit einem Remotedesktopgateway (RD-Gateway) können Sie eine Verbindung mit einem Remotecomputer in einem Unternehmensnetzwerk über das Internet herstellen. Sie können Ihre Gateways mit dem Remotedesktopclient erstellen und verwalten.

Gehe wie folgt vor, um ein neues Gateway einzurichten:

1. Tippe im Connection Center auf **Einstellungen**.
2. Tippe neben dem Gateway auf **+** , um ein neues Gateway hinzuzufügen.

      >[!NOTE]
      >Sie können ein Gateway auch beim Hinzufügen einer neuen Verbindung hinzufügen.

3. Geben Sie die folgenden Informationen ein:
   - **Servername**: Der Name des Computers, den Sie als Gateway verwenden möchten. Der Servername kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können dem Servernamen auch Portinformationen hinzufügen (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
   - **Benutzerkonto**: Wählen Sie ein Benutzerkonto für das Remotedesktopgateway aus (bzw. fügen Sie es hinzu), mit dem Sie eine Verbindung herstellen. Sie können auch die Option **Desktopbenutzerkonto verwenden** auswählen, damit die gleichen Anmeldeinformationen wie für die Remotedesktopverbindung verwendet werden.
4. Tippen Sie auf **Speichern**.

## <a name="global-app-settings"></a>Globale App-Einstellungen

Du kannst die folgenden globalen Einstellungen in deinem Client festlegen, indem du auf **Einstellungen** tippst:

### <a name="managed-items"></a>Verwaltete Elemente

- **Benutzerkonto**: Ermöglicht das Hinzufügen, Bearbeiten und Löschen von auf dem Client gespeicherten Benutzerkonten. Sie können das Kennwort für ein Konto auch aktualisieren, nachdem es geändert wurde.
- **Gateway**: Ermöglicht das Hinzufügen, Bearbeiten und Löschen von auf dem Client gespeicherten Gatewayservern.
- **Gruppe**: Ermöglicht das Hinzufügen, Bearbeiten und Löschen von auf dem Client gespeicherten Gruppen. Sie können hier auch Verbindungen gruppieren.

### <a name="session-settings"></a>Sitzungseinstellungen

- **Start connections in full screen** (Verbindungen im Vollbildmodus starten): Wenn diese Option aktiviert ist, verwendet der Client bei jedem Verbindungsstart den gesamten Bildschirm des aktuellen Monitors.
- **Start each connection in a new window** (Jede Verbindung in einem neuen Fenster starten): Wenn diese Option aktiviert ist, wird jede Verbindung in einem neuen Fenster gestartet. Du kannst sie auf unterschiedlichen Monitoren anordnen und über die Taskleiste dazwischen umschalten.
- **When resizing the app** (Beim Ändern der App-Größe): Ermöglicht die Steuerung der Vorgänge, die beim Ändern der Größe des Clientfensters ablaufen. Standardmäßig ist **Stretch the content, preserving aspect ratio** (Inhalt strecken, Seitenverhältnis beibehalten) festgelegt.
- **Tastaturbefehle verwenden mit**: Sie können angeben, wo Tastaturbefehle wie *WIN* oder *ALT+TAB-TASTE* verwendet werden. In der Standardeinstellung werden sie nur an die Sitzung gesendet, wenn die Verbindung im Vollbildmodus angezeigt wird.
- **Prevent the screen from timing out** (Timeout für Bildschirm verhindern): Ermöglicht die Verhinderung eines Timeouts, wenn eine Sitzung aktiv ist. Das Verhindern eines Timeouts ist hilfreich, wenn für die Verbindung keine Interaktionen von längerer Dauer benötigt werden.

### <a name="app-settings"></a>App-Einstellungen

- **Show Desktop Previews** (Desktopvorschauen anzeigen): Mit dieser Option kannst du eine Vorschau des Desktops im Connection Center anzeigen, bevor du eine Verbindung damit herstellst. Diese Einstellung ist standardmäßig eingeschaltet.
- **Help improve Remote Desktop** (Zur Verbesserung von Remotedesktop beitragen): Sendet anonyme Daten an Microsoft. Wir verwenden diese Daten, um den Client zu verbessern. Weitere Informationen dazu, wie wir mit diesen anonymen und privaten Daten umgehen, finden Sie unter [Datenschutzerklärung von Microsoft](https://privacy.microsoft.com/privacystatement). Diese Einstellung ist standardmäßig eingeschaltet.

### <a name="manage-your-user-accounts"></a>Verwalten Ihrer Benutzerkonten

Wenn Sie eine Verbindung mit einem Desktop oder mit Remoteressourcen herstellen, können Sie die Kontoinformationen für spätere Verbindungen speichern. Sie können auch Benutzerkonten auf dem Client definieren, anstatt die Benutzerdaten zu speichern, wenn Sie eine Verbindung mit einem Desktop herstellen.

Gehen Sie wie folgt vor, um ein neues Benutzerkonto zu erstellen:

1. Tippe im Connection Center auf **Einstellungen**.
2. Tippe neben dem Benutzerkonto auf **+** , um ein neues Benutzerkonto hinzuzufügen.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername**: Der Name des Benutzers, der zur Verwendung für eine Remoteverbindung gespeichert werden soll. Du kannst den Benutzernamen in einem der folgenden Formate eingeben: „user_name“, „domain\user_name“ oder user_name@domain.com.
   - **Kennwort**: Das Kennwort für den angegebenen Benutzer. Sie können dieses Feld leer lassen, damit bei der Verbindungsherstellung ein Kennwort abgefragt wird.
4. Tippen Sie auf **Speichern**.

Lösche ein Benutzerkonto wie folgt:

1. Tippe im Connection Center auf **Einstellungen**.
2. Wähle das zu löschende Konto in der Liste unter „Benutzerkonto“ aus.
3. Tippe neben „Benutzerkonto“ auf das Symbol „Bearbeiten“.
4. Tippe unten auf **Dieses Konto entfernen**, um das Benutzerkonto zu löschen.
5. Du kannst auch das Benutzerkonto bearbeiten und auf **Speichern** tippen.

## <a name="navigate-the-remote-desktop-session"></a>Navigieren in der Remotedesktopsitzung

Wenn du eine Remotedesktopverbindung startest, stehen Tools zur Verfügung, die du für die Navigation in der Sitzung verwenden kannst.

### <a name="start-a-remote-desktop-connection"></a>Starten einer Remotedesktopverbindung

1. Tippe auf die Remotedesktopverbindung, um die Sitzung zu starten.
2. Falls Sie für die Verbindung keine Anmeldeinformationen gespeichert haben, werden Sie zum Angeben eines **Benutzernamens** und eines **Kennworts** aufgefordert.
3. Gehen Sie bei einer Aufforderung zum Überprüfen des Zertifikats für den Remotedesktop wie folgt vor: Prüfen Sie die Informationen, und vergewissern Sie sich, dass Sie dem PC vertrauen, bevor Sie auf **Verbinden** tippen. Du kannst auch die Option **Don’t ask about this certificate again** (Nicht mehr nach diesem Zertifikat fragen) aktivieren, um anzugeben, dass dieses Zertifikat immer akzeptiert werden soll.

### <a name="connection-bar"></a>Verbindungsleiste

Die Verbindungsleiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente. Standardmäßig befindet sich die Verbindungsleiste in der Mitte am oberen Rand des Bildschirms. Tippe auf die Leiste, und ziehe sie nach links oder rechts, um sie zu verschieben.

- **Schwenken-Steuerelement**: Mit dem Schwenken-Steuerelement kann der Bildschirm vergrößert und verschoben werden. Das Schwenken-Steuerelement ist nur auf touchfähigen Geräten verfügbar und der Modus für die direkte Toucheingabe wird verwendet.
   - Um das Schwenken-Steuerelement zu aktivieren oder zu deaktivieren, tippen Sie auf der Verbindungsleiste auf das Schwenksymbol, um das Schwenken-Steuerelement anzuzeigen. Die Anzeige wird vergrößert, während das Schwenken-Steuerelement aktiv ist. Tippen Sie auf der Verbindungsleiste erneut auf das Schwenksymbol, um das Steuerelement auszublenden und die ursprüngliche Auflösung des Bildschirms wiederherzustellen.
   - Zum Verwenden des Schwenken-Steuerelements tippen Sie auf das Schwenken-Steuerelement, halten es gedrückt und ziehen es dann in die Richtung, in der Sie den Bildschirm verschieben möchten.
   - Zum Verschieben des Schwenken-Steuerelements doppeltippen Sie auf das Schwenken-Steuerelement, und halten Sie es gedrückt, um es auf dem Bildschirm zu verschieben.
- **Zusätzliche Optionen**: Tippen Sie auf das Symbol für zusätzliche Optionen, um die Auswahl- und die Befehlsleiste der Sitzung anzuzeigen.
- **Tastatur**: Tippe auf das Tastatursymbol, um die Bildschirmtastatur ein- oder auszublenden. Das Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur eingeblendet ist.

### <a name="command-bar"></a>Befehlsleiste

Tippen Sie auf der Verbindungsleiste auf **...** , um die Befehlsleiste rechts auf dem Bildschirm anzuzeigen.

- **Startseite**: Verwende die Schaltfläche „Startseite“, um von der Befehlsleiste zurück zum Connection Center zu wechseln.
  - Sie können für die gleiche Aktion auch die Schaltfläche „Zurück“ verwenden. Wenn Sie die Schaltfläche „Zurück“ verwenden, wird Ihre aktive Sitzung nicht getrennt, und Sie können weitere Verbindungen starten.
- **Trennen**: Verwenden Sie die Schaltfläche „Trennen“, um die Verbindung mit der Sitzung zu trennen. Ihre Apps bleiben so lange aktiv, bis die Sitzung auf dem Remote-PC beendet wird.
- **Vollbild**: Dient zum Aktivieren bzw. Deaktivieren des Vollbildmodus.
- **Touch oder Maus**: Hiermit können Sie zwischen den Mausmodi umschalten (direkte Toucheingabe und Mauszeiger).

### <a name="use-direct-touch-gestures-and-mouse-modes-in-a-remote-session"></a>Verwenden von direkten Touchgesten und Mausmodi in einer Remotesitzung

Für die Interaktion mit der Sitzung sind zwei Mausmodi verfügbar.

- **Direkte Toucheingabe**: Alle Berührungen werden an die Sitzung übergeben, damit sie remote interpretiert werden können.
  - Dies entspricht der Nutzung von Windows mit einem Touchscreen.
- **Mauszeiger**: Wandelt Ihren lokalen Touchscreen in ein großes Touchpad um, damit ein Mauszeiger in der Sitzung verschoben werden kann.
  - Dies entspricht der Nutzung von Windows mit einem Touchpad.

> [!NOTE]
> In Windows 8 oder höher werden die nativen Touchgesten im Modus für die direkte Touchbewegung unterstützt.

| Mausmodus    | Mausvorgang      | Geste                                                               |
|---------------|----------------------|-----------------------------------------------------------------------|
| Direkte Touchbewegung  | Linksklick           | Mit einem Finger tippen                                                          |
| Direkte Touchbewegung  | Klicken Sie mit der rechten Maustaste auf          | Tippen und mit einem Finger halten                                                |
| Mauszeiger | Linksklick           | Mit einem Finger tippen                                                          |
| Mauszeiger | Linksklick und ziehen  | Doppeltippen und mit einem Finger halten, dann ziehen                               |
| Mauszeiger | Klicken Sie mit der rechten Maustaste auf          | Mit zwei Fingern tippen                                                          |
| Mauszeiger | Rechtsklick und ziehen | Doppeltippen und mit zwei Fingern halten, dann ziehen                              |
| Mauszeiger | Mausrad          | Tippen und mit zwei Fingern halten, dann nach oben oder unten ziehen                          |
| Mauszeiger | Zoom                 | Zwei Finger zusammenführen, um die Ansicht zu vergrößern, oder auseinander bewegen, um sie zu verkleinern |

> [!TIP]
> Fragen und Kommentare sind immer willkommen. Wenn Sie Supportanfragen oder Produktfeedback jedoch im Kommentarbereich dieses Artikels posten, können wir nicht auf Ihr Feedback reagieren. Wenn Sie Hilfe benötigen oder Probleme mit Ihrem Client beheben möchten, empfehlen wir Ihnen dringend, das [Remotedesktopclient-Forum](/answers/topics/windows-remote-desktop-client.html) zu besuchen und einen neuen Thread zu starten. Wenn Sie eine Featureempfehlung geben möchten, können Sie uns dies im [Feedback-Hub](feedback-hub://?tabid=2&contextid=605) mitteilen.