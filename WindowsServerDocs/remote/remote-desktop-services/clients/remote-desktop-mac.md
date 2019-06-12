---
title: Erste Schritte mit Remotedesktop auf Mac
description: Erfahren Sie, wie Sie den Remotedesktopclient für Mac einrichten
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7afc65f8-3158-49c9-9d48-4dab1c69afba
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 10/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: a54ffd3d5596ba8c71deab668e4952da445ca12e
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804941"
---
# <a name="get-started-with-remote-desktop-on-mac"></a>Erste Schritte mit Remotedesktop auf Mac

>Gilt für: Windows 10, Windows 8.1, Windows Server 2012 R2, WindowsServer 2016

Sie können den Remotedesktopclient für Mac verwenden, zum Arbeiten mit Windows-apps, Ressourcen und Desktops über Ihr Mac-Computer. Verwenden Sie die folgende Informationen, um erste Schritte – und sehen Sie sich die [– häufig gestellte Fragen](remote-desktop-client-faq.md) Wenn Sie Fragen haben.

>[!NOTE]
> - Möchten Sie wissen zu den neuen Versionen der MacOS-Client? Sehen Sie sich [Neuigkeiten für Remotedesktop auf einem Mac?](mac-whatsnew.md)
> - Der Macintosh-Client wird auf Computern mit der MacOS 10.10 oder höher ausgeführt werden.
> - Die Informationen in diesem Artikel betreffen in erster Linie auf die Vollversion des Mac-Clients – die Version, die in den Mac App Store verfügbar. Testen Sie neue Features durch die Preview-app hier herunterladen: [Beta-Client-Anmerkungen zu dieser Version](https://go.microsoft.com/fwlink/?LinkID=619698&clcid=0x409).

## <a name="get-the-remote-desktop-client"></a>Abrufen der Remotedesktop-client
Erste Schritte mit Remotedesktop auf Ihrem Mac, gehen Sie wie folgt vor:

1. Laden Sie die Microsoft-Remotedesktop-Client aus der [Mac App Store](https://itunes.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12).
2. [Richten Sie Ihren PC, um Remoteverbindungen](remote-desktop-client-faq.md#how-do-i-set-up-a-pc-for-remote-desktop). (Wenn Sie diesen Schritt überspringen, können nicht Sie auf Ihren PC verbinden.)
3. Fügen Sie eine Remotedesktopverbindung oder einer Remoteressource. Können Sie eine Verbindung direkt mit einem Windows-PC und einer Remoteressource, verwenden Sie ein RemoteApp-Programms, sitzungsbasierten Desktops herstellen oder ein virtueller Desktop veröffentlicht lokal mithilfe der RemoteApp- und Desktopverbindungen. Dieses Feature steht in der Regel in unternehmensumgebungen.

## <a name="what-about-the-mac-beta-client"></a>Was ist mit dem Mac-Beta-Client?
Testen wir neue Features für unsere Vorschau-Kanal auf HockeyApp. Möchten Sie es auschecken? Wechseln Sie zu [Microsoft Remote Desktop für Mac](https://go.microsoft.com/fwlink/?LinkID=619698) , und klicken Sie auf **herunterladen**. Sie müssen ein Konto anzumelden oder sich in HockeyApp zum Herunterladen von Beta-Client zu erstellen.

Wenn Sie bereits auf den Client verfügen, können Sie überprüfen, Updates, um sicherzustellen, dass Sie die neueste Version verfügen. Klicken Sie in der Beta-Client auf **Microsoft Remote Desktop Beta** oben, und klicken Sie dann auf **nach Updates suchen**. 

## <a name="add-a-remote-desktop-connection"></a>Fügen Sie eine Remotedesktopverbindung
So erstellen Sie eine Remotedesktopverbindung

1. Klicken Sie im Connection Center, auf **+** , und klicken Sie dann auf **Desktop**.
2. Geben Sie die folgende Informationen ein:
   - **PC-Namen** -der Name des Computers.
      - Dies kann ein Windows-Computername sein (finden Sie in der **System** Einstellungen), einen Domänennamen, oder eine IP-Adresse.
      - Sie können auch Portinformationen hinzufügen am Ende der diesem Namen gibt, wie z. B. *MyDesktop:3389*.
   - **Benutzerkonto** – Hinzufügen des Benutzerkontos, das Sie verwenden, um Zugriff auf den remote-PC.
     - Für Active Directory (AD), Computer oder lokale Konten verknüpft, verwenden Sie eines der folgenden Formate: *User_name*, *Domäne\Benutzername*, oder <em>user_name@domain.com</em>.
     - Verwenden Sie für Azure Active Directory (AAD) verknüpften Computer, eine der folgenden Formate: *AzureAD\user_name* oder <em>AzureAD\user_name@domain.com</em>.
     - Sie können auch auswählen, ob ein Kennwort erforderlich ist.
     - Bei der Verwaltung von mehreren Benutzerkonten mit dem gleichen Benutzernamen legen Sie einen Anzeigenamen ein, um die Konten zu unterscheiden.
     - Verwalten Sie Ihre gespeicherten Benutzerkonten in den Einstellungen der app. 

3. Sie können auch diese optionalen Einstellungen für die Verbindung festlegen:
   - Legen Sie einen Anzeigenamen 
   - Hinzufügen eines Gateways
   - Festlegen der Audioausgang
   - Swap-Maustasten
   - Aktivieren Sie im Admin-Modus
   - Lokalen Ordner in einer Remotesitzung umleiten
   - Weiterleiten von lokalen Druckern
   - Weiterleiten von Smartcards
4. Klicken Sie auf **Speichern**.

Um die Verbindung zu starten, doppelklicken Sie einfach auf sie. Dasselbe gilt für Remoteressourcen zugreifen.

### <a name="export-and-import-connections"></a>Exportieren und Importieren von Verbindungen
Sie können eine Remotedesktop-Definition exportieren und auf ein anderes Gerät verwenden. Remote-Desktops werden in separaten gespeichert. RDP-Dateien.

1. Klicken Sie im Connection Center den Remotedesktop.
2. Klicken Sie auf **Exportieren**.
3. Navigieren Sie zum Speicherort, in denen den Remotedesktop gespeichert werden soll. RDP-Datei.
4. Klicken Sie auf **OK**.

Verwenden Sie die folgenden Schritte aus, um Remotedesktop zu importieren. RDP-Datei.

1. Klicken Sie in der Menüleiste auf **Datei** > **Import**.
2. Navigieren Sie zu der. RDP-Datei.
3. Klicken Sie auf **Öffnen**.

## <a name="add-a-remote-resource"></a>Hinzufügen einer Remoteressource
Remote-Ressourcen sind die RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops mithilfe der RemoteApp- und Desktopverbindungen veröffentlicht.

- Die URL wird die Verknüpfung mit dem Web Access für Remotedesktop-Server, der Sie Zugriff auf RemoteApp- und Desktopverbindungen erhalten.
- Die konfigurierten RemoteApp- und Desktopverbindungen werden aufgeführt.

So fügen Sie eine Remoteressource hinzu:

1. Connection Center klicken Sie in der **+** , und klicken Sie dann auf **Remoteressourcen hinzufügen**. 
2. Geben Sie Informationen für die Remoteressource:
   - **Feed-URL** -die URL der Web Access für Remotedesktop-Server. Ihr Unternehmens-e-Mail-Konto auch in dieses Feld eingegeben werden können, weist diese den Client, suchen Sie für den RD-Web-Server Ihre e-Mail-Adresse zugeordnet.
   - **Benutzername** -den Benutzernamen ein, für den Web Access für Remotedesktop-Server verwenden Sie eine Verbindung herstellen.
   - **Kennwort** -das Kennwort für den Web Access für Remotedesktop-Server hergestellt.
3. Klicken Sie auf **Speichern**.


Der remote-Ressourcen werden im Connection Center angezeigt.


## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>Verbinden Sie mit einem RD-Gateway auf interne Ressourcen zugreifen

Ein Remotedesktopgateway (RD-Gateway) können Sie die Verbindung mit einem Remotecomputer in einem Unternehmensnetzwerk von überall aus im Internet. Sie können Gateways erstellen und Verwalten Ihrer in den Einstellungen der app oder beim Einrichten einer neuen desktop-Verbindungs.

So richten ein neues Gateway in die Einstellungen aus:

1. Klicken Sie im Connection Center, auf **Voreinstellungen > Gateways**. 
2. Klicken Sie auf die **+** Schaltfläche am unteren Rand der Tabelle geben Sie die folgenden Informationen:
   - **Servername** – der Name des Computers als Gateway verwenden möchten. Dies kann es sich um einen Windows-Computernamen, einen Internet-Domänennamen oder eine IP-Adresse sein. Sie können auch Informationen hinzufügen, um den Namen des Servers (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
   - **Benutzername** -den Benutzernamen und Kennwort ein, das für den Remotedesktop-Gateway hergestellt. Sie können auch auswählen, **verwenden Sie die Anmeldeinformationen für die Verbindung** den gleichen Benutzernamen und das Kennwort wie für die Remotedesktopverbindung verwenden.


## <a name="manage-your-user-accounts"></a>Verwalten Sie Ihre Benutzerkonten

Wenn Sie auf einem Desktop- oder remote-Ressourcen verbinden, können Sie die Benutzerkonten erneut aus speichern. Sie können Ihre Benutzerkonten verwalten, mit dem Remotedesktop-Client.

So erstellen Sie ein neues Benutzerkonto:

1. Klicken Sie im Connection Center, auf **Einstellungen** > **Konten**.
2. Klicken Sie auf **Benutzerkonto hinzufügen**.
3. Geben Sie die folgende Informationen ein:
   - **Benutzername** -der Name des Benutzers, der für die Verwendung mit einer remote-Verbindung zu speichern. Sie können den Benutzernamen eingeben, in einem der folgenden Formate: Domäne\Benutzername, User_name oder user_name@domain.com.
   - **Kennwort** -das Kennwort für den Benutzer, die Sie angegeben haben. Jedes Benutzerkonto, das Sie speichern, um für Remoteverbindungen verwenden möchten, muss ein Kennwort zugeordnet.
   - **Anzeigenamen** : Wenn Sie das gleiche Benutzerkonto mit verschiedenen Kennwörtern verwenden legen Sie einen Anzeigenamen ein, die diese Benutzerkonten zu unterscheiden.
4. Tippen Sie auf **speichern**, und tippen Sie dann auf **Einstellungen**.

## <a name="customize-your-display-resolution"></a>Passen Sie Ihrer Bildschirmauflösung an
Sie können die anzeigeauflösung für die Remotedesktopsitzung angeben.

1. Klicken Sie im Connection Center, auf **Voreinstellungen**.
2. Klicken Sie auf **Auflösung**. 
3. Klicken Sie auf **+** .
4. Geben Sie eine Auflösung von Höhe und Breite werden soll, und klicken Sie dann auf **OK.**

Um die Auflösung zu löschen, wählen Sie ihn, und klicken Sie dann auf **-** .

**Zeigt separate Leerzeichen enthalten** , wenn Sie Mac OS X 10.9 ausgeführt werden und deaktiviert **zeigt separate Leerzeichen enthalten** in Mavericks (**Systemeinstellungen > Mission Control**), müssen Sie konfigurieren Diese Einstellung in der Remotedesktop-Client mit der gleichen Option.

### <a name="drive-redirection-for-remote-resources"></a>Laufwerkumleitung für Remoteressourcen
Laufwerkumleitung wird, damit Sie mit einer Remoteanwendung lokal auf Ihrem Mac erstellte Dateien speichern können, für die Remoteressourcen, unterstützt. Der umgeleitete Ordner ist immer Ihr Basisverzeichnis als Netzlaufwerk angezeigt wird, in der Remotesitzung.

> [!NOTE]
> Um dieses Feature verwenden zu können, muss der Administrator die entsprechenden Einstellungen auf dem Server festgelegt.


## <a name="use-a-keyboard-in-a-remote-session"></a>Verwenden Sie eine Tastatur in einer Remotesitzung

Mac-Tastaturlayouts unterscheiden sich von der Windows-Tastaturlayouts. 

- Der Schlüssel auf der Tastatur Mac entspricht, die Windows-Taste.
- Um Aktionen auszuführen, die die Schaltfläche "Befehl" auf dem Mac verwenden, müssen Sie die Schaltfläche "Control" in Windows verwenden (z. B.: Copy = Ctrl + C).
- Die Funktionsschlüssel können in der Sitzung aktiviert werden, außerdem die FN-Taste drücken (z. B.: FN + F1).
- Die Alt-Taste rechts neben der LEERTASTE auf der Tastatur Mac entspricht die Alt Gr/Rechte Alt-Taste in Windows.

Standardmäßig wird die Remotesitzung das gleiche Gebietsschema der Tastatur als Betriebssystem verwenden, die Sie auf den Client ausführen. (Wenn auf Ihrem Mac de ausgeführt wird – wir Betriebssystem, die für die Remotesitzungen ebenfalls verwendet werden. Wenn das Gebietsschema des Betriebssystems Tastatur nicht verwendet wird, überprüfen Sie die Tastatur auf einem Remotecomputer festlegen und Ändern der Einstellung manuell. Finden Sie unter den [Remote Desktop-Client – häufig gestellte Fragen](remote-desktop-client-faq.md) für Weitere Informationen zu Tastaturen und Gebietsschemas.


## <a name="support-for-remote-desktop-gateway-pluggable-authentication-and-authorization"></a>Unterstützung für Remote Desktop Gateway austauschbare Authentifizierung und Autorisierung

Windows Server 2012 R2 wurde Unterstützung für eine neue Authentifizierungsmethode, Remote Desktop Gateway austauschbare Authentifizierung und Autorisierung, wodurch die bietet mehr Flexibilität für die benutzerdefinierte Authentifizierung Routinen eingeführt. Sie können jetzt dieses Authentifizierungsmodell, mit dem Mac-Client. 

> [!IMPORTANT]
> Benutzerdefinierte Authentifizierung und Autorisierung Modelle vor dem Windows 8.1 werden nicht unterstützt, obwohl die oben genannten Artikel wird, sie erläutert.

Weitere Informationen zu diesem Feature finden Sie [ http://aka.ms/paa-sample ](http://aka.ms/paa-sample).


> [!TIP]
> Fragen und Kommentare sind immer Willkommen. Allerdings Supportfragen Sie keine Anforderung für die Hilfe zur Problembehandlung, indem Sie über die Kommentarfunktion am Ende dieses Artikels. Wechseln Sie stattdessen zu den [Remotedesktop-Client-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc) und einen neuen Thread starten. Haben Sie Vorschläge Feature? Teilen Sie uns in die [Client User Voice-Forum](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android).

