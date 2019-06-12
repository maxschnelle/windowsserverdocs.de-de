---
title: Remotedesktop - Zugriff auf Ihren PC zulassen
description: Erfahren Sie mehr über die Optionen für den Remotezugriff auf Ihren PC
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d03dcd307696aea55ab6a1569ab907635994772a
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804988"
---
# <a name="remote-desktop---allow-access-to-your-pc"></a>Remotedesktop - Zugriff auf Ihren PC zulassen

>Gilt für: Windows 10, Windows 8.1, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2

Sie können Remotedesktop verwenden, eine Verbindung herstellen und Ihr PC von einem Remotegerät zu steuern, indem eine [Microsoft-Remotedesktopclient](remote-desktop-clients.md) (für Windows, iOS, MacOS und Android verfügbar). Wenn Sie Remoteverbindungen auf Ihren PC gewähren, können Sie ein anderes Gerät verwenden, um eine Verbindung mit Ihrem PC herstellen und haben Zugriff auf alle Ihre apps, Dateien und Netzwerkressourcen, als säßen Sie am Schreibtisch.  

> [!NOTE]
> Sie können Remotedesktop verwenden, zur Verbindung mit Windows 10 Pro und Enterprise, Windows 8.1 und 8 Enterprise und Pro, Windows 7 Professional, Enterprise und Ultimate und Windows Server-Versionen höher als Windows Server 2008. Sie können nicht auf Computern mit der Home-Edition (z. B. Windows 10 Home) eine Verbindung herstellen. 

Verbindung mit einem remote-PC, dass der Computer muss aktiviert sein, er muss über eine Netzwerkverbindung verfügen, Remote Desktop muss aktiviert sein, müssen Sie über das Netzwerk zugreifen auf den Remotecomputer (Dies kann über das Internet sein), und Sie benötigen die Berechtigung, eine Verbindung herstellen. Für die Berechtigungen für eine Verbindung herstellen müssen Sie in der Liste der Benutzer sein. Bevor Sie eine Verbindung zu starten, ist es eine gute Idee, um den Namen des Computers zu suchen, die Sie die Verbindung herstellen und Sie sicherstellen, dass Remotedesktop-Verbindungen über die Firewall zugelassen werden.

## <a name="how-to-enable-remote-desktop"></a>Gewusst wie: Aktivieren von Remotedesktop

Die einfachste Möglichkeit, den Zugriff auf Ihren PC von einem Remotegerät zu ermöglichen, wird die Remotedesktop-Optionen unter "Einstellungen" verwendet. Da diese Funktion in das Windows 10 Fall Creators Update (1709), eine Separate, herunterladbare hinzugefügt wurde, dass die app auch zur Verfügung steht bereitstellt, ähnliche Funktionalität wie bei früheren Versionen von Windows. Sie können auch die herkömmliche Weise aktivieren Sie Remotedesktop verwenden, aber diese Methode weniger Funktionen und die Validierung bereitstellt.

### <a name="windows-10-fall-creator-update-1709-or-later"></a>Windows 10 Fall creators Update (1709) oder höher

Sie können Ihren PC für den Remotezugriff mit wenigen einfachen Schritten konfigurieren.
1. Wählen Sie auf dem Gerät, um eine Verbindung herstellen möchten, **starten** und dann auf die **Einstellungen** Symbol auf der linken Seite.
2. Wählen Sie die **System** Gruppe gefolgt von der [ **Remotedesktop** ](ms-settings:remotedesktop) Element.
3. Verwenden Sie den Schieberegler, um Remotedesktop zu aktivieren.
4. Es wird außerdem empfohlen, den PC zu halten, aktiv und sichtbar ist, um Verbindungen zu ermöglichen. Klicken Sie auf **Einstellungen anzeigen** zu aktivieren.
5. Bei Bedarf fügen Sie Benutzer, die durch Klicken auf eine Remoteverbindung herstellen können **wählen Benutzer, die Remotezugriff auf diesen PC können**.
   1. Mitglieder der Gruppe "Administratoren" haben automatisch Zugriff auf.
6. Notieren Sie sich den Namen des diesem PC unter **Herstellen einer Verbindung mit diesem PC**. Sie benötigen diese Option, um die Clients konfigurieren.

### <a name="windows-7-and-early-version-of-windows-10"></a>Windows 7 und frühe Version von Windows 10

Um Ihren PC für den Remotezugriff zu konfigurieren, herunterladen und Ausführen der [Microsoft Remote Desktop-Assistenten](https://www.microsoft.com/download/details.aspx?id=50042). Dieser Assistent aktualisiert die Systemeinstellungen, um den Remotezugriff zu aktivieren, wird sichergestellt, Ihren Computer für Verbindungen aktiv ist, und stellt sicher, dass die Firewall herstellen von Remotedesktopverbindungen zulässt. 

### <a name="all-versions-of-windows-legacy-method"></a>Alle Versionen von Windows (Legacy-Methode)

Befolgen Sie die Anweisungen, um mit den Eigenschaften des älteren Systems Remotedesktop zu aktivieren, [Herstellen einer Verbindung mit einem anderen Computer mithilfe der Remotedesktopverbindung](https://windows.microsoft.com/windows/remote-desktop-connection-faq).

## <a name="should-i-enable-remote-desktop"></a>Sollte ich Remotedesktop aktivieren?

Wenn Sie nur Ihren PC zugreifen, wenn Sie physisch davor ungenutzte möchten, müssen Sie keine Remotedesktop zu aktivieren. Aktivieren von Remotedesktop öffnet einen Port auf Ihrem PC, der an das lokale Netzwerk sichtbar ist. Sie sollten nur Remote Desktop in vertrauenswürdigen Netzwerken wie z. B. Ihre Startseite aktivieren. Sie möchten auch nach dem Aktivieren von Remotedesktop auf einem beliebigen PC, in denen Zugriff auf eng gesteuert wird.

Denken Sie daran, dass wenn Sie den Zugriff auf Remotedesktop, aktivieren Sie alle Benutzer in der Gruppe "Administratoren" gewähren sowie alle weiteren Benutzer Sie auswählen, die Möglichkeit, die Remotezugriff auf ihre Konten auf dem Computer.

Sie sollten sicherstellen, dass jedes Konto mit Zugriff auf Ihren PC mit einem sicheren Kennwort konfiguriert ist.

## <a name="why-allow-connections-only-with-network-level-authentication"></a>Warum zulassen, dass nur Verbindungen mit Authentifizierung auf Netzwerkebene? 

Sie können zum Einschränken des Zugriffs auf Ihren PC wählen Sie aus, den Zugriff nur mit den Network Level Authentication (NLA). Wenn Sie diese Option aktivieren, müssen Benutzer authentifizieren sich mit dem Netzwerk, bevor sie eine Verbindung mit Ihrem PC herstellen können. Zulassen von Verbindungen nur von Computern, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebene ausgeführt wird, ist eine sicherere Methode zur Authentifizierung, die helfen können, Ihren Computer vor böswilligen Benutzern und Software zu schützen. Weitere Informationen zu NLA und Remotedesktop, sehen Sie sich [NLA-Feature konfigurieren, für die RDS-Verbindungen](https://technet.microsoft.com/library/cc732713(v=ws.11).aspx).

Wenn Sie Remote auf einem PC in Ihrem privaten Netzwerk von außerhalb von diesem Netzwerk eine Verbindung herstellen, sollten wählen Sie diese Option nicht aus.
