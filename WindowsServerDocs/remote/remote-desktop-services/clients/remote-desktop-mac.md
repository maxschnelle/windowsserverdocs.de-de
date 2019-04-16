---
title: Erste Schritte mit Remotedesktop auf einem Mac
description: Erfahren Sie, wie der Remotedesktop-Client für Mac einrichten
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
ms.openlocfilehash: e8c5da1960d0e3129b5520e65c2d5ecf45eef778
ms.sourcegitcommit: 6dc14d4315793132488494b5543ee83e3f562f09
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2018
ms.locfileid: "4555717"
---
# Erste Schritte mit Remotedesktop auf einem Mac

>Gilt für: Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2016

Sie können den Remotedesktopclient für Mac verwenden, Arbeit mit Windows-apps und Ressourcen Desktops auf Ihrem Mac-Computer. Verwenden Sie die folgende Informationen für erste Schritte – und sehen Sie sich die [häufig gestellten Fragen](remote-desktop-client-faq.md) , wenn Sie Fragen haben.

>[!Note]
> - Mehr über die neuen Versionen für den MacOS-Client? Sehen Sie sich [Neuigkeiten für den Remotedesktop auf einem Mac?](mac-whatsnew.md)
> - Der Mac-Client auf Computern mit MacOS 10.10 und höher ausgeführt wird.
> - Die Informationen in diesem Artikel gilt in erster Linie für die Vollversion der Mac-Client – die in der Mac-AppStore verfügbare Version. Testen Sie neue Features, durch das Herunterladen von unseren Preview-app: [Betaclient Anmerkungen zu dieser Version](https://go.microsoft.com/fwlink/?LinkID=619698&clcid=0x409).

## Abrufen von Remotedesktop-Clients
So beginnen Sie mit den Remotedesktop auf Ihrem Mac, gehen Sie wie folgt vor:

1. Laden Sie den Microsoft-Remotedesktopclient aus dem [Mac App Store](https://itunes.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12).
2. [Einrichten des Computers für Remoteverbindungen](remote-desktop-client-faq.md#how-do-i-set-up-a-pc-for-remote-desktop). (Wenn Sie diesen Schritt überspringen, können nicht Sie an Ihren PC anschließen.)
3. Fügen Sie eine Remotedesktopverbindung oder eine remote-Ressourcen. Verwenden Sie eine Verbindung für die Verbindung direkt mit einem Windows-PC und einer remote-Ressourcen verwenden eine RemoteApp-Programm, eine Sitzung-basierten Desktopcomputern, oder ein virtueller Desktop veröffentlicht lokal mithilfe von RemoteApp und Desktop-Verbindungen. Dieses Feature ist in der Regel in unternehmensumgebungen verfügbar.

## Was ist mit der Mac-Beta-Client?
Wir haben neue Features auf unsere Preview-Kanal auf HockeyApp testen. Es auschecken möchten? Wechseln Sie zu [Microsoft-Remotedesktop für Mac](https://go.microsoft.com/fwlink/?LinkID=619698) , und klicken Sie auf **herunterladen**. Sie müssen ein Konto oder melden Sie sich in HockeyApp zum Herunterladen von des Beta-Clients zu erstellen.

Wenn Sie bereits auf den Client verfügen, können Sie überprüfen, für Updates, um sicherzustellen, dass Sie die neueste Version verfügen. Klicken Sie in die Betaclient auf **Microsoft Remote Desktop Beta** am oberen, und klicken Sie dann auf **nach Updates suchen**. 

## Fügen Sie eine Remotedesktopverbindung
So erstellen Sie eine Remotedesktopverbindung:

1. Klicken Sie in der Mitte Verbindung auf **+**, und klicken Sie dann auf **Desktop**.
2. Geben Sie die folgenden Informationen ein:
   - **PC-Name** - der Name des Computers.
      - Dies kann eine Windows-Computernamen (finden Sie in **den Systemeinstellungen** ), einen Domänennamen oder einer IP-Adresse sein.
      - Sie können auch Portinformationen am Ende dieser Name, z. B. *MyDesktop:3389*hinzufügen.
   - **Benutzerkonto** - Hinzufügen des Benutzerkontos, das Sie verwenden, um die remote-PC zugreifen.
      - Für Active Directory (AD) Computer oder lokale Konten verknüpft, verwenden Sie eine der folgenden Formaten: *Benutzername*, *Domäne\Benutzername*oder *user_name@domain.com*.
      - Für Azure Active Directory (AAD) beigetreten, verwenden Sie eine der folgenden Formate: *AzureAD\user_name* oder *AzureAD\ user_name@domain.com*.
      - Sie können auch auswählen, ob ein Kennwort erforderlich.
      - Wenn Sie mehrere Benutzerkonten mit Benutzername und zu verwalten, legen Sie einen Anzeigenamen, die Konten zu unterscheiden.
      - Verwalten Sie Ihre gespeicherte Benutzerkonten in den Einstellungen der app. 

3. Sie können auch diese optionalen Einstellungen für die Verbindung festlegen:
   - Legen Sie einen Anzeigenamen 
   - Hinzufügen eines Gateways
   - Legen Sie die Audioausgabe
   - Maustasten vertauschen
   - Admin-Modus aktivieren
   - Umleitung lokaler Ordner in einer Remotesitzung
   - Vorwärts lokalen Drucker
   - Vorwärts Smartcards
4. Klicken Sie auf **Speichern**.

Um die Verbindung zu starten, doppelklicken sie. Dies gilt auch für remote-Ressourcen.

### Exportieren und Importieren von Verbindungen
Sie können eine Remotedesktopverbindung Definition exportieren und auf einem anderen Gerät verwenden. Remotedesktops werden in separaten gespeichert. RDP-Dateien.

1. In der Mitte Verbindung mit der rechten Maustaste Remotedesktop.
2. Klicken Sie auf **Exportieren**.
3. Navigieren Sie zum Speicherort, in dem Sie den Remotedesktop speichern möchten. RDP-Datei.
4. Klicken Sie auf **OK**.

Gehen Sie folgendermaßen vor, um einen Remotedesktop zu importieren. RDP-Datei.

1. Klicken Sie in der Menüleiste auf **Datei > Importieren**.
2. Navigieren Sie zu der. RDP-Datei.
3. Klicken Sie auf **Öffnen**.

## Fügen Sie eine remote-Ressourcen
Remote-Ressourcen sind RemoteApp-Programme Sitzung-basierten Desktops und virtuelle Desktops mit RemoteApp und Desktop Connections veröffentlicht.

- Die URL zeigt den Link mit dem Web Access für Remotedesktop-Server, der Sie auf RemoteApp und Desktop Connections zugreifen kann.
- Die konfigurierte RemoteApp und Desktop-Verbindungen werden aufgeführt.

So fügen Sie eine remote-Ressourcen hinzu:

1. In der Verbindung Center auf **+**, und klicken Sie dann auf **Remote-Ressourcen hinzufügen**. 
2. Geben Sie Informationen für die remote-Ressourcen:
   - **Feed-URL** - der URL des Web Access für Remotedesktop-Servers. Sie Ihre unternehmenseigenen e-Mail-Konto auch in diesem Feld – eingeben können teilt diese auf dem Client, suchen Sie für den Remotedesktop-Web-Server Ihre e-Mail-Adresse zugeordnet ist.
   - **Benutzername** – der Benutzername für das Web Access für Remotedesktop-Server verwenden, die Sie zum Verbinden.
   - **Kennwort** : das Kennwort für das Web Access für Remotedesktop-Server verwenden, die Sie zum Verbinden.
3. Klicken Sie auf **Speichern**.


Die remote-Ressourcen werden in der Mitte Verbindung angezeigt.


## Verbinden Sie mit einem Remotedesktopgateway auf interne Ressourcen zugreifen

Ein Remotedesktopgateway (RD-Gateway) können Sie die Verbindung mit eines Remotecomputer in einem Unternehmensnetzwerk überall im Internet. Sie erstellen und Verwalten Ihrer Gateways in den Einstellungen der app oder beim Einrichten einer neuen Remotedesktop-Verbindungs.

So richten ein neues Gateway in Voreinstellungen

1. Klicken Sie in der Mitte Verbindung auf **Voreinstellungen > Gateways**. 
2. Klicken Sie auf die **+** Schaltfläche am unteren Rand der Tabelle geben Sie die folgenden Informationen:
  - **Servername** – den Namen des Computers, den Sie als Gateway verwenden möchten. Dies kann eine Windows-Computernamen, ein Internetdomänenname oder einer IP-Adresse sein. Sie können auch Portinformationen hinzufügen, um den Namen des Servers (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
  - **Benutzername** - Benutzername und Kennwort für den Remotedesktop-Gateway verwendet werden, die Sie zum Verbinden. Sie können auch die **Anmeldeinformationen verwenden** , um den gleichen Benutzernamen und Kennwort als die für die Remotedesktopverbindung verwenden auswählen.


## Verwalten von Benutzerkonten

Wenn Sie auf einem desktop oder remote-Ressourcen zugreifen, können Sie die Benutzerkonten erneut aus speichern. Sie können Ihre Benutzerkonten mithilfe von Remotedesktop-Clients verwalten.

So erstellen Sie ein neues Benutzerkonto:

1. Klicken Sie in der Mitte Verbindung auf **Einstellungen** > **Konten**.
2. Klicken Sie auf **Benutzerkonto**.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername** - der Name des Benutzers an, für die Verwendung mit einer Remoteverbindung zu speichern. Sie können den Benutzernamen eingeben, in den folgenden Formaten: Benutzername, Domäne\Benutzername, oder user_name@domain.com.
   - **Kennwort** : das Kennwort für den Benutzer, die, den Sie angegeben. Jedes Benutzerkonto, die Sie speichern, um für Remoteverbindungen verwenden möchten, muss ein Kennwort zugeordnet ist.
   - **Anzeigename** - legen bei Verwendung der gleichen Benutzerkonto mit unterschiedlichen Kennwörtern Sie einen Anzeigenamen, diese Konten zu unterscheiden.
4. Tippen Sie auf **Speichern**, und tippen Sie dann auf **Einstellungen**.

## Anpassen der Auflösung
Sie können die Auflösung für den desktop Remotesitzung angeben.

1. Klicken Sie in der Mitte Verbindung auf **Voreinstellungen**.
2. Klicken Sie auf **Auflösung**. 
3. Klicken Sie auf **+**.
4. Geben Sie eine Auflösung Höhe und Breite, und klicken Sie dann auf **OK.**

Um die Auflösung zu löschen, auszuwählen, und klicken Sie dann auf **-**.

**Displays verfügen über separate Leerzeichen** Wenn Sie Mac OS X 10.9 ausgeführt werden und in Mavericks **Displays verfügen über separate Leerzeichen deaktiviert** (**Systemeinstellungen > Mission Steuerelement**), müssen Sie diese Einstellung in der Remotedesktop-Client mit der gleichen Option zu konfigurieren.

### Intensivieren Sie die Umleitung für remote-Ressourcen
Laufwerk Umleitung ist für remote-Ressourcen unterstützt, damit Sie mit einer remote-Anwendung lokal auf Ihrem Mac erstellte Dateien speichern können Der umgeleitete Ordner ist immer Basisverzeichnis als Netzlaufwerk in der Remotesitzung angezeigt.

> [!NOTE]
> Um dieses Feature verwenden zu können, muss der Administrator die entsprechenden Einstellungen auf dem Server festlegen.


## Verwenden Sie eine Tastatur in einer Remotesitzung

Mac-Tastaturlayouts unterscheiden sich von der Windows-Tastaturlayouts. 

- Der Befehl Schlüssel auf der Mac-Tastatur entspricht der Windows-Taste.
- Um Aktionen auszuführen, die die Befehlsschaltfläche auf dem Mac verwenden, Sie müssen die Schaltfläche Steuerung unter Windows verwenden (z. B.: Kopie = STRG + C).
- Die Funktionstasten in der Sitzung durch Drücken von außerdem FN aktiviert werden können (z. B.: FN + F1).
- Die Alt-Taste rechts neben der LEERTASTE auf der Mac-Tastatur entspricht die Alt Alt Gr/rechts-Taste in Windows.

Standardmäßig verwendet die Remotesitzung Tastatur Gebietsschema als das Betriebssystem, die Sie auf den Client ausführen. (Wenn Ihr Mac En ausgeführt wird – uns OS, das für die Remotesitzungen sowie verwendet wird. Wenn das Betriebssystem Gebietsschema nicht verwendet wird, überprüfen Sie die Tastatur auf die remote-PC einrichten und Ändern der Einstellung manuell. Finden Sie im [Remote Desktop Client – häufig gestellte Fragen](remote-desktop-client-faq.md) für Weitere Informationen zu Tastaturen und Gebietsschemas.


## Unterstützung für Remotedesktop-Gateway-Plug-Authentifizierung und Autorisierung

Windows Server 2012 R2 eingeführt, Unterstützung für neue Authentifizierungsmethode, Remotedesktopgateway austauschbaren Authentifizierung und Autorisierung, die für die benutzerdefinierte Authentifizierung Routinen mehr Flexibilität bereitstellt. Jetzt können Sie dieses Authentifizierungsmodell mit dem Mac-Client. 

> [!IMPORTANT]
> Benutzerdefinierte Authentifizierung und Autorisierung Modelle vor Windows 8.1 werden nicht unterstützt, während der oben genannten Artikel werden erläutert.

Weitere Informationen zu diesem Feature Auschecken [http://aka.ms/paa-sample](http://aka.ms/paa-sample).


> [!TIP]
> Fragen und Kommentare sind immer Willkommen. Allerdings bitte nicht Veröffentlichen einer Anforderung für Hilfe zur Problembehandlung, mit dem Kommentarfeature am Ende dieses Artikels. Stattdessen, besuchen Sie das [Forum für Remotedesktop-Client](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc) , und starten Sie einen neuen Thread. Haben Sie einen Vorschlag für eine Funktion? Teilen Sie uns im [Forum für Client Benutzer Voice](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android).

