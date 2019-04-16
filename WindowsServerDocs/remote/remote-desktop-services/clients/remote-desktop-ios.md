---
title: Erste Schritte mit Remotedesktop für iOS
description: Erfahren Sie, wie Sie den Remotedesktopclient für iOS einrichten
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
ms.openlocfilehash: aab84dde3ded2a3d3f17f4bb318302321c444606
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297229"
---
# Erste Schritte mit Remotedesktop für iOS

>Gilt für: Windows 10, Windows 8.1, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2

Sie können den Remotedesktopclient für iOS verwenden, funktionieren mit Windows-apps, Ressourcen und Desktops von Ihrem Gerät iOS (iPhones und iPads).

Verwenden Sie die folgende Informationen, um zu beginnen. Achten Sie darauf, um die [– häufig gestellte Fragen](remote-desktop-client-faq.md) zu überprüfen, wenn Sie Fragen haben.

> [!NOTE]
> - Sie wissen die neuen Versionen für iOS-Client? Sehen Sie sich [für Remotedesktop auf iOS Neuigkeiten?](ios-whatsnew.md)
> - Die iOS-Client unterstützt Geräte unter iOS 6.x und höher.

## Remotedesktop-Clients und beginnen sie mit

### Den Remotedesktop-Client aus dem iOS-Store herunterladen
Um mit Remotedesktop auf Ihrem Gerät iOS beginnen, gehen Sie wie folgt vor:

1. Laden Sie die Microsoft-Remotedesktopclient aus [iTunes](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8).
2. Die [Einrichtung Ihres PCs für Remoteverbindungen festlegen](remote-desktop-client-faq.md#how-do-i-set-up-a-pc-for-remote-desktop).
3. Fügen Sie eine [Remotedesktopverbindung](#add-a-remote-desktop-connection) oder eine [remote-Ressourcen](#add-a-remote-resource). Verwenden Sie eine Verbindung zum Herstellen einer direkt auf einem Windows-PC und eine remote-Ressource mit einem RemoteApp-Programm, Sitzung-basierten Desktop oder ein virtueller Desktop veröffentlicht lokale mit RemoteApp und Desktop-Verbindungen. Dieses Feature ist in der Regel in unternehmensumgebungen verfügbar.

### Herunterladen des Remotedesktop-iOS Beta-Clients
Befolgen Sie auf Ihrem Gerät iOS [diese Anweisungen,](https://aka.ms/rdiosbeta) um die iOS Beta Remotedesktopclient herunterzuladen.

### Fügen Sie eine Remotedesktopverbindung

So erstellen Sie eine Remotedesktopverbindung: 
1. In der Verbindung Center tippen **+**, und tippen Sie dann auf **Hinzufügen PC oder Server**.
2. Geben Sie die folgende Informationen für die Remotedesktopverbindung:
  - **PC-Name** – der Name des Computers. Dies kann es sich um einen Windows-Computernamen, ein Internetdomänenname oder einer IP-Adresse sein. Sie können auch auf den PC-Namen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**) Portinformationen anfügen.
  - **Benutzername** – den Benutzernamen zu verwenden, um die remote-PC zuzugreifen. Sie können die folgenden Formate: *Benutzername*, *Domäne\Benutzername*oder *user_name@domain.com*. Sie können auch angeben, ob für einen Benutzernamen und Kennwort auffordern.
3. Sie können auch die folgenden zusätzlichen Optionen festlegen:
  - **Anzeigename (optional)** – eine leicht zu merkenden Namen für den PC herstellen. Sie können eine beliebige Zeichenfolge verwenden, aber der PC-Name wird angezeigt, wenn Sie einen Anzeigenamen nicht angeben.
  - **Gateway (optional)** – der Remotedesktop-Gateway, das Sie zum Herstellen einer virtuellen Desktops, RemoteApp-Programme und Sitzung-basierte Desktops auf einem internen Firmennetzwerk verwenden möchten. Erhalten Sie die Informationen über das Gateway von Ihr Systemadministrator.
  - **Sound** – wählen Sie das Gerät für Audio während der Remotesitzung verwendet. Sie können auswählen, um auf lokalen Geräten, auf dem Remotegerät oder gar wiederzugeben.
  - Die gleichen Befehl mit der rechten Maustaste **Maustasten vertauschen** – Wenn eine Maus Geste einen Befehl mit der linken Maustaste senden würden, stattdessen sendet. Dies ist notwendig, wenn die remote-PC für linkshändige mausmodus konfiguriert ist.
  - **Administratormodus** – eine Verbindung mit einem Administration-Sitzung auf einem Server mit WindowsServer 2003 oder höher.
4. Tippen Sie auf **Speichern**.

Möchten Sie diese Einstellungen bearbeiten? Drücken Sie und halten Sie den Desktop, die, den Sie bearbeiten möchten, und tippen Sie dann auf das Symbol "Einstellungen". 

### Fügen Sie eine remote-Ressource
Remote-Ressourcen sind RemoteApp-Programme, Sitzung-basierte Desktops und virtuelle Desktops mit RemoteApp und Desktop Connections veröffentlicht.

- Die URL zeigt den Link mit dem Web Access für Remotedesktop-Server, der Sie auf RemoteApp und Desktop Connections zugreifen kann.
- Die konfigurierte RemoteApp und Desktop-Verbindungen werden aufgeführt.

So fügen Sie eine remote-Ressourcen hinzu:

1. Tippen Sie auf dem Bildschirm Verbindung Center auf **+**, und tippen Sie dann auf **Remote-Ressourcen hinzufügen**. 
2. Geben Sie die Informationen für die remote-Ressourcen:
   - **Feed-URL** - die URL des Web Access für Remotedesktop-Servers. Sie Ihre unternehmenseigenen e-Mail-Konto auch in diesem Feld – eingeben können, weist dies den Client für den Remotedesktop-Web-Server Ihrer e-Mail-Adresse zugeordnet zu suchen.
   - **Benutzername** - der Benutzername für das Web Access für Remotedesktop-Server zu verwenden, die Sie zum Verbinden.
   - **Kennwort** : das Kennwort für das Web Access für Remotedesktop-Server zu verwenden, die Sie zum Verbinden.
3. Tippen Sie auf **Speichern**.

Die remote-Ressourcen werden in der Mitte Verbindung angezeigt.


## Verbinden Sie mit einem RD-Gateway auf interne Ressourcen zugreifen

Ein Remotedesktopgateway (RD-Gateway) können Sie die Verbindung mit eines Remotecomputer in einem Unternehmensnetzwerk von jedem beliebigen Standort auf das Internet. Sie erstellen und Verwalten Ihrer Gateways über den Remotedesktopclient.

So richten ein neues gateway

1. Tippen Sie in der Mitte Verbindung auf **Einstellungen > Gateways**. 
2. Tippen Sie auf **Hinzufügen des Remotedesktop-Gateway**.
3. Geben Sie die folgenden Informationen ein:
  - **Servername** – den Namen des Computers, den Sie als Gateway verwenden möchten. Dies kann es sich um einen Windows-Computernamen, ein Internetdomänenname oder einer IP-Adresse sein. Sie können auch die Portinformationen hinzufügen, um den Namen des Servers (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
  - **Benutzername** - Benutzername und Kennwort für den Remotedesktop-Gateway verwendet werden, der an angeschlossen sind. Sie können auch die **Verbindungsanmeldeinformationen verwenden** , um den gleichen Benutzernamen und Kennwort als die für die Remotedesktopverbindung verwenden auswählen.


## Verwalten von Benutzerkonten 

Wenn Sie auf einem desktop oder remote-Ressourcen zugreifen, können Sie die Benutzerkonten Auswahl aus erneut speichern. Sie können Ihre Benutzerkonten mithilfe von Remotedesktop-Clients verwalten.

So erstellen Sie ein neues Benutzerkonto:

1. Tippen Sie auf **Einstellungen**, und tippen Sie dann auf **Benutzernamen**, in der Mitte Verbindung.
2. Tippen Sie auf die **Benutzerkonto hinzufügen**.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername** - der Name des Benutzers für die Verwendung mit eine Remoteverbindung zu speichern. Sie können den Benutzernamen eingeben, in den folgenden Formaten: Benutzername, Domäne\Benutzername, oder user_name@domain.com.
   - **Kennwort** : das Kennwort für den Benutzer, die, den Sie angegeben. Jedes Benutzerkonto, die Sie speichern, um für Remoteverbindungen verwenden möchten, muss ein Kennwort zugeordnet ist.
4. Tippen Sie auf **Speichern**, und tippen Sie dann auf **Einstellungen**.
5. Tippen Sie auf **Fertig** , um die neue Konfiguration zu speichern.

So löschen Sie ein Benutzerkonto

1. Tippen Sie in der Mitte Verbindung **Einstellungen > Benutzernamen**ein.
2. Wischen Sie die Zeile von rechts nach links, um den Benutzer auszuwählen.
3. Tippen Sie auf **Löschen**.



## Navigieren Sie der Remotedesktop-Sitzung
Wenn Sie eine Remotedesktopsitzung starten, stehen Tools zur Verfügung, die Sie verwenden können, um die Sitzung zu navigieren.

### Starten Sie eine Remotedesktopverbindung

1. Tippen Sie auf die Remotedesktopverbindung, um die remote-desktop-Sitzung zu starten. 
2. Wenn Sie, zum Überprüfen des Zertifikats für den Remotedesktop gefragt werden, tippen Sie auf **annehmen**. Sie können auch immer bewegen Sie den Umschalter **nicht erneut zur Verbindung mit diesem Computer auffordern** , **zu**akzeptieren. 

### Symbolleiste Verbindung

Die Verbindung Leiste erhalten Sie Zugriff auf zusätzliche Navigationssteuerelementen. 

- **Schwenken-Steuerelement**: Das Schwenksteuerelement ermöglicht den Bildschirm vergrößert und anders angeordnet werden. Beachten Sie, dass Schwenken-Steuerelement nur per direct verfügbar ist.
   - Aktivieren / Deaktivieren der Schwenken-Steuerelement: Tippen Sie auf das Schwenken-Symbol auf der Verbindungsleiste zum Anzeigen des Steuerelements verschieben und vergrößern/verkleinern des Bildschirms. Tippen Sie auf das Schwenken-Symbol auf der Verbindungsleiste erneut aus, um das Steuerelement ausblenden und den Bildschirm an der ursprünglichen Auflösung zurückzugeben.
   - Verwenden Sie das Schwenksteuerelement: Tippen und halten heruntergezogen steuern und ziehen Sie dann in die Richtung, möchten Sie den Bildschirm zu verschieben.
   - Verschieben Sie das Schwenksteuerelement: Doppeltippen und halten Sie das Schwenksteuerelement, das Steuerelement auf dem Bildschirm zu verschieben.
- **Name der Verbindung**: den Verbindungsnamen der aktuellen wird angezeigt. Tippen Sie auf den Verbindungsnamen die Sitzung Leiste angezeigt.
- **Tastatur**: Tippen Sie auf das Tastatursymbol ein-oder Ausblenden der Tastatur. Schwenken-Steuerelement wird automatisch angezeigt, wenn die Bildschirmtastatur angezeigt wird.
- **Verschieben Sie die Symbolleiste Verbindung**: Tippen und halten Sie die Symbolleiste Verbindung und dann Drag & Drop an eine neue Position am oberen Rand des Bildschirms.

### Auswahl der Sitzung
Sie können mehrere Verbindungen, die auf verschiedenen Computern gleichzeitig öffnen haben. Tippen Sie auf die Symbolleiste Verbindung, um die Sitzung Leiste auf der linken Seite des Bildschirms angezeigt werden soll. Die Sitzung Leiste können Sie Ihre öffnen Verbindungen anzeigen und zwischen diesen zu wechseln. 

- Wechseln Sie zwischen apps in einer Sitzung öffnen remote-Ressourcen.

    Wenn Sie mit remote-Ressourcen verbunden sind, können Sie zwischen geöffnete Anwendungen in dieser Sitzung durch Tippen auf das Menü einer Erweiterung aus der Liste der verfügbaren Elemente auswählen wechseln.
- Eine neue Sitzung starten

  Sie können neue Anwendungen oder desktop-Sitzung vom innerhalb Ihrer aktuellen Verbindung starten: Tippen Sie auf **Neu starten**, und wählen Sie dann aus der Liste der verfügbaren Elemente.

- Trennen der Verbindung eine Sitzung

  Um eine Sitzung tippen X in der linken Seite der Kachel Sitzung zu trennen.

### Befehlsleiste

Die Befehlsleiste ersetzt das Dienstprogramm Leiste ab Version 8.0.1. Wechseln Sie zwischen den Modi Maus und zurück zum Verbindungscenter aus der Befehlsleiste.

## Verwenden von Touchgesten und Maus-Modi in einer Remotesitzung

Der Client verwendet standard Touchgesten. Sie können auch Touchgesten verwenden, Mausaktionen auf dem Remotedesktop replizieren. Die verfügbaren Maus-Modi werden in der folgenden Tabelle definiert.

> [!NOTE]
> Interaktion mit Windows 8 oder höher werden die systemeigenen Touchgesten im direkten Touch-Modus unterstützt. Weitere Informationen zu Windows 8-Gesten, finden Sie unter [Touch: "Wischen", tippen, und darüber hinaus](https://windows.microsoft.com/en-US/windows-8/touch-swipe-tap-beyond).

| Mausmodus    | Maus-Vorgang      | Geste                                                    |
|---------------|----------------------|------------------------------------------------------------|
| Direkte Toucheingabe  | Linksklick           | 1 Fingern tippen                                               |
| Direkte Toucheingabe  | Rechtsklick          | 1 Fingern tippen und halten                                      |
| Mauszeiger | Linksklick           | 1 Fingern tippen                                               |
| Mauszeiger | Linksklick und ziehen  | Ziehen Sie 1 Finger double tippen und halten,                    |
| Mauszeiger | Rechtsklick          | 2 Fingern tippen                                               |
| Mauszeiger | Rechtsklick und ziehen | 2 Finger double tippen und halten, ziehen Sie                    |
| Mauszeiger | Mausrad          | 2 Finger tippen und halten und ziehen Sie nach oben oder unten                |
| Mauszeiger | Zoom                 | Zusammendrücken Sie 2 Finger zum Verkleinern oder vergrößern 2 Finger zum Verkleinern |

## Unterstützte Eingabegeräte

Die [iOS Beta Remotedesktopclient](https://aka.ms/rdiosbeta) unterstützt die Swiftpoint GT und ProPoint physischen Mäuse. Swiftpoint bietet eine [exklusive Rabatt](https://www.swiftpoint.com/microsoft/) auf die GT für iOS-Beta-Client-Benutzer an.

Die iOS-Client unterstützt derzeit nur Swiftpoint Mäuse. Verweisen Sie auf die Seite [Neuigkeiten bei der iOS-Client](ios-whatsnew.md) und dem [Store für iOS-App](https://aka.ms/rdios) für Nachrichten über die Unterstützung für andere Geräte in Zukunft an.

## Verwenden Sie eine Tastatur in einer Remotesitzung

Sie können entweder ein auf dem Bildschirm Tastatur oder physische Tastatur in der Remotesitzung.

Für auf dem Bildschirm Tastaturen, verwenden Sie die Schaltfläche auf der rechten Rand der Leiste über die Tastatur zum Wechseln zwischen der Standard- und zusätzliche Tastatur.

Wenn für Ihr Gerät iOS Bluetooth aktiviert ist, erkennt der Client automatisch die Bluetooth-Tastatur.

Beachten Sie, dass aufgrund von Einschränkungen für das Betriebssystem, spezielle Tasten wie beispielsweise STRG, Option und Funktion nicht erwartungsgemäß funktioniert mit einer Bluetooth-Tastatur. Die folgenden Schlüssel verwendet werden:

- Alphanumerischen Tasten
- Pfeiltasten
- Registerkarte ": Registerkarte" funktioniert, aber die Tastenkombination UMSCHALT + Tabulatortaste funktioniert nicht
- Home / Pos1: Alt + nach-links = Home
- Ende: Alt + nach-rechts = Ende
- Bild-auf: Alt + nach-oben = Bild-auf
- Bild-ab: Alt + nach-unten = Bild-ab
- Alle auswählen: Befehl + A = STRG + A (Wählen Sie alle in den meisten Programmen)
- Ausschneiden: Befehl + X = STRG + X (Ausschneiden in den meisten Programmen)
- Kopieren: Befehl + C = STRG + C (Kopieren in den meisten Programmen)
- Einfügen: Befehl + V = STRG + V (Einfügen in den meisten Programmen)
- Symbole: Alt + alphanumerisch Schlüssel erzeugen Sie unterschiedliche Symbole abhängig von der Sprache konfiguriert

> [!TIP]
> Fragen und Kommentare sind immer Willkommen. Allerdings bitte nicht Veröffentlichen einer Anforderung für Hilfe zur Problembehandlung, mit dem Kommentarfeature am Ende dieses Artikels. Stattdessen, wechseln Sie zu der [Remotedesktop-Client-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc) , und starten Sie einen neuen Thread. Haben Sie einen Vorschlag Feature? Teilen Sie uns in der [Client-User-Voice-Forum](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android).

