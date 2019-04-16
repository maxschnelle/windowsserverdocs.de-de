---
title: Erste Schritte mit Remotedesktop für Android
description: Grundlegende Schritte für den Remotedesktop-Client für Android einrichten.
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
ms.date: 07/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 42b4b4ffb73bd9d5d1397d32bd36c41d7e404dd7
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297429"
---
# Erste Schritte mit Remotedesktop für Android

>Gilt für: Windows 10, Windows 8.1, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2

Remotedesktop-Clients für Android können Sie direkt von Ihrem Android-Gerät mit Windows-apps und Desktops arbeiten.

Verwenden Sie die folgende Informationen, um zu beginnen. Achten Sie darauf, um die [– häufig gestellte Fragen](remote-desktop-client-faq.md) zu überprüfen, wenn Sie Fragen haben.

> [!NOTE]
> - Sie wissen die neuen Versionen für die Android-Client? Sehen Sie sich [Neuigkeiten für Remotedesktop auf Android?](android-whatsnew.md)
> Sie können den Client auf Android 4.1 und neueren Geräte und zu Chromebooks mit ChromeOS 53 installiert ausführen. Erfahren Sie mehr über Android Anwendungen auf Chrome [hier](https://sites.google.com/a/chromium.org/dev/chromium-os/chrome-os-systems-supporting-android-apps).

## Abrufen des Remotedesktop-Clients und es verwenden

Um mit Remotedesktop auf Ihrem Android-Gerät zu beginnen, gehen Sie wie folgt vor:

1. Remotedesktop-Clients von [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)herunterladen 
2. Die [Einrichtung Ihres PCs für Remoteverbindungen festlegen](remote-desktop-allow-access.md).
3. Fügen Sie eine Remotedesktopverbindung oder eine remote-Ressource. Sie eine Verbindung für die Verbindung direkt mit einem Windows-PC und eine remote-Ressource, um einen RemoteApp-Programm, eine Sitzung-basierten Desktopcomputern oder virtueller Desktop lokal veröffentlicht. 
4. Erstellen Sie ein Grafikobjekt, damit Sie Remotedesktop schnell zugreifen können.

> [!NOTE]
> Wenn Sie, die zuvor flight neue Features möchten wird empfohlen, unsere [Microsoft Remote Desktop Beta](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android.beta) -Anwendung aus dem Google Play-Store heruntergeladen. 

### Fügen Sie eine Remotedesktopverbindung

So erstellen Sie eine Remotedesktopverbindung:

1. In der Verbindung Center tippen **+**, und tippen Sie dann auf **Desktop**.
2. Geben Sie die folgende Informationen für den Computer, um eine Verbindung herstellen möchten:
  - **PC-Name** – der Name des Computers. Dies kann es sich um einen Windows-Computernamen, ein Internetdomänenname oder einer IP-Adresse sein. Sie können auch auf den PC-Namen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**) Portinformationen anfügen.
  - **Benutzername** – den Benutzernamen zu verwenden, um die remote-PC zuzugreifen. Sie können die folgenden Formate: *Benutzername*, *Domäne\Benutzername*oder *user_name@domain.com*. Sie können auch angeben, ob für einen Benutzernamen und Kennwort auffordern.
3. Sie können auch die folgenden zusätzlichen Optionen festlegen:
  - **Anzeigename** – eine leicht zu merkenden Namen für den PC herstellen. Sie können eine beliebige Zeichenfolge verwenden, aber der PC-Name wird angezeigt, wenn Sie einen Anzeigenamen nicht angeben.
  - **Gateway** – der Remotedesktop-Gateway, das Sie zum Herstellen einer virtuellen Desktops, RemoteApp-Programme und Sitzung-basierte Desktops auf einem internen Firmennetzwerk verwenden möchten. Erhalten Sie die Informationen über das Gateway von Ihr Systemadministrator.
    Möchten Sie eine Remote Desktop-Gateway zu konfigurieren?
  - **Sound** – wählen Sie das Gerät für Audio während der Remotesitzung verwendet. Sie können auswählen, um auf lokalen Geräten, auf dem Remotegerät oder gar wiederzugeben.
  - Legen eine benutzerdefinierte Auflösung für eine Verbindung **Anpassen Bildschirmauflösung** - diese Einstellung aktivieren. Wenn deaktiviert die Auflösung angewendet wird die Sie in den globalen Einstellungen der app definiert haben.
  - **Maustasten Swap** – verwenden Sie diese Option, um die linke Maustaste Schaltflächenfunktionen für die rechte Maustaste auszutauschen. (Dies ist besonders hilfreich, wenn die remote-PC für ein linkshändiges Benutzer konfiguriert ist eine rechtshändige Maus zu verwenden.)
  - **Verbinden mit Admin-Sitzung** – verwenden Sie diese Option zum Herstellen einer Konsolen-Sitzung auf einen Windows-Server zu verwalten.
  - **In lokalen Speicher umgeleitet** – stellt Ihren lokalen Speicher als eine remote-Dateisystem auf dem remote-PC bereit.
4. Tippen Sie auf **Speichern**.

Möchten Sie diese Einstellungen bearbeiten? Tippen Sie auf das Überlaufmenü (**...**) neben dem Namen des Desktops, und tippen Sie dann auf **Bearbeiten**.

Die Verbindung löschen möchten? Erneut, tippen Sie auf das Überlaufmenü (**...**), und tippen Sie dann auf **Entfernen**.

>[!TIP]
> Wenn Sie Fehler 0xf07 erhalten, über eine Kennworteingabe ("Wir konnten nicht mit dem remote-PC verbinden das Kennwort für das Benutzerkonto ist abgelaufen"), Ändern des Kennworts, und versuchen Sie es erneut.

### Fügen Sie eine remote-Ressource
Remote-Ressourcen sind RemoteApp-Programme, Sitzung-basierte Desktops und virtuelle Desktops mit RemoteApp und Desktop Connections veröffentlicht.

So fügen Sie eine remote-Ressourcen hinzu:

1. Tippen Sie auf dem Bildschirm Verbindung Center auf **+**, und tippen Sie dann auf **Remote-Ressourcen-Feed**. 
2. Geben Sie die Informationen für die Remote-Ressourcen:
   - **E-Mail oder URL** - die URL des Web Access für Remotedesktop-Servers. Sie Ihre unternehmenseigenen e-Mail-Konto auch in diesem Feld – eingeben können, weist dies den Client für den Remotedesktop-Web-Server Ihrer e-Mail-Adresse zugeordnet zu suchen.
   - **Benutzername** - der Benutzername für das Web Access für Remotedesktop-Server zu verwenden, die Sie zum Verbinden.
   - **Kennwort** : das Kennwort für das Web Access für Remotedesktop-Server zu verwenden, die Sie zum Verbinden.
3. Tippen Sie auf **Speichern**.

Die remote-Ressourcen werden in der Mitte Verbindung angezeigt.


So löschen Sie remote-Ressourcen:

1. Tippen Sie auf das Überlaufmenü (**...**) neben der remote-Ressource, in der Mitte Verbindung.
2. Tippen Sie auf **Entfernen**.
3. Bestätigen Sie den Vorgang.

### Widgets – anheften einen gespeicherten Desktop-zu-Ihre Startseite

Die Remote Desktop-Anwendungen unterstützen zum Anheften von Verbindungen zu Ihrer Startseite mithilfe des Features Android Widgets. Die Möglichkeit, dass Sie ein Grafikobjekt hinzufügen, hängt von den Typ des verwendeten Android-Gerät und seines Betriebssystems ab. Hier ist die am häufigsten verwendete Methode zum Widgets hinzufügen: 

1. Tippen Sie auf **apps** , um das Menü "apps" zu starten.
2. Tippen Sie auf **Widgets**.
3. Wischen Sie über die Widgets und suchen Sie nach der Remotedesktop-Symbol in der Beschreibung "Pin Remote Desktop".
4. Tippen Sie auf halten Sie diese Remotedesktop-Widgets und verschieben Sie diese auf dem Startbildschirm aus.
5. Wenn Sie das Symbol loslassen, sehen Sie die gespeicherten Remotedesktops. Wählen Sie die Verbindung, die Sie an Ihre Startseite speichern möchten.

Sie können nun die Remotedesktopverbindung direkt aus Ihrer Startseite beginnen, durch Tippen.

> [!NOTE]
> Wenn Sie die desktop-Verbindung in der Remotedesktop-Anwendung umbenennen, wird die Beschriftung des diese angehefteten Remotedesktop nicht aktualisiert.

## Verbinden Sie mit einem RD-Gateway auf interne Ressourcen zugreifen

Ein Remotedesktopgateway (RD-Gateway) können Sie die Verbindung mit eines Remotecomputer in einem Unternehmensnetzwerk von jedem beliebigen Standort auf das Internet. Sie erstellen und Verwalten Ihrer Gateways über den Remotedesktopclient.

So richten ein neues gateway

1. Tippen Sie in der Mitte Verbindung auf **Einstellungen > Gateways**. Tippen Sie auf **+** ein neues Gateway hinzufügen.
2. Geben Sie die folgenden Informationen ein:
  - **Servername** – den Namen des Computers, den Sie als Gateway verwenden möchten. Dies kann es sich um einen Windows-Computernamen, ein Internetdomänenname oder einer IP-Adresse sein. Sie können auch die Portinformationen hinzufügen, um den Namen des Servers (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
  - **Benutzername** - Benutzername und Kennwort für den Remotedesktopgateway verwendet werden, der an angeschlossen sind. Sie können auch die **desktop-Benutzerkonto verwenden** , um dieselben Anmeldeinformationen verwenden, als die für die Remotedesktopverbindung auswählen.

## Verwalten von Benutzerkonten

Wenn Sie auf einem desktop oder remote-Ressourcen zugreifen, können Sie die Benutzerkonten Auswahl aus erneut speichern. Sie können auch Benutzerkonten definieren, in der Client selbst, im Gegensatz zu den Daten des Benutzers speichern, beim Herstellen einer Verbindung mit eines Desktops.

So erstellen Sie ein neues Benutzerkonto:

1. Tippen Sie auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**, in der Mitte Verbindung.
2. Tippen Sie auf **+** ein neues Benutzerkonto hinzufügen.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername** - der Name des Benutzers für die Verwendung mit eine Remoteverbindung zu speichern. Sie können den Benutzernamen eingeben, in den folgenden Formaten: Benutzername, Domäne\Benutzername, oder user_name@domain.com.
   - **Kennwort** : das Kennwort für den Benutzer, die, den Sie angegeben. Jedes Benutzerkonto, die Sie speichern, um für Remoteverbindungen verwenden möchten, muss ein Kennwort zugeordnet ist.
4. Tippen Sie auf **Speichern**.

So löschen Sie ein Benutzerkonto

1. Tippen Sie in der Mitte Verbindung auf **Einstellungen > Benutzerkonten**.
2. Tippen Sie und halten Sie ein Benutzerkonto in der Liste, um es auszuwählen. Sie können mehrere Benutzer auswählen.
3. Tippen Sie auf der Papierkorb können, um die ausgewählten Benutzer löschen.

## Navigieren Sie der Remotedesktop-Sitzung
Wenn Sie eine Remotedesktopverbindung starten, stehen Tools zur Verfügung, die Sie verwenden können, um die Sitzung zu navigieren.

### Starten Sie eine Remotedesktopverbindung

1. Tippen Sie auf der Remotedesktop-Verbindung, um die Sitzung zu starten. 
2. Wenn Sie, zum Überprüfen des Zertifikats für den Remotedesktop gefragt werden, tippen Sie auf " **Verbinden**". Sie können auch **nicht erneut zur Verbindung mit diesem Computer auffordern** , um das Zertifikat immer akzeptieren auswählen.

### Verwalten von globalen Appeinstellungen

Sie können die folgenden globale Einstellungen in Ihrem Android-Client festlegen:

- **Desktop-Vorschau anzeigen** - gibt Aufschluss über eine Vorschau von einem Desktop in der Mitte der Verbindung, bevor Sie eine Verbindung damit hergestellt. Standardmäßig ist dies **auf**fest.
- **Zusammendrücken Zoom** - können Sie für das Zoomen zusammendrücken Gesten. Wenn die app, die Sie über Remotedesktop verwenden (eingeführt in Windows 8) Multi-Touch unterstützt, aktivieren Sie diese Einstellung **Deaktivieren**.
- **Hilfe zur Verbesserung der Remotedesktop** - sendet anonyme Daten an Microsoft. Wir verwenden diese Daten, um den Client zu verbessern. Sie erfahren, wie wir diese anonymen, privaten Daten behandeln, finden Sie unter der [Remote Desktop Client Datenschutzbestimmungen von Microsoft](https://www.microsoft.com/privacystatement/RemoteApp/Default.aspx). Standardmäßig ist diese Einstellung **auf**.
- Das **Anzeigen** – es gibt zwei globale Einstellungen für die Anzeige:
   - **Ausrichtung** – festgelegt die bevorzugte Ausrichtung (Quer- oder Hochformat entsprechen) für Ihre Sitzung. 
   >[!NOTE]
   > Wenn Sie mit einem PC mit Windows 8 oder eine ältere Version von Windows zu verbinden, wird die Sitzung nicht ordnungsgemäß skaliert. Am besten ist auf dem PC, und wieder in der Ausrichtung, die Sie verwenden möchten. Eine noch bessere Möglichkeit besteht darin, mindestens upgrade des PCs auf Windows 8.1.

   - **Auflösung** : Legt die Auflösung, die Sie für desktop-Verbindungen Global verwenden möchten. Wenn Sie bereits eine benutzerdefinierte Lösung für eine einzelne app oder die Verbindung eingerichtet haben, ändert diese Einstellung, die sich nicht.
   >[!NOTE]
   >Wenn Sie eine der Anzeigeeinstellungen ändern, gelten diese nur für neue Verbindungen von diesem Punkt auf. Damit die Änderung in einer Sitzung angezeigt, die Sie bereits verbunden sind, um zu trennen und dann erneut eine Verbindung herzustellen.

### Symbolleiste Verbindung

Die Verbindung Leiste erhalten Sie Zugriff auf zusätzliche Navigationssteuerelementen. Standardmäßig wird die Symbolleiste Verbindung in der Mitte am oberen Rand des Bildschirms platziert. Doppeltippen und ziehen Sie die Leiste nach links oder rechts, um es zu bewegen.

- **Schwenken-Steuerelement**: Das Schwenksteuerelement ermöglicht den Bildschirm vergrößert und anders angeordnet werden. Beachten Sie, dass Schwenken-Steuerelement nur per direct verfügbar ist.
   - Aktivieren / Deaktivieren der Schwenken-Steuerelement: Tippen Sie auf das Schwenken-Symbol auf der Verbindungsleiste zum Anzeigen des Steuerelements verschieben und vergrößern/verkleinern des Bildschirms. Tippen Sie auf das Schwenken-Symbol auf der Verbindungsleiste erneut aus, um das Steuerelement ausblenden und den Bildschirm an der ursprünglichen Auflösung zurückzugeben.
   - Verwenden Sie das Schwenksteuerelement: Tippen und halten heruntergezogen steuern und ziehen Sie dann in die Richtung, möchten Sie den Bildschirm zu verschieben.
   - Verschieben Sie das Schwenksteuerelement: Doppeltippen und halten Sie das Schwenksteuerelement, das Steuerelement auf dem Bildschirm zu verschieben.
- **Zusätzliche Optionen**: Tippen Sie auf das Symbol zusätzliche Optionen zum Anzeigen der Sitzung Auswahl Leiste und Befehl Leiste (siehe unten).
- **Tastatur**: Tippen Sie auf das Tastatursymbol ein-oder Ausblenden der Tastatur. Schwenken-Steuerelement wird automatisch angezeigt, wenn die Bildschirmtastatur angezeigt wird.
- **Verschieben Sie die Symbolleiste Verbindung**: Tippen und halten Sie die Symbolleiste Verbindung und dann Drag & Drop an eine neue Position am oberen Rand des Bildschirms.


### Befehlsleiste

Tippen Sie auf die Symbolleiste Verbindung, um die Befehlsleiste auf der rechten Seite des Bildschirms angezeigt werden soll. Sie können zwischen den Modi Maus (direkte Touch und Mauszeiger) wechseln. Verwenden Sie die Schaltfläche "Startseite", um die Verbindung Center aus der Befehlsleiste zurückzugeben. Alternativ können Sie die Schaltfläche "zurück" für dieselbe Aktion. Die aktive Sitzung wird nicht getrennt werden. 


### Direkte Verwendung touch Gesten und Maus-Modi in einer Remotesitzung

Der Client verwendet standard Touchgesten. Sie können auch Touchgesten verwenden, Mausaktionen auf dem Remotedesktop replizieren. Die verfügbaren Maus-Modi werden in der folgenden Tabelle definiert.

> [!NOTE]
> Interaktion mit Windows 8 oder höher werden die systemeigenen Touchgesten im direkten Touch-Modus unterstützt. 

| Mausmodus    | Maus-Vorgang      | Geste                                                               |
|---------------|----------------------|-----------------------------------------------------------------------|
| Direkte Toucheingabe  | Linksklick           | 1 Fingern tippen                                                          |
| Direkte Toucheingabe  | Rechtsklick          | 1 Fingern tippen und halten                                                 |
| Mauszeiger | Zoom                 | Verwenden Sie 2 Finger, und um vergrößern oder zu verschieben Finger voneinander um zu verkleinern zusammendrücken. |
| Mauszeiger | Linksklick           | 1 Fingern tippen                                                          |
| Mauszeiger | Linksklick und ziehen  | Ziehen Sie 1 Finger double tippen und halten,                               |
| Mauszeiger | Rechtsklick          | 2 Fingern tippen                                                          |
| Mauszeiger | Rechtsklick und ziehen | 2 Finger double tippen und halten, ziehen Sie                               |
| Mauszeiger | Mausrad          | 2 Finger tippen und halten und ziehen Sie nach oben oder unten                           |

> [!TIP]
> Fragen und Kommentare sind immer Willkommen. Allerdings bitte nicht Veröffentlichen einer Anforderung für Hilfe zur Problembehandlung, mit dem Kommentarfeature am Ende dieses Artikels. Stattdessen, wechseln Sie zu der [Remotedesktop-Client-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc) , und starten Sie einen neuen Thread. Haben Sie einen Vorschlag Feature? Teilen Sie uns in der [Client-User-Voice-Forum](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android).
