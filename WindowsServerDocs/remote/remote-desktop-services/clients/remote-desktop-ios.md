---
title: Erste Schritte mit Remotedesktop auf iOS
description: Informationen Sie zum Einrichten des Remotedesktopclients für iOS
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03ec5a3d-d3f2-4afd-9405-ae58b6ecc91c
author: lizap
manager: dongill
ms.author: elizapo
date: 01/13/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a1939c7fd6d25d756369c85e4adaa6c15195b37
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889631"
---
# <a name="get-started-with-remote-desktop-on-ios"></a>Erste Schritte mit Remotedesktop auf iOS

>Gilt für: Windows 10, Windows 8.1, Windows Server 2012 R2, WindowsServer 2016

Sie können den Remotedesktopclient für iOS verwenden, zum Arbeiten mit Windows-apps, Ressourcen und Desktops über Ihr iOS-Gerät (iPhones und iPads).

Verwenden Sie die folgende Informationen, um zu beginnen. Achten Sie darauf, sehen Sie sich die [– häufig gestellte Fragen](remote-desktop-client-faq.md) , wenn Sie Fragen haben.

> [!NOTE]
> - Möchten Sie wissen zu den neuen Releases für die iOS-Client? Sehen Sie sich [für Remotedesktop unter iOS Neuigkeiten?](ios-whatsnew.md)
> - Das iOS-Client unterstützt Geräte mit iOS 6.x oder höher.

## <a name="get-the-remote-desktop-client-and-start-using-it"></a>Abrufen der Remotedesktop-Client, und verwenden

### <a name="download-the-remote-desktop-client-from-the-ios-store"></a>Der Remotedesktop-Client aus dem iOS-Store herunterladen
Um mit Remotedesktop auf Ihrem iOS-Gerät zu beginnen, gehen Sie wie folgt vor:

1. Laden Sie die Microsoft-Remotedesktop-Client aus [iTunes](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8).
2. [Richten Sie Ihren PC, um Remoteverbindungen](remote-desktop-client-faq.md#how-do-i-set-up-a-pc-for-remote-desktop).
3. Hinzufügen einer [Remotedesktopverbindung](#add-a-remote-desktop-connection) oder [Remoteressource](#add-a-remote-resource). Können Sie eine Verbindung herstellen einer Verbindung mit einem direkt auf einem Windows-PC ein RemoteApp-Programm verwendet werden und eine Remoteressource, sitzungsbasierten Desktop oder einem virtuellen Desktop veröffentlicht lokal mithilfe der RemoteApp- und Desktopverbindungen. Dieses Feature steht in der Regel in unternehmensumgebungen.

### <a name="download-the-remote-desktop-ios-beta-client"></a>Laden Sie den Remotedesktop-iOS-Beta-client
Führen Sie auf Ihrem iOS-Gerät [diese Anweisungen](https://aka.ms/rdiosbeta) der Remotedesktop-iOS-Beta-Client herunterladen.

### <a name="add-a-remote-desktop-connection"></a>Fügen Sie eine Remotedesktopverbindung

So erstellen Sie eine Remotedesktopverbindung 
1. In das Connection Center Tap **+**, und tippen Sie dann auf **hinzufügen PC oder Server**.
2. Geben Sie die folgende Informationen für die Remotedesktopverbindung aus:
  - **PC-Namen** – der Name des Computers. Dies kann es sich um einen Windows-Computernamen, einen Internet-Domänennamen oder eine IP-Adresse sein. Sie können auch die Portinformationen anfügen, auf den PC-Namen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**).
  - **Benutzername** – den Benutzernamen ein, die auf einem Remotecomputer verwenden. Sie können die folgenden Formate verwenden: *User_name*, *Domäne\Benutzername*, oder *user_name@domain.com*. Sie können auch angeben, ob Benutzername und Kennwort aufgefordert.
3. Sie können auch die folgenden zusätzlichen Optionen festlegen:
  - **Anzeigename (optional)** – ein leicht zu merkenden Namen für den PC mit dem Sie eine Verbindung mit. Sie können eine beliebige Zeichenfolge verwenden, aber der PC-Name wird angezeigt, wenn Sie einen Anzeigenamen nicht angeben, aus.
  - **(Optional) Gateway** – die Remotedesktop-Gateway, das Sie Verbindung mit virtuellen Desktops, RemoteApp-Programmen und sitzungsbasierten Desktops in einem internen Unternehmensnetzwerk herstellen möchten. Rufen Sie Informationen über das Gateway von Ihrem Systemadministrator an.
  - **Sound** – wählen Sie das Gerät für Audio während der Remotesitzung verwenden. Sie können auswählen, um auf den lokalen Geräten, dem Remotegerät oder überhaupt nicht Systemsound wiederzugeben.
  - **Austauschen der Maustasten** – Wenn eine mausbewegung einen Befehl mit der linken Maustaste sendet, sendet er stattdessen den gleichen Befehl mit der rechten Maustaste. Dies ist erforderlich, wenn der remote-PC für Linkshänder mausmodus konfiguriert ist.
  - **Administratormodus** : Verbinden einer Sitzung für die Verwaltung auf einem Server mit WindowsServer 2003 oder höher.
4. Tippen Sie auf **speichern**.

Möchten Sie diese Einstellungen zu bearbeiten? Drücken Sie und halten Sie den Desktop, die, den Sie bearbeiten möchten, und tippen Sie dann auf das Symbol "Einstellungen". 

### <a name="add-a-remote-resource"></a>Hinzufügen einer Remoteressource
Remote-Ressourcen sind die RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops mithilfe der RemoteApp- und Desktopverbindungen veröffentlicht.

- Die URL wird die Verknüpfung mit dem Web Access für Remotedesktop-Server, der Sie Zugriff auf RemoteApp- und Desktopverbindungen erhalten.
- Die konfigurierten RemoteApp- und Desktopverbindungen werden aufgeführt.

So fügen Sie eine Remoteressource hinzu:

1. Tippen Sie auf dem Bildschirm "Connection Center" auf **+**, und tippen Sie dann auf **Remoteressourcen hinzufügen**. 
2. Geben Sie Informationen für die Remoteressource:
   - **Feed-URL** -die URL der Web Access für Remotedesktop-Server. Ihr Unternehmens-e-Mail-Konto auch in dieses Feld eingegeben werden können, weist diese den Client, suchen Sie für den RD-Web-Server Ihre e-Mail-Adresse zugeordnet.
   - **Benutzername** -den Benutzernamen ein, für den Web Access für Remotedesktop-Server verwenden Sie eine Verbindung herstellen.
   - **Kennwort** -das Kennwort für den Web Access für Remotedesktop-Server hergestellt.
3. Tippen Sie auf **speichern**.

Der remote-Ressourcen werden im Connection Center angezeigt.


## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>Verbinden Sie mit einem RD-Gateway auf interne Ressourcen zugreifen

Ein Remotedesktopgateway (RD-Gateway) können Sie die Verbindung mit einem Remotecomputer in einem Unternehmensnetzwerk von überall aus im Internet. Sie können erstellen und verwalten Ihre Gateways mit dem Remotedesktop-Client.

So richten ein neues Gateway:

1. Tippen Sie in das Connection Center, auf **Einstellungen > Gateways**. 
2. Tippen Sie auf **Hinzufügen eines remotedesktopgateways**.
3. Geben Sie die folgende Informationen ein:
  - **Servername** – der Name des Computers als Gateway verwenden möchten. Dies kann es sich um einen Windows-Computernamen, einen Internet-Domänennamen oder eine IP-Adresse sein. Sie können auch Informationen hinzufügen, um den Namen des Servers (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
  - **Benutzername** -den Benutzernamen und Kennwort ein, das für den Remotedesktop-Gateway hergestellt. Sie können auch auswählen, **verwenden Sie die Anmeldeinformationen für die Verbindung** den gleichen Benutzernamen und das Kennwort wie für die Remotedesktopverbindung verwenden.


## <a name="manage-your-user-accounts"></a>Verwalten Sie Ihre Benutzerkonten 

Wenn Sie auf einem Desktop- oder remote-Ressourcen verbinden, können Sie die Benutzerkonten erneut aus speichern. Sie können Ihre Benutzerkonten verwalten, mit dem Remotedesktop-Client.

So erstellen Sie ein neues Benutzerkonto:

1. Tippen Sie in das Connection Center, auf **Einstellungen**, und tippen Sie dann auf **Benutzernamen**.
2. Tippen Sie auf **Benutzerkonto hinzufügen**.
3. Geben Sie die folgende Informationen ein:
   - **Benutzername** -der Name des Benutzers, der für die Verwendung mit einer remote-Verbindung zu speichern. Sie können den Benutzernamen eingeben, in einem der folgenden Formate: Domäne\Benutzername, User_name oder user_name@domain.com.
   - **Kennwort** -das Kennwort für den Benutzer, die Sie angegeben haben. Jedes Benutzerkonto, das Sie speichern, um für Remoteverbindungen verwenden möchten, muss ein Kennwort zugeordnet.
4. Tippen Sie auf **speichern**, und tippen Sie dann auf **Einstellungen**.
5. Tippen Sie auf **Fertig** um die neue Konfiguration zu speichern.

So löschen Sie ein Benutzerkonto

1. Tippen Sie in das Connection Center, auf **Einstellungen > Benutzernamen**.
2. Streichen Sie nach der Zeile von rechts nach links, um den Benutzer auszuwählen.
3. Tippen Sie auf **löschen**.



## <a name="navigate-the-remote-desktop-session"></a>Navigieren Sie von der Remotedesktopsitzung
Wenn Sie eine Remotedesktopsitzung starten, gibt es Tools zur Verfügung, Sie verwenden können, um die Sitzung zu navigieren.

### <a name="start-a-remote-desktop-connection"></a>Starten Sie eine Remotedesktopverbindung

1. Tippen Sie auf die Remotedesktopverbindung zum Starten der Remotedesktopsitzung. 
2. Wenn Sie aufgefordert werden, um zu überprüfen, ob das Zertifikat für den Remotedesktop, tippen Sie auf **Accept**. Sie können auch immer annehmen, indem er mit der **nicht mehr nachfragen für Verbindungen mit diesem Computer** wechseln **ON**. 

### <a name="connection-bar"></a>Verbindungsleiste

Die Verbindung Leiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente. 

- **Schwenken-Steuerelement**: Das Schwenksteuerelement ermöglicht es sich um den Bildschirm vergrößert und verschoben werden. Beachten Sie, dass Pan-Steuerelement ist nur verfügbar, die mithilfe von direkten Touch.
   - Aktivieren Sie bzw. deaktivieren Sie die Pan-Steuerelement: Tippen Sie auf das schwenksymbol, in der Verbindungsleiste "zum Anzeigen des Steuerelements Schwenken und vergrößern den Bildschirm. Tippen Sie auf das schwenksymbol in die Symbolleiste für die Verbindung erneut aus, um das Steuerelement wird ausgeblendet, und den Bildschirm an seiner ursprünglichen Auflösung zurückgeben.
   - Verwenden Sie die Pan-Steuerelement: Tippen Sie auf halten Sie das Schwenken STRG gedrückt und ziehen Sie dann in die Richtung auf den Bildschirm verschoben werden soll.
   - Verschieben Sie die Pan-Steuerelement: Doppelte Tippen Sie und halten Sie die Pan-Steuerelement auf das Steuerelement auf dem Bildschirm verschoben werden.
- **Verbindungsname**: Der Verbindungsname der aktuellen wird angezeigt. Tippen Sie auf den Verbindungsnamen, um die Leiste Sitzung anzuzeigen.
- **Tastatur**: Tippen Sie auf das Symbol "Tastatur" zum Anzeigen oder Ausblenden der Tastaturfokus. Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur angezeigt wird.
- **Verschieben Sie die Symbolleiste Verbindung**: Tippen Sie auf und enthalten Verbindungsleiste, und klicken Sie dann Drag & drop an eine neue Position am oberen Rand des Bildschirms.

### <a name="session-selection"></a>Auswahl der Sitzung
Sie können mehrere Verbindungen, die auf anderen PCs gleichzeitig geöffnet haben. Tippen Sie auf die Symbolleiste Verbindung, um die Sitzung Leiste auf der linken Seite des Bildschirms angezeigt. Die Sitzung Leiste können Sie Ihre geöffneten Verbindungen anzeigen und zwischen diesen wechseln. 

- Wechseln Sie zwischen apps in einer Sitzung remote Ressource öffnen.

    Wenn Sie mit den Remoteressourcen verbunden sind, können Sie zwischen Anwendungen innerhalb dieser Sitzung durch Tippen auf das Menü "Expander", und wählen Sie aus der Liste der verfügbaren Elemente öffnen wechseln.
- Eine neue Sitzung starten

  Sie können neue Anwendungen oder Remotedesktopsitzungen aus starten, innerhalb der aktuellen Verbindung: Tippen Sie auf **starten neue**, und wählen Sie dann aus der Liste der verfügbaren Elemente.

- Trennen einer Sitzung

  Um eine Sitzung tippen X in der linken Seite der Kachel Sitzung zu trennen.

### <a name="command-bar"></a>Befehlsleiste

Die Befehlsleiste ersetzt das Dienstprogramm Leiste ab Version 8.0.1. Wechseln Sie zwischen den Modi für die Maus und zurück an das Rechenzentrum für die Verbindung in der Befehlsleiste.

## <a name="use-touch-gestures-and-mouse-modes-in-a-remote-session"></a>Verwenden Sie in einer Remotesitzung Fingereingabe und gerätedrehung Maus-Modi

Der Client verwendet die standard Touchgesten. Sie können auch Touchgesten verwenden, um Aktionen auf dem Remotedesktop zu replizieren. Die Mauszeiger-Modi zur Verfügung, werden in der folgenden Tabelle definiert.

> [!NOTE]
> Interaktion mit Windows 8 oder höher werden die systemeigenen Touchgesten in Direct Touch-Modus unterstützt. Weitere Informationen zu Windows 8 finden Sie unter Gesten [Touch: Wischen, tippen Sie auf, und darüber hinaus](https://windows.microsoft.com/en-US/windows-8/touch-swipe-tap-beyond).

| Mausmodus    | Mausvorgang      | Geste                                                    |
|---------------|----------------------|------------------------------------------------------------|
| Direct touch  | Linksklick           | 1 Finger tap                                               |
| Direct touch  | Rechtsklick          | 1 Finger tippen und halten                                      |
| Mauszeiger | Linksklick           | 1 Finger tap                                               |
| Mauszeiger | Linksklick und ziehen  | Doppeltippen 1 Finger, und halten, ziehen Sie dann                    |
| Mauszeiger | Rechtsklick          | 2 Finger tap                                               |
| Mauszeiger | Rechtsklick und ziehen | 2 Finger Doppeltippen und halten, ziehen Sie dann                    |
| Mauszeiger | Mausrad          | 2 Finger tippen und halten, und ziehen Sie dann nach oben oder unten                |
| Mauszeiger | Zoom                 | Zusammendrücken Sie 2 Finger zum Vergrößern und verteilt 2 Finger zum Verkleinern |

## <a name="supported-input-devices"></a>Unterstützte Eingabegeräte

Die [iOS Beta Remotedesktopclient](https://aka.ms/rdiosbeta) unterstützt die Swiftpoint GT und ProPoint physischen Mäuse. Swiftpoint Angebot ist ein [exklusiven Rabatt](https://www.swiftpoint.com/microsoft/) auf GT für iOS-Beta-Client-Benutzer.

Das iOS-Client unterstützt derzeit nur Swiftpoint Mäuse. Finden Sie in der [Neuigkeiten in der iOS-Client](ios-whatsnew.md) Seite und die [iOS App Store](https://aka.ms/rdios) für Nachrichten über die Unterstützung von anderen Geräten in der Zukunft.

## <a name="use-a-keyboard-in-a-remote-session"></a>Verwenden Sie eine Tastatur in einer Remotesitzung

Verwenden Sie entweder einen auf dem Bildschirm Tastatur oder physische Tastatur in der Remotesitzung.

Für auf dem Bildschirm Tastaturen, verwenden Sie die Schaltfläche am rechten Rand des Balkens über die Tastatur der standard sowie zusätzliche Tastatur wechseln.

Wenn für Ihr iOS-Gerät Bluetooth aktiviert ist, erkennt der Client automatisch die Bluetooth-Tastatur.

Denken Sie daran, dass aufgrund von Beschränkungen im Betriebssystem spezielle Schlüssel wie z. B. STRG, Option und -Funktion nicht erwartungsgemäß funktioniert mit einer Bluetooth-Tastatur. Arbeiten Sie die folgenden Schlüssel:

- Alphanumerische Schlüssel
- Pfeiltasten
- Registerkarte ": Registerkarte funktioniert, aber die Tab-Taste funktioniert nicht
- Start / Pos1: ALT + nach-links = Home
- Ende: ALT + nach-rechts = Ende
- Bild-auf: ALT + nach-oben = Bild-auf
- Seite nach unten ALT + nach-unten = Bild-ab
- Wählen Sie alle: Befehl + A = STRG + A (auf alle in den meisten Programmen)
- Schneiden Sie aus: Befehl + X = STRG + X (Ausschneiden in den meisten Programmen)
- Kopieren: Befehl + C = STRG + C (Kopieren in den meisten Programmen)
- Fügen Sie: Befehl + V = STRG + V (Fügen Sie in den meisten Programmen)
- Symbole: ALT + alphanumerisch Schlüssel erzeugt andere Symbole, abhängig von der Sprache konfiguriert

> [!TIP]
> Fragen und Kommentare sind immer Willkommen. Allerdings Supportfragen Sie keine Anforderung für die Hilfe zur Problembehandlung, indem Sie über die Kommentarfunktion am Ende dieses Artikels. Wechseln Sie stattdessen zu den [Remotedesktop-Client-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc) und einen neuen Thread starten. Haben Sie Vorschläge Feature? Teilen Sie uns in die [Client User Voice-Forum](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android).

