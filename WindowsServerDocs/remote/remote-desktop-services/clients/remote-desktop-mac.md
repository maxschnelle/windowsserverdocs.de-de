---
title: Erste Schritte mit dem macOS-Client
description: Informationen zum Einrichten des Remotedesktopclients für Mac
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 7afc65f8-3158-49c9-9d48-4dab1c69afba
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 07/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7be6b7542ca77c80a638df6404aefe77d8d7d19c
ms.sourcegitcommit: b363d8ceed863c8fd5a464bc8afdc4ef1af9a6f8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86445704"
---
# <a name="get-started-with-the-macos-client"></a>Erste Schritte mit dem macOS-Client

>Gilt für: Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2016

Sie können den Remotedesktopclient für Mac verwenden, um mit Windows-Apps, -Ressourcen und -Desktops auf Ihrem Mac zu arbeiten. Verwenden Sie die folgenden Informationen für die ersten Schritte, und lesen Sie die [häufig gestellten Fragen](remote-desktop-client-faq.md), wenn Sie Fragen haben.

>[!NOTE]
> - Möchten Sie mehr über die neuen Versionen für den macOS-Client erfahren? Lesen Sie [Neuerungen bei Remotedesktop unter Mac](mac-whatsnew.md).
> - Der Mac-Client wird auf Computern unter macOS 10.10 oder höher ausgeführt.
> - Die Informationen in diesem Artikel beziehen sich in erster Linie auf die Vollversion des Mac-Clients – die im Mac App Store verfügbare Version. Testen Sie neue Features, indem Sie unsere Vorschau-App hier herunterladen: [Beta-Client – Anmerkungen zu dieser Version](https://go.microsoft.com/fwlink/?LinkID=619698&clcid=0x409).

## <a name="get-the-remote-desktop-client"></a>Abrufen des Remotedesktopclients

Führen Sie die folgenden Schritte für den Einstieg in Remotedesktop auf Ihrem Mac aus:

1. Laden Sie den Microsoft-Remotedesktopclient aus dem [Mac App Store](https://itunes.apple.com/app/microsoft-remote-desktop/id1295203466?mt=12) herunter.
2. [Richten Sie Ihren PC so ein, dass Remoteverbindungen zulässig sind](remote-desktop-client-faq.md#how-do-i-set-up-a-pc-for-remote-desktop). (Wenn Sie diesen Schritt überspringen, können Sie keine Verbindung mit Ihrem PC herstellen.)
3. Fügen Sie eine Remotedesktopverbindung oder eine Remoteressource hinzu. Mit einer Verbindung können Sie eine direkte Verbindung mit einem Windows-PC herstellen, und mit einer Remoteressource können Sie ein RemoteApp-Programm, einen sitzungsbasierten Desktop oder einen virtuellen Desktop verwenden, das/der mithilfe von RemoteApp- und Desktopverbindungen veröffentlicht wird. Dieses Feature ist in der Regel in Unternehmensumgebungen verfügbar.

## <a name="what-about-the-mac-beta-client"></a>Informationen zum Mac-Beta-Client

Wir testen neue Features auf unserem Vorschaukanal auf AppCenter. Möchten Sie das ausprobieren? Wechsele zu [Microsoft-Remotedesktop für Mac](https://aka.ms/rdmacbeta), und wähle **Herunterladen** aus. Du musst kein Konto erstellen oder dich bei AppCenter anmelden, um den Beta-Client herunterladen zu können.

Wenn Sie bereits über den Client verfügen, können Sie nach Updates suchen, um sicherzustellen, dass Sie die neueste Version verwenden. Wähle im Betaclient oben **Microsoft-Remotedesktop Beta** und dann **Nach Updates suchen** aus. 

## <a name="add-a-workspace"></a>Hinzufügen eines Arbeitsbereichs

Abonniere den Feed, den du vom Administrator erhalten hast, um die Liste der verwalteten Ressourcen abzurufen, die auf deinem macOS-Gerät zur Verfügung stehen.

So abonnierst du einen Feed

1. Wähle auf der Hauptseite **Feed hinzufügen** aus, um eine Verbindung mit dem Dienst herzustellen und deine Ressourcen abzurufen.
2. Gib die Feed-URL ein. Dies kann eine URL oder eine E-Mail-Adresse sein:
   - Diese URL ist normalerweise eine Windows Virtual Desktop-URL. Welche URL Sie verwenden, hängt von Ihrer Windows Virtual Desktop-Version ab.
      - Für die Fall 2019-Version verwenden Sie `https://rdweb.wvd.microsoft.com/api/feeddiscovery/webfeeddiscovery.aspx`.
      - Für die Spring 2020-Version verwenden Sie `https://rdweb.wvd.microsoft.com/api/arm/feeddiscovery`.
   - Um E-Mail zu verwenden, gib deine E-Mail-Adresse ein. Dies weist den Client an, nach einer URL zu suchen, die deiner E-Mail-Adresse zugeordnet ist, sofern der Administrator dies entsprechend konfiguriert hat.
3. Wähle **Abonnieren** aus.
4. Melde dich bei entsprechender Aufforderung mit deinem Benutzerkonto an.

Nachdem du dich angemeldet hast, sollte eine Liste der verfügbaren Ressourcen angezeigt werden.

Nachdem du einen Feed abonniert hast, wird der Inhalt dieses Feeds automatisch regelmäßig aktualisiert. Dabei können basierend auf Änderungen durch den Administrator Ressourcen hinzugefügt, geändert oder entfernt werden.

### <a name="export-and-import-connections"></a>Exportieren und Importieren von Verbindungen

Sie können eine Remotedesktop-Verbindungsdefinition exportieren und auf einem anderen Gerät verwenden. Remotedesktops werden in separaten RDP-Dateien gespeichert.

So exportieren Sie eine RDP-Datei

1. Klicken Sie im Connection Center mit der rechten Maustaste auf den Remotedesktop.
2. Wähle **Exportieren** aus.
3. Navigieren Sie zu dem Speicherort, an dem die Remotedesktopdatei (RDP) gespeichert werden soll.
4. Wählen Sie **OK** aus.

So importieren Sie eine RDP-Datei

1. Wähle auf der Menüleiste **Datei** > **Importieren** aus.
2. Navigieren Sie zur RDP-Datei.
3. Wähle **Öffnen** aus.

## <a name="add-a-remote-resource"></a>Hinzufügen einer Remoteressource

Bei Remoteressourcen handelt es sich um RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops, die mithilfe von RemoteApp- und Desktopverbindungen veröffentlicht werden.

- Die URL zeigt den Link zum Server mit Web Access für Remotedesktop an, der Ihnen Zugriff auf RemoteApp- und Desktopverbindungen bietet.
- Die konfigurierten RemoteApp- und Desktopverbindungen werden aufgeführt.

Gehen Sie wie folgt vor, um eine Remoteressource hinzuzufügen:

1. Wähle im Connection Center das Pluszeichen ( **+** ) und dann **Remoteressourcen hinzufügen** aus.
2. Geben Sie Informationen für die Remoteressource ein:
   - **Feed-URL**: Die URL des Servers mit Web Access für Remotedesktop. In dieses Feld können Sie auch Ihr geschäftliches E-Mail-Konto eingeben. Dies weist den Client an, nach dem Ihrer E-Mail-Adresse zugeordneten Server mit Web Access für Remotedesktop zu suchen.
   - **Benutzername**: Der Benutzername, der für den Server mit Web Access für Remotedesktop verwendet werden soll, mit dem Sie eine Verbindung herstellen.
   - **Kennwort**: Das Kennwort, das für den Server mit Web Access für Remotedesktop verwendet werden soll, mit dem Sie eine Verbindung herstellen.
3. Wählen Sie **Speichern**.

Die Remoteressourcen werden im Connection Center angezeigt.

## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>Herstellen einer Verbindung mit einem Remotedesktopgateway zum Zugreifen auf interne Ressourcen

Mit einem Remotedesktopgateway (RD-Gateway) können Sie eine Verbindung mit einem Remotecomputer in einem Unternehmensnetzwerk über das Internet herstellen. Sie können Ihre Gateways in den Einstellungen der App oder beim Einrichten einer neuen Desktopverbindung erstellen und verwalten.

Gehen Sie wie folgt vor, um ein neues Gateway in den Einstellungen einzurichten:

1. Wähle im Connection Center **Einstellungen > Gateways** aus. 
2. Wähle im unteren Bereich der Tabelle die Schaltfläche **+** aus. Gib die folgenden Informationen ein:
   - **Servername**: Der Name des Computers, den Sie als Gateway verwenden möchten. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können dem Servernamen auch Portinformationen hinzufügen (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
   - **Benutzername**: Der Benutzername und das Kennwort für das Remotedesktopgateway, mit dem Sie eine Verbindung herstellen. Sie können auch **Anmeldeinformationen für die Verbindung verwenden** auswählen, damit derselbe Benutzername und dasselbe Kennwort wie für die Remotedesktopverbindung verwendet werden.

## <a name="manage-your-user-accounts"></a>Verwalten Ihrer Benutzerkonten

Wenn Sie eine Verbindung mit einem Desktop oder Remoteressourcen herstellen, können Sie die Benutzerkonten speichern, um sie erneut auswählen zu können. Sie können Ihre Benutzerkonten mit dem Remotedesktopclient verwalten.

Gehen Sie wie folgt vor, um ein neues Benutzerkonto zu erstellen:

1. Wähle im Connection Center **Einstellungen** > **Konten** aus.
2. Wähle **Benutzerkonto hinzufügen** aus.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername**: Der Name des Benutzers, der zur Verwendung für eine Remoteverbindung gespeichert werden soll. Sie können den Benutzernamen in einem der folgenden Formate eingeben: Benutzername, Domäne\Benutzername oder user_name@domain.com.
   - **Kennwort**: Das Kennwort für den angegebenen Benutzer. Jedem Benutzerkonto, das Sie zur Verwendung für Remoteverbindungen speichern möchten, muss ein Kennwort zugeordnet sein.
   - **Anzeigename**: Wenn Sie das gleiche Benutzerkonto mit verschiedenen Kennwörtern verwenden, legen Sie einen Anzeigenamen fest, um diese Benutzerkonten zu unterscheiden.
4. Wähle **Speichern** und dann **Einstellungen** aus.

## <a name="customize-your-display-resolution"></a>Anpassen der Bildschirmauflösung

Sie können die Bildschirmauflösung für die Remotedesktopsitzung angeben.

1. Wähle im Connection Center **Einstellungen** aus.
2. Wähle **Auflösung** aus.
3. Wähle **+** aus.
4. Gib die Höhe und Breite für eine Auflösung ein, und wähle dann **OK** aus.

Um die Auflösung zu löschen, wähle sie aus, und wähle dann das Minuszeichen ( **-** ) aus.

## <a name="displays-have-separate-spaces"></a>Monitore verwenden verschiedene Spaces

Wenn Sie das Betriebssystem Mac OS X 10.9 verwenden und in Mavericks die Option **Monitore verwenden verschiedene Spaces** (unter **Systemeinstellungen > Mission Control**) deaktiviert haben, müssen Sie diese Einstellung im Remotedesktopclient mit der gleichen Option konfigurieren.

### <a name="drive-redirection-for-remote-resources"></a>Laufwerkumleitung für Remoteressourcen

Die Laufwerkumleitung wird für Remoteressourcen unterstützt, sodass Sie mit einer Remoteanwendung erstellte Dateien lokal auf Ihrem Mac speichern können. Der umgeleitete Ordner ist immer Ihr Basisverzeichnis, das als Netzlaufwerk in der Remotesitzung angezeigt wird.

> [!NOTE]
> Damit dieses Feature verwendet werden kann, muss der Administrator die entsprechenden Einstellungen auf dem Server festlegen.

## <a name="use-a-keyboard-in-a-remote-session"></a>Verwenden einer Tastatur in einer Remotesitzung

Mac-Tastaturlayouts unterscheiden sich von Windows-Tastaturlayouts.

- Die Befehlstaste auf der Mac-Tastatur entspricht der Windows-Taste.
- Um Aktionen auszuführen, für die auf dem Mac die Befehlstaste verwendet wird, müssen Sie unter Windows die STRG-TASTE verwenden (z. B. Kopieren = STRG+C).
- Die Funktionstasten können in der Sitzung aktiviert werden, indem Sie zusätzlich die FN-Taste drücken (z. B. FN+F1).
- Auf der Mac-Tastatur entspricht die ALT-TASTE rechts neben der LEERTASTE auf einer Windows-Tastatur der ALT GR-TASTE (der rechten ALT-TASTE).

Die Remotesitzung verwendet standardmäßig dasselbe Tastaturgebietsschema wie das Betriebssystem, unter dem der Client ausgeführt wird. (Wird Ihr Mac unter einem englischen Betriebssystem (en-us) ausgeführt, wird dieses Betriebssystem auch für die Remotesitzungen verwendet.) Wenn das Tastaturgebietsschema des Betriebssystems nicht verwendet wird, überprüfen Sie die Tastatureinstellung auf dem Remotecomputer, und ändern Sie die Einstellung manuell. Weitere Informationen zu Tastaturen und Gebietsschemas finden Sie unter [Häufig gestellte Fragen zu den Remotedesktopclients](remote-desktop-client-faq.md).

## <a name="support-for-remote-desktop-gateway-pluggable-authentication-and-authorization"></a>Unterstützung für die austauschbare Remotedesktopgateway-Authentifizierung und -Autorisierung

In Windows Server 2012 R2 wurde die Unterstützung für eine neue Authentifizierungsmethode, die austauschbare Remotedesktopgateway-Authentifizierung und -Autorisierung eingeführt, die mehr Flexibilität für benutzerdefinierte Authentifizierungsroutinen bietet. Sie können dieses Authentifizierungsmodell jetzt mit dem Mac-Client ausprobieren.

> [!IMPORTANT]
> Benutzerdefinierte Authentifizierungs- und Autorisierungsmodelle vor Windows 8.1 werden nicht unterstützt, aber im obigen Artikel erläutert.

Weitere Informationen zu diesem Feature finden Sie unter [https://aka.ms/paa-sample](https://aka.ms/paa-sample).

> [!TIP]
> Fragen und Kommentare sind immer willkommen. Verwenden Sie jedoch NICHT die Kommentarfunktion am Ende dieses Artikels, um Hilfe bei der Problembehandlung anzufordern. Verwenden Sie stattdessen das [Remotedesktopclient-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc), und erstellen Sie einen neuen Thread. Haben Sie einen Vorschlag für ein Feature? Teilen Sie uns dies im [UserVoice-Forum für den Client](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android) mit.
