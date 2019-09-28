---
title: Remotedesktop – Gewähren des Zugriffs auf Ihren PC
description: Informationen zu den Optionen für den Remotezugriff auf Ihren PC
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f1557ed-53f7-4333-b023-c8e0f4b58bf4
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6a875f8bddd934ac9fb70ca9c0b86772d9fa63b7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404174"
---
# <a name="remote-desktop---allow-access-to-your-pc"></a>Remotedesktop – Gewähren des Zugriffs auf Ihren PC

>Gilt für: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Sie können Remotedesktop verwenden, um Ihren PC mithilfe eines (für Windows, iOS, MacOS und Android verfügbaren) [Microsoft-Remotedesktopclients](remote-desktop-clients.md) mit einem Remotegerät zu verbinden und darüber zu steuern. Wenn Sie Remoteverbindungen mit Ihrem PC zulassen, können Sie ein anderes Gerät verwenden, um eine Verbindung mit Ihrem PC herzustellen, und Sie haben dann Zugriff auf alle Ihre Apps, Dateien und Netzwerkressourcen, als säßen Sie direkt an Ihrem Schreibtisch.  

> [!NOTE]
> Sie können Remotedesktop verwenden, um eine Verbindung mit Windows 10 Pro und Enterprise, Windows 8.1 und Windows 8 Enterprise und Pro, Windows 7 Professional, Enterprise und Ultimate sowie mit neueren Windows Server-Versionen als Windows Server 2008 herzustellen. Mit Computern, auf denen die Home-Edition (z. B. Windows 10 Home) ausgeführt wird, können Sie keine Verbindung herstellen. 

Damit Sie eine Verbindung mit einem Remote-PC herstellen können, müssen die folgenden Voraussetzungen erfüllt sein: Der entsprechende Computer muss eingeschaltet sein, er muss über eine Netzwerkverbindung verfügen, Remotedesktop muss aktiviert sein, Sie müssen über Netzwerkzugriff auf den Remotecomputer verfügen (dies kann über das Internet erfolgen), und Sie müssen über die Berechtigung zum Herstellen einer Verbindung verfügen. Als Voraussetzung für die Berechtigung zum Herstellen einer Verbindung müssen Sie auf der Liste der Benutzer aufgeführt sein. Bevor Sie eine Verbindung starten, ist es sinnvoll, nach dem Namen des Computers zu suchen, mit dem Sie die Verbindung herstellen, und sicherzustellen, dass Remotedesktopverbindungen über die Firewall des Computers zulässig sind.

## <a name="how-to-enable-remote-desktop"></a>So aktivieren Sie Remotedesktop

Die einfachste Möglichkeit, den Zugriff auf Ihren PC über ein Remotegerät zuzulassen, besteht darin, die Remotedesktopoptionen unter „Einstellungen“ zu verwenden. Diese Funktion wurde in Windows 10 Fall Creators Update (1709) hinzugefügt. Es steht jedoch auch eine separate herunterladbare App zur Verfügung, die eine ähnliche Funktion für frühere Versionen von Windows bereitstellt. Sie können auch die ältere Methode zum Aktivieren von Remotedesktop verwenden. Diese Methode bietet jedoch weniger Funktionalität und Überprüfungsmöglichkeiten.

### <a name="windows-10-fall-creator-update-1709-or-later"></a>Windows 10 Fall Creator Update (1709) oder höher

Sie können Ihren PC in wenigen einfachen Schritten für den Remotezugriff konfigurieren.
1. Wählen Sie auf dem Gerät, mit dem Sie eine Verbindung herstellen möchten, die Option **Start** aus, und klicken Sie dann auf der linken Seite auf das Symbol **Einstellungen**.
2. Wählen Sie die Gruppe **System** und dann das Element [**Remotedesktop**](ms-settings:remotedesktop) aus.
3. Verwenden Sie den Schieberegler, um Remotedesktop zu aktivieren.
4. Es wird außerdem empfohlen, den PC eingeschaltet zu lassen und sichtbar zu machen, um Verbindungen zu vereinfachen. Klicken Sie zum Aktivieren auf **Einstellungen anzeigen**.
5. Fügen Sie bei Bedarf Benutzer hinzu, die eine Remoteverbindung herstellen können, indem Sie auf **Benutzer auswählen, die remote auf diesen PC zugreifen können** klicken.
   1. Mitglieder der Gruppe „Administratoren“ verfügen automatisch über Zugriff.
6. Notieren Sie sich den Namen dieses Computers unter **Herstellen einer Verbindung mit diesem PC**. Sie benötigen diese Angabe zum Konfigurieren der Clients.

### <a name="windows-7-and-early-version-of-windows-10"></a>Windows 7 und eine frühe Version von Windows 10

Um Ihren PC für den Remotezugriff konfigurieren zu können, müssen Sie den [Microsoft-Remotedesktop-Assistenten](https://www.microsoft.com/download/details.aspx?id=50042) herunterladen und ausführen. Dieser Assistent aktualisiert die Systemeinstellungen, um den Remotezugriff zu aktivieren, und stellt sicher, dass Ihr Computer für Verbindungen aktiv ist und Ihre Firewall Remotedesktopverbindungen zulässt. 

### <a name="all-versions-of-windows-legacy-method"></a>Alle Versionen von Windows (ältere Methode)

Um Remotedesktop mit den älteren Systemeigenschaften zu aktivieren, folgen Sie den Anweisungen unter [Eine Verbindung mit einem anderen Computer mithilfe der Remotedesktopverbindung herstellen](https://windows.microsoft.com/windows/remote-desktop-connection-faq).

## <a name="should-i-enable-remote-desktop"></a>Sollte ich Remotedesktop aktivieren?

Wenn Sie nur auf Ihren PC zugreifen möchten, wenn Sie direkt davor sitzen, müssen Sie Remotedesktop nicht aktivieren. Durch das Aktivieren von Remotedesktop wird auf Ihrem PC ein Port geöffnet, der für Ihr lokales Netzwerk sichtbar ist. Sie sollten Remotedesktop nur in vertrauenswürdigen Netzwerken (z. B. in Ihrem Heimnetzwerk) aktivieren. Außerdem sollten Sie Remotedesktop nicht auf Computern aktivieren, auf denen der Zugriff streng kontrolliert wird.

Denken Sie daran, dass Sie durch Aktivieren des Zugriffs auf Remotedesktop allen Benutzern in der Gruppe „Administratoren“ sowie allen weiteren von Ihnen ausgewählten Benutzern die Möglichkeit einräumen, remote auf ihre Konten auf dem Computer zuzugreifen.

Sie sollten sicherstellen, dass jedes Konto mit Zugriff auf Ihren PC mit einem sicheren Kennwort konfiguriert ist.

## <a name="why-allow-connections-only-with-network-level-authentication"></a>Warum sollten Verbindungen nur mit Authentifizierung auf Netzwerkebene zulässig sein? 

Wenn Sie einschränken möchten, wer auf Ihren PC zugreifen kann, wählen Sie aus, dass der Zugriff nur mit Authentifizierung auf Netzwerkebene (Network Level Authentication, NLA) gewährt wird. Wenn Sie diese Option aktivieren, müssen sich Benutzer beim Netzwerk authentifizieren, bevor sie eine Verbindung mit Ihrem PC herstellen können. Das Zulassen von Verbindungen nur von Computern, auf denen Remotedesktop mit NLA ausgeführt wird, ist eine sicherere Authentifizierungsmethode, die Ihren Computer vor böswilligen Benutzern und Schadsoftware schützen kann. Weitere Informationen zu NLA und Remotedesktop finden Sie unter [Konfigurieren der Authentifizierung auf Netzwerkebene für Remotedesktopdienste-Verbindungen](https://technet.microsoft.com/library/cc732713(v=ws.11).aspx).

Wählen Sie diese Option nicht aus, wenn Sie eine Remoteverbindung mit einem PC in Ihrem Heimnetzwerk von außerhalb dieses Netzwerks herstellen.
