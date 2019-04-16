---
title: Erste Schritte mit Remotedesktop unter Windows
description: Grundlegende Schritte für den Remotedesktop-Client für Windows einrichten.
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
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1c06e2eca725a825ac0fa4c7b617a26d89c898ff
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297459"
---
# Erste Schritte mit Remotedesktop unter Windows

>Gilt für: Windows 10, Windows 8.1, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2

Sie können den Remotedesktop-Client für Windows verwenden, zum Arbeiten mit Windows-apps und Desktops Remote von einem anderen Windows-Gerät.

Verwenden Sie die folgende Informationen, um zu beginnen. Achten Sie darauf, um die [– häufig gestellte Fragen](remote-desktop-client-faq.md) zu überprüfen, wenn Sie Fragen haben.

> [!NOTE]
> - Sie wissen die neuen Versionen für den Windows-Client? Sehen Sie sich [Neuigkeiten für Remotedesktop auf Windows?](windows-whatsnew.md)
> - Sie können den Client auf eine beliebige Version von Windows 10 ausführen.

## Abrufen des Remotedesktop-Clients und es verwenden

Um mit Remotedesktop auf Ihrem Windows 10-Gerät zu beginnen, gehen Sie wie folgt vor:

1. Herunterladen des Remotedesktop-Clients aus dem [Microsoft Store](https://www.microsoft.com/store/p/microsoft-remote-desktop/9wzdncrfj3ps). 
2. Die [Einrichtung Ihres PCs für Remoteverbindungen festlegen](remote-desktop-allow-access.md).
3. Fügen Sie eine Remotedesktopverbindung oder eine remote-Ressource. Sie verwenden eine Verbindung direkt auf einem Windows-PC und eine remote-Ressource RemoteApp-Programme, Sitzung-basierten Desktopcomputern oder virtueller Desktop, die Veröffentlichung von Ihrem Administrator. 
4. Anheften Sie Elemente, damit Sie schnell mit Remotedesktop abrufen können.

### Fügen Sie eine Remotedesktopverbindung

So erstellen Sie eine Remotedesktopverbindung:

1. Tippen Sie auf **+ Hinzufügen**, und tippen Sie dann auf **Desktop**, in der Mitte der Verbindung.
2. Geben Sie die folgende Informationen für den Computer, um eine Verbindung herstellen möchten:
  - **PC-Name** – der Name des Computers. Dies kann es sich um einen Windows-Computernamen, ein Internetdomänenname oder einer IP-Adresse sein. Sie können auch auf den PC-Namen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**) Portinformationen anfügen.
  - **Benutzerkonto** – das Benutzerkonto mit den remote-PC zugreifen. Tippen Sie auf **+** ein neues Konto hinzufügen, oder wählen Sie ein vorhandenes Konto. Sie können die folgenden Formate für den Benutzernamen: *Benutzername*, *Domäne\Benutzername*oder *user_name@domain.com*. Sie können auch angeben, ob für einen Benutzernamen und Kennwort bei der Verbindung auffordern, **jedes Mal nachfragen**.
3. Sie können auch zusätzliche Optionen festlegen, durch Tippen auf **Weitere anzeigen**:
  - **Der Anzeigename des** – eine leicht zu merkenden Namen für den PC herstellen. Sie können eine beliebige Zeichenfolge verwenden, aber der PC-Name wird angezeigt, wenn Sie einen Anzeigenamen nicht angeben.
  - **Gruppe** – Geben Sie eine Gruppe zu vereinfachen, die Verbindungen später zu suchen. Sie können eine neue Gruppe hinzufügen, durch Tippen auf **+** oder aus der Liste auswählen.
  - **Gateway** – der Remotedesktop-Gateway, das Sie zum Herstellen einer virtuellen Desktops, RemoteApp-Programme und Sitzung-basierte Desktops auf einem internen Firmennetzwerk verwenden möchten. Erhalten Sie die Informationen über das Gateway von Ihr Systemadministrator.
  - **Verbinden mit Admin-Sitzung** – verwenden Sie diese Option zum Herstellen einer Konsolen-Sitzung auf einen Windows-Server zu verwalten.
  - **Maustasten Swap** – verwenden Sie diese Option, um die linke Maustaste Schaltflächenfunktionen für die rechte Maustaste auszutauschen. (Dies ist besonders hilfreich, wenn die remote-PC für ein linkshändiges Benutzer konfiguriert ist eine rechtshändige Maus zu verwenden.)
  - **Auf Meine Remotesitzung Auflösung festgelegt:** – wählen Sie die Auflösung, die Sie in der Sitzung verwenden möchten. **Für mich auswählen** , wird die Auflösung basierend auf der Größe des Clients festgelegt.
  - **Ändern der Größe der Anzeige:** – Wenn Sie eine hohe statische Auflösung für die Sitzung auswählen, haben Sie die Möglichkeit, Elemente auf dem Bildschirm angezeigt, um die Lesbarkeit zu verbessern. Hinweis: Dies gilt nur, wenn Windows 8.1 oder höher eine Verbindung herstellt.
  - **Aktualisieren Sie die Remotesitzung Auflösung auf ihre Größe ändern** – Wenn aktiviert, wird der Client dynamisch die Sitzung Auflösung basierend auf der Größe des Clients aktualisieren. Hinweis: Dies gilt nur, wenn Windows 8.1 oder höher eine Verbindung herstellt.
  - **Zwischenablage** – Wenn aktiviert, können Sie Text und Bilder in die remote-PC zu kopieren.
  - **Audiowiedergabe** – wählen Sie das Gerät für Audio während der Remotesitzung verwendet. Sie können auswählen, um auf den lokalen Geräten, remote-PC oder gar wiederzugeben.
  - **Audioaufnahme** – Wenn aktiviert, können Sie eine lokale Mikrofon mit Anwendungen auf die remote-PC verwenden.
4. Tippen Sie auf **Speichern**.

Möchten Sie diese Einstellungen bearbeiten? Tippen Sie auf das Überlaufmenü (**...**) neben dem Namen des Desktops, und tippen Sie dann auf **Bearbeiten**.

Die Verbindung löschen möchten? Erneut, tippen Sie auf das Überlaufmenü (**...**), und tippen Sie dann auf **Entfernen**.

### Fügen Sie eine remote-Ressource
Remote-Ressourcen sind RemoteApp-Programme, Sitzung-basierte Desktops und virtuelle Desktops, die von Ihrem Administrator mit Remote Desktop Services veröffentlicht.

So fügen Sie eine remote-Ressourcen hinzu:

1. Klicken Sie auf dem Bildschirm Verbindung Center Tippen Sie **+ Hinzufügen**, und tippen Sie dann auf **Remote-Ressourcen**. 
2. Geben Sie den **Feed-URL** , die von Ihrem Administrator bereitgestellt, und tippen Sie auf **Feeds suchen**.
3. Wenn Sie aufgefordert werden, geben Sie die Anmeldeinformationen verwenden, um den Feed zu abonnieren.

Die remote-Ressourcen werden in der Mitte Verbindung angezeigt.


So löschen Sie remote-Ressourcen:

1. Tippen Sie auf das Überlaufmenü (**...**) neben der remote-Ressource, in der Mitte Verbindung.
2. Tippen Sie auf **Entfernen**.

### Einen gespeicherten Desktop-zu-Startmenü anheften

Um eine Verbindung mit Ihrer Menü "Start" anzuheften, tippen Sie auf das Überlaufmenü (**...**) neben dem Namen des Desktops, und tippen Sie dann auf **an "Start" anheften**.

Jetzt können Sie die Remotedesktopverbindung direkt über das Startmenü starten, durch Tippen.

## Verbinden Sie mit einem RD-Gateway auf interne Ressourcen zugreifen

Ein Remotedesktopgateway (RD-Gateway) können Sie die Verbindung mit eines Remotecomputer in einem Unternehmensnetzwerk von jedem beliebigen Standort auf das Internet. Sie erstellen und Verwalten Ihrer Gateways über den Remotedesktopclient.

So richten ein neues gateway

1. Tippen Sie in der Mitte Verbindung auf **Einstellungen**.
2. Neben Gateway, tippen Sie auf **+** ein neues Gateway hinzufügen. Hinweis: Ein Gateway kann auch hinzugefügt werden, wenn Sie eine neue Verbindung hinzufügen.
3. Geben Sie die folgenden Informationen ein:
  - **Servername** – den Namen des Computers, den Sie als Gateway verwenden möchten. Dies kann es sich um einen Windows-Computernamen, ein Internetdomänenname oder einer IP-Adresse sein. Sie können auch die Portinformationen hinzufügen, um den Namen des Servers (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
  - **Benutzerkonto** - wählen, oder fügen Sie ein Benutzerkonto mit den Remotedesktopgateway verwenden Sie eine Verbindung herstellen. Sie können auch die **desktop-Benutzerkonto verwenden** , um dieselben Anmeldeinformationen verwenden, als die für die Remotedesktopverbindung auswählen.
4. Tippen Sie auf **Speichern**.  

## Globale app-Einstellungen

Sie können die folgenden globale Einstellungen in Ihrem Client durch Tippen auf **Einstellungen**festlegen:

ELEMENTE VERWALTET
- **Benutzerkonto** – so können Sie hinzufügen, zu bearbeiten und Löschen von Benutzerkonten, die in der Client gespeichert. Dies ist eine gute Möglichkeit, aktualisieren Sie das Kennwort für ein Konto ein, nachdem es geändert wurde.
- **Gateway** - ermöglicht Ihnen das Hinzufügen, bearbeiten und Löschen von Gatewayservern, die in der Client gespeichert.
- **Gruppe** – so können Sie hinzufügen, zu bearbeiten und Löschen von Gruppen, die in der Client gespeichert. Damit können Sie einfach die Gruppe-Verbindungen.

SITZUNGSEINSTELLUNGEN
- **Verbindungen im Vollbildmodus starten** - Wenn aktiviert, wenn eine Verbindung gestartet wird, wird der Client den gesamten Bildschirm des aktuellen Bildschirms verwenden.
- **Starten Sie jede Verbindung in einem neuen Fenster** - aktiviert ist, jede Verbindung wird gestartet, wenn in einem eigenen Fenster, sodass Sie sie auf verschiedenen Bildschirmen platzieren, und wechseln Sie zwischen ihnen die Verwendung der Taskleiste.
- **Beim Ändern der Größe der app:** -können Sie steuern, was geschieht, wenn der Client Fenstergröße ist. Die Standardeinstellung ist **den Inhalt, unter Beibehaltung des Seitenverhältnisses**gestreckt.
- **Tastaturbefehle mit verwenden:** -wir Sie angeben, wo Tastaturbefehle wie *gewinnen* oder *ALT + TAB* verwendet werden. Standardmäßig wird diese in der Sitzung senden nur wenn die Verbindung im vollständigen Scren befindet.
- **Die Anzeige des Timeout** - können Sie verhindern, dass den Bildschirm Timeout, wenn eine Sitzung aktiv ist. Dies ist hilfreich, wenn die Verbindung kein Eingriff für längere Zeit benötigt.

APP-EINSTELLUNGEN
- **Desktop-Vorschau anzeigen** - gibt Aufschluss über eine Vorschau von einem Desktop in der Mitte der Verbindung, bevor Sie eine Verbindung damit hergestellt. Standardmäßig ist dies **auf**fest.
- **Verbessern von Remotedesktop** - sendet anonyme Daten an Microsoft. Wir verwenden diese Daten, um den Client zu verbessern. Weitere Informationen zu wie wir diese anonymen, privaten Daten behandeln, finden Sie unter der [Datenschutzbestimmungen von Microsoft](https://privacy.microsoft.com/en-us/privacystatement). Standardmäßig ist diese Einstellung **auf**.

### Verwalten von Benutzerkonten

Wenn Sie auf einem desktop oder remote-Ressourcen zugreifen, können Sie die Benutzerkonten Auswahl aus erneut speichern. Sie können auch Benutzerkonten definieren, in der Client selbst, im Gegensatz zu den Daten des Benutzers speichern, beim Herstellen einer Verbindung mit eines Desktops.

So erstellen Sie ein neues Benutzerkonto:

1. Tippen Sie in der Mitte Verbindung auf **Einstellungen**.
2. Neben dem Benutzerkonto, tippen Sie auf **+** ein neues Benutzerkonto hinzufügen.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername** : der Name des Benutzers für die Verwendung mit eine Remoteverbindung zu speichern. Sie können den Benutzernamen eingeben, in den folgenden Formaten: Benutzername, Domäne\Benutzername, oder user_name@domain.com.
   - **Kennwort** : das Kennwort für den Benutzer, die, den Sie angegeben. Dies kann während der Verbindung eines Kennworts aufgefordert werden leer sein.
4. Tippen Sie auf **Speichern**.

So löschen Sie ein Benutzerkonto

1. Tippen Sie in der Mitte Verbindung auf **Einstellungen**.
2. Wählen Sie das Konto aus der Liste unter Benutzerkonto löschen.
3. Neben dem Benutzerkonto Tippen Sie auf das Symbol "Bearbeiten".
4. Tippen Sie auf **dieses Konto entfernen** , unten, um das Benutzerkonto löschen.
5. Sie können auch Bearbeiten des Benutzerkontos und tippen Sie auf **Speichern**.

## Navigieren Sie der Remotedesktop-Sitzung
Wenn Sie eine Remotedesktopverbindung starten, stehen Tools zur Verfügung, die Sie verwenden können, um die Sitzung zu navigieren.

### Starten Sie eine Remotedesktopverbindung

1. Tippen Sie auf der Remotedesktop-Verbindung, um die Sitzung zu starten.
2. Wenn Sie Anmeldeinformationen für die Verbindung gespeichert haben, werden Sie aufgefordert, einen **Benutzernamen** und **Kennwort**bereitzustellen.
3. Wenn Sie zum Überprüfen des Zertifikats für den Remotedesktop gefragt werden, überprüfen Sie die Informationen, und sicherzustellen Sie, dass dies ein PC ist Sie vor dem tippen **Connect**vertrauen. Sie können auch **nicht über dieses Zertifikat erneut Fragen** , um dieses Zertifikat immer akzeptieren auswählen.

### Symbolleiste Verbindung

Die Verbindung Leiste erhalten Sie Zugriff auf zusätzliche Navigationssteuerelementen. Standardmäßig wird die Symbolleiste Verbindung in der Mitte am oberen Rand des Bildschirms platziert. Tippen Sie auf, und ziehen Sie die Leiste nach links oder rechts, um es zu bewegen.

- **Schwenken-Steuerelement** - Schwenken-Steuerelement können den Bildschirm vergrößert und anders angeordnet werden. Beachten Sie, dass Schwenken-Steuerelement nur auf die Toucheingabe aktivierten Geräten und mit dem direkte Toucheingabe-Modus verfügbar ist.
   - Aktivieren / Deaktivieren der Schwenken-Steuerelement: Tippen Sie auf das Schwenken-Symbol auf der Verbindungsleiste zum Anzeigen des Steuerelements verschieben und vergrößern/verkleinern des Bildschirms. Tippen Sie auf das Schwenken-Symbol auf der Verbindungsleiste erneut aus, um das Steuerelement ausblenden und den Bildschirm an der ursprünglichen Auflösung zurückzugeben.
   - Verwenden Sie das Schwenksteuerelement - tippen halten Sie das Schwenksteuerelement und ziehen Sie dann in die Richtung, möchten Sie den Bildschirm zu verschieben.
   - Verschieben Sie das Schwenksteuerelement - Doppeltippen, und halten Sie das Schwenksteuerelement, das Steuerelement auf dem Bildschirm zu verschieben.
- **Zusätzliche Optionen** : Tippen Sie auf das Symbol zusätzliche Optionen für die Sitzung Auswahl Leiste und Befehl Leiste (siehe unten) angezeigt.
- **Tastatur** - Tippen Sie auf das Symbol "Tastatur" zum Anzeigen oder Ausblenden der Bildschirmtastatur. Schwenken-Steuerelement wird automatisch angezeigt, wenn die Bildschirmtastatur angezeigt wird.

### Befehlsleiste

Tippen Sie auf die **...** auf der Verbindungsleiste die Befehlsleiste auf der rechten Seite des Bildschirms angezeigt.

- **Home** - Verwendung der Home-Schaltfläche, aus der Befehlsleiste in die Mitte der Verbindung zurückgegeben werden sollen.
  - Alternativ können Sie die Schaltfläche "zurück" für dieselbe Aktion.
  - Die aktive Sitzung wird nicht getrennt werden.
  - Dadurch können Sie zusätzliche Verbindungen zu starten.
- **Zum Trennen** - verwenden Sie die Schaltfläche zum Trennen, um die Verbindung zu beenden.
  - Ihre apps werden aktiv bleiben, solange die Sitzung nicht auf die remote-PC beendet wird.
- **Vollbild-** - betritt oder verlässt Vollbildmodus.
- **Touch /-Maus** – Sie können zwischen den Modi Maus (direkte Touch und Mauszeiger) wechseln.

### Direkte Verwendung touch Gesten und Maus-Modi in einer Remotesitzung

Es sind zwei Maus-Modi Interaktion mit der Sitzung verfügbar.
- **Direkte Toucheingabe**: übergibt alle des touchkontakts in der Sitzung Remote interpretiert werden.
  - In die gleiche Weise wie Windows mit Touchscreen verwendet.
- **Mauszeiger**: Transformationen Ihrer lokalen Touchscreen in einem großen Touchpad ermöglicht, einen Mauszeiger in der Sitzung.
  - Wird verwendet, auf die gleiche Weise, die Sie mit einem Touchpad Entwicklungskit verwenden würden.

> [!NOTE]
> Interaktion mit Windows 8 oder höher werden die systemeigenen Touchgesten im direkten Touch-Modus unterstützt. 

| Mausmodus    | Maus-Vorgang      | Geste                                                               |
|---------------|----------------------|-----------------------------------------------------------------------|
| Direkte Toucheingabe  | Linksklick           | 1 Fingern tippen                                                          |
| Direkte Toucheingabe  | Rechtsklick          | 1 Fingern tippen und halten                                                 |
| Mauszeiger | Linksklick           | 1 Fingern tippen                                                          |
| Mauszeiger | Linksklick und ziehen  | Ziehen Sie 1 Finger double tippen und halten,                               |
| Mauszeiger | Rechtsklick          | 2 Fingern tippen                                                          |
| Mauszeiger | Rechtsklick und ziehen | 2 Finger double tippen und halten, ziehen Sie                               |
| Mauszeiger | Mausrad          | 2 Finger tippen und halten und ziehen Sie nach oben oder unten                           |
| Mauszeiger | Zoom                 | Verwenden Sie 2 Finger, und um vergrößern oder zu verschieben Finger voneinander um zu verkleinern zusammendrücken. |

> [!TIP]
> Fragen und Kommentare sind immer Willkommen. Allerdings bitte nicht Veröffentlichen einer Anforderung für Hilfe zur Problembehandlung, mit dem Kommentarfeature am Ende dieses Artikels. Stattdessen, wechseln Sie zu der [Remotedesktop-Client-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc) , und starten Sie einen neuen Thread. Haben Sie einen Vorschlag Feature? Teilen Sie uns über die [Feedback-Hub](feedback-hub://?tabid=2&contextid=605).
