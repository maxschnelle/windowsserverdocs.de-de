---
title: Erste Schritte mit dem Windows Store-Client
description: Enthält grundlegende Einrichtungsschritte für den Remotedesktopclient für Windows Store.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 64f038e1-40ec-4c67-938b-72edea49e5d8
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/27/2019
ms.localizationpriority: medium
ms.openlocfilehash: 64362c6f6da77ee15a95ddcbaf33c6cb9ecd5cf4
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80861433"
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

1. Tippe im Connection Center auf **+ Hinzufügen** und dann auf **Desktop**.
2. Gib die folgenden Informationen für den Computer ein, mit dem du eine Verbindung herstellen möchtest:
   - **PC-Name**: Der Name des Computers. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Du kannst auch Portinformationen an den PC-Namen anfügen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**).
   - **Benutzerkonto**: Das Benutzerkonto zum Zugreifen auf den Remote-PC. Tippe auf **+** , um ein neues Konto hinzuzufügen oder ein vorhandenes Konto auszuwählen. Du kannst die folgenden Formate für den Benutzernamen verwenden: *user_name*, *domain\user_name* oder <em>user_name@domain.com</em>. Darüber hinaus kannst du angeben, ob während der Verbindungsherstellung ein Benutzername und das zugehörige Kennwort abgefragt werden können, indem du die Option **Jedes Mal nachfragen**  wählst.
3. Du kannst auch zusätzliche Optionen festlegen, indem du auf **Mehr anzeigen** tippst:
   - **Anzeigename**: Ein leicht zu merkender Name für den PC, mit dem du eine Verbindung herstellst. Du kannst eine beliebige Zeichenfolge verwenden. Wenn du keinen Anzeigenamen angibst, wird der PC-Name angezeigt.
   - **Gruppe**: Gib eine Gruppe an, damit deine Verbindungen später leichter auffindbar sind. Du kannst eine neue Gruppe hinzufügen, indem du auf **+** tippst oder einen Eintrag aus der Liste auswählst.
   - **Gateway**: Das Remotedesktopgateway, das du zum Herstellen einer Verbindung mit virtuellen Desktops, RemoteApp-Programmen und sitzungsbasierten Desktops in einem internen Unternehmensnetzwerk verwenden möchtest. Du erhältst die Informationen über das Gateway von deinem Systemadministrator.
   - **Mit Administratorsitzung verbinden**: Verwende diese Option, um eine Verbindung mit einer Konsolensitzung zum Verwalten eines Windows-Servers herzustellen.
   - **Maustasten tauschen**: Verwende diese Option, um die Funktionen der linken Maustaste und der rechten Maustaste zu tauschen. (Dies ist besonders nützlich, wenn der Remote-PC für Linkshänder konfiguriert ist, du aber eine Maus für Rechtshänder verwendest.)
   - **Set my remote session resolution to** (Auflösung für Remotesitzung festlegen auf): Wähle die Auflösung aus, die du in der Sitzung verwenden möchtest. Mit **Choose for me** (Für mich auswählen) wird die Auflösung anhand der Größe des Clients festgelegt.
   - **Größe der Anzeige ändern**: Beim Auswählen einer hohen statischen Auflösung für die Sitzung hast du die Option, Elemente auf dem Bildschirm größer darzustellen, um die Lesbarkeit zu verbessern. Hinweis: Dies gilt nur bei einer Verbindungsherstellung mit Windows 8.1 oder höher.
   - **Update the remote session resolution on resize** (Auflösung der Remotesitzung bei Größenänderung aktualisieren): Wenn diese Option aktiviert ist, aktualisiert der Client die Sitzungsauflösung dynamisch basierend auf der Größe des Clients. Hinweis: Dies gilt nur bei einer Verbindungsherstellung mit Windows 8.1 oder höher.
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
3. Gib bei entsprechender Aufforderung die Anmeldeinformationen an, die zum Abonnieren des Feeds verwendet werden sollen.

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
2. Tippe neben dem Gateway auf **+** , um ein neues Gateway hinzuzufügen. Hinweis: Ein Gateway kann auch beim Hinzufügen einer neuen Verbindung hinzugefügt werden.
3. Gib die folgenden Informationen ein:
   - **Servername**: Der Name des Computers, den Sie als Gateway verwenden möchten. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können dem Servernamen auch Portinformationen hinzufügen (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
   - **Benutzerkonto**: Wähle ein Benutzerkonto für das Remotedesktopgateway aus (bzw. füge es hinzu), mit dem du eine Verbindung herstellst. Du kannst auch die Option **Desktopbenutzerkonto verwenden** wählen, damit die gleichen Anmeldeinformationen wie für die Remotedesktopverbindung verwendet werden.
4. Tippe auf **Speichern**.  

## <a name="global-app-settings"></a>Globale App-Einstellungen

Du kannst die folgenden globalen Einstellungen in deinem Client festlegen, indem du auf **Einstellungen** tippst:

VERWALTETE ELEMENTE

- **Benutzerkonto**: Ermöglicht das Hinzufügen, Bearbeiten und Löschen von auf dem Client gespeicherten Benutzerkonten. Dies ist eine gute Möglichkeit, das Kennwort für ein Konto zu aktualisieren, nachdem es geändert wurde.
- **Gateway**: Ermöglicht das Hinzufügen, Bearbeiten und Löschen von auf dem Client gespeicherten Gatewayservern.
- **Gruppe**: Ermöglicht das Hinzufügen, Bearbeiten und Löschen von auf dem Client gespeicherten Gruppen. Diese werden zum einfachen Gruppieren von Verbindungen genutzt.

SITZUNGSEINSTELLUNGEN

- **Start connections in full screen** (Verbindungen im Vollbildmodus starten): Wenn diese Option aktiviert ist, verwendet der Client bei jedem Verbindungsstart den gesamten Bildschirm des aktuellen Monitors.
- **Start each connection in a new window** (Jede Verbindung in einem neuen Fenster starten): Wenn diese Option aktiviert ist, wird jede Verbindung in einem neuen Fenster gestartet. Du kannst sie auf unterschiedlichen Monitoren anordnen und über die Taskleiste dazwischen umschalten.
- **When resizing the app** (Beim Ändern der App-Größe): Ermöglicht die Steuerung der Vorgänge, die beim Ändern der Größe des Clientfensters ablaufen. Standardmäßig ist **Stretch the content, preserving aspect ratio** (Inhalt strecken, Seitenverhältnis beibehalten) festgelegt.
- **Use keyboard commands with** (Tastaturbefehle verwenden mit): Du kannst angeben, wo Tastaturbefehle wie *WIN* oder *ALT+TAB-TASTE* verwendet werden. In der Standardeinstellung werden sie nur an die Sitzung gesendet, wenn die Verbindung im Vollbildmodus angezeigt wird.
- **Prevent the screen from timing out** (Timeout für Bildschirm verhindern): Ermöglicht die Verhinderung eines Timeouts, wenn eine Sitzung aktiv ist. Dies ist hilfreich, wenn für die Verbindung keine Interaktionen von längerer Dauer benötigt werden.

APP-EINSTELLUNGEN

- **Show Desktop Previews** (Desktopvorschauen anzeigen): Mit dieser Option kannst du eine Vorschau des Desktops im Connection Center anzeigen, bevor du eine Verbindung damit herstellst. Diese Option ist standardmäßig auf **Ein** festgelegt.
- **Help improve Remote Desktop** (Zur Verbesserung von Remotedesktop beitragen): Sendet anonyme Daten an Microsoft. Wir verwenden diese Daten, um den Client zu verbessern. Weitere Informationen dazu, wie wir mit diesen anonymen privaten Daten umgehen, findest du unter [Datenschutzerklärung von Microsoft](https://privacy.microsoft.com/en-us/privacystatement). Diese Einstellung ist standardmäßig auf **Ein** festgelegt.

### <a name="manage-your-user-accounts"></a>Verwalten von Benutzerkonten

Wenn du eine Verbindung mit einem Desktop oder mit Remoteressourcen herstellst, kannst du die Benutzerkonten speichern, um sie erneut auswählen zu können. Du kannst auch Benutzerkonten auf dem Client selbst definieren, anstatt die Benutzerdaten zu speichern, wenn du eine Verbindung mit einem Desktop herstellst.

Erstelle wie folgt ein neues Benutzerkonto:

1. Tippe im Connection Center auf **Einstellungen**.
2. Tippe neben dem Benutzerkonto auf **+** , um ein neues Benutzerkonto hinzuzufügen.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername**: Der Name des Benutzers, der zur Verwendung für eine Remoteverbindung gespeichert werden soll. Du kannst den Benutzernamen in einem der folgenden Formate eingeben: „user_name“, „domain\user_name“ oder user_name@domain.com.
   - **Kennwort**: Das Kennwort für den angegebenen Benutzer. Du kannst diese Option leer lassen, damit bei der Verbindungsherstellung ein Kennwort abgefragt wird.
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
2. Falls du für die Verbindung keine Anmeldeinformationen gespeichert hast, wirst du zum Angeben eines **Benutzernamens** und eines **Kennworts** aufgefordert.
3. Gehe bei einer Aufforderung zum Überprüfen des Zertifikats für den Remotedesktop wie folgt vor: Prüfe die Informationen, und vergewissere dich, dass es sich um einen vertrauenswürdigen PC handelt, bevor du auf **Verbinden** tippst. Du kannst auch die Option **Don’t ask about this certificate again** (Nicht mehr nach diesem Zertifikat fragen) aktivieren, um anzugeben, dass dieses Zertifikat immer akzeptiert werden soll.

### <a name="connection-bar"></a>Verbindungsleiste

Die Verbindungsleiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente. Standardmäßig befindet sich die Verbindungsleiste in der Mitte am oberen Rand des Bildschirms. Tippe auf die Leiste, und ziehe sie nach links oder rechts, um sie zu verschieben.

- **Schwenken-Steuerelement**: Mit dem Schwenken-Steuerelement kann der Bildschirm vergrößert und verschoben werden. Beachte, dass das Schwenken-Steuerelement nur auf touchfähigen Geräten verfügbar ist und dass der Modus für die direkte Toucheingabe verwendet wird.
   - Aktivieren/Deaktivieren des Schwenken-Steuerelements: Tippen Sie auf der Verbindungsleiste auf das Schwenksymbol, um das Schwenken-Steuerelement anzuzeigen und den Bildschirm zu vergrößern. Tippe auf der Verbindungsleiste erneut auf das Schwenksymbol, um das Steuerelement auszublenden und die ursprüngliche Auflösung des Bildschirms wiederherzustellen.
   - Verwenden des Schwenken-Steuerelements: Tippe auf das Schwenken-Steuerelement, halte es gedrückt, und ziehe es dann in die Richtung, in der du den Bildschirm verschieben möchtest.
   - Verschieben des Schwenken-Steuerelements: Doppeltippe auf das Schwenken-Steuerelement, und halte es gedrückt, um es auf dem Bildschirm zu verschieben.
- **Zusätzliche Optionen**: Tippe auf das Symbol für zusätzliche Optionen, um die Auswahl- und die Befehlsleiste (siehe unten) der Sitzung anzuzeigen.
- **Tastatur**: Tippe auf das Tastatursymbol, um die Bildschirmtastatur ein- oder auszublenden. Das Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur eingeblendet ist.

### <a name="command-bar"></a>Befehlsleiste

Tippe auf der Verbindungsleiste auf **...** , um die Befehlsleiste rechts auf dem Bildschirm anzuzeigen.

- **Startseite**: Verwende die Schaltfläche „Startseite“, um von der Befehlsleiste zurück zum Connection Center zu wechseln.
  - Alternativ kannst du hierfür auch die Schaltfläche „Zurück“ verwenden.
  - Die Verbindung deiner aktiven Sitzung wird nicht getrennt.
  - So hast du die Möglichkeit, weitere Verbindungen zu starten.
- **Trennen**: Verwende die Schaltfläche „Trennen“, um die Verbindung zu beenden.
  - Deine Apps bleiben so lange aktiv, bis die Sitzung auf dem Remote-PC beendet wird.
- **Vollbild**: Dient zum Aktivieren bzw. Deaktivieren des Vollbildmodus.
- **Touch/Maus**: Hiermit kannst du zwischen den Mausmodi umschalten (direkte Toucheingabe und Mauszeiger).

### <a name="use-direct-touch-gestures-and-mouse-modes-in-a-remote-session"></a>Verwenden von Gesten für die direkte Toucheingabe und Mausmodi in einer Remotesitzung

Für die Interaktion mit der Sitzung sind zwei Mausmodi verfügbar.

- **Direkte Toucheingabe**: Alle Berührungen werden an die Sitzung übergeben, damit sie remote interpretiert werden können.
  - Dies entspricht der Nutzung von Windows mit einem Touchscreen.
- **Mauszeiger**: Wandelt deinen lokalen Touchscreen in ein großes Touchpad um, damit ein Mauszeiger in der Sitzung verschoben werden kann.
  - Dies entspricht der Nutzung von Windows mit einem Touchpad.

> [!NOTE]
> Bei der Interaktion mit Windows 8 oder höher werden die nativen Touchgesten im Modus für die direkte Touchbewegung unterstützt.

| Mausmodus    | Mausvorgang      | Geste                                                               |
|---------------|----------------------|-----------------------------------------------------------------------|
| Direkte Touchbewegung  | Linksklick           | Mit einem Finger tippen                                                          |
| Direkte Touchbewegung  | Rechtsklick          | Mit einem Finger tippen und halten                                                 |
| Mauszeiger | Linksklick           | Mit einem Finger tippen                                                          |
| Mauszeiger | Linksklick und ziehen  | Mit einem Finger doppeltippen und halten, dann ziehen                               |
| Mauszeiger | Rechtsklick          | Mit zwei Fingern tippen                                                          |
| Mauszeiger | Rechtsklick und ziehen | Mit zwei Fingern doppeltippen und halten, dann ziehen                               |
| Mauszeiger | Mausrad          | Mit zwei Fingern tippen und halten, dann nach oben oder unten ziehen                           |
| Mauszeiger | Zoom                 | Zwei Finger zusammenführen, um die Ansicht zu vergrößern, oder auseinander, um sie zu verkleinern. |

> [!TIP]
> Fragen und Kommentare sind immer willkommen. Verwenden Sie jedoch NICHT die Kommentarfunktion am Ende dieses Artikels, um Hilfe bei der Problembehandlung anzufordern. Verwenden Sie stattdessen das [Remotedesktopclient-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc), und erstellen Sie einen neuen Thread. Hast du einen Vorschlag für ein Feature? Teile uns den Vorschlag über den [Feedback-Hub](feedback-hub://?tabid=2&contextid=605) mit.
