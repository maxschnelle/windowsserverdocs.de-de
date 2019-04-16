---
title: Remotedesktop - ermöglichen den Zugriff auf Ihrem PC
description: Erfahren Sie mehr über Ihre Optionen für den Remotezugriff auf Ihrem PC
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
ms.openlocfilehash: d3c85c1c765583eb26cef60ecd245708e0e02772
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297219"
---
# Remotedesktop - ermöglichen den Zugriff auf Ihrem PC

>Gilt für: Windows 10, Windows 8.1, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2

Sie können Remotedesktop herstellen und steuern Ihren PC vor einem Remotegerät mithilfe eines [Microsoft-Remotedesktopclient](remote-desktop-clients.md) (für Windows, iOS, MacOS und Android verfügbar). Wenn Sie Remoteverbindungen mit Ihrem PC zulassen, können Sie ein anderes Gerät mit Ihrem PC herstellen und haben Zugriff auf alle Ihre apps, Dateien und Netzwerkressourcen, als säßen Sie direkt an Ihrem Schreibtisch.  

> [!NOTE]
> Sie können Remotedesktop Verbindung mit Windows 10 Pro und Enteprise, Windows 8.1 und 8 Enterprise und Pro, Windows 7 Professional, Enterprise und Ultimate und Windows Server-Versionen als Windows Server 2008 neuere verwenden. Sie können nicht für Computer unter der Home-Edition (z. B. Windows 10 Home) verbinden. 

Um mit einem remote-PC, verbinden, dass Computer muss aktiviert sein, müssen sie eine Netzwerkverbindung, Remotedesktop muss aktiviert sein, müssen Sie Zugriff auf das Netzwerk mit dem Remotecomputer (Dies kann über das Internet sein), und Sie benötigen die Berechtigung, eine Verbindung herzustellen. Für die Berechtigung, eine Verbindung herstellen müssen Sie in der Liste der Benutzer sein. Bevor Sie eine Verbindung beginnen, ist es sinnvoll, den Namen des Computers zu suchen, die Sie eine Verbindung herstellen, und stellen Sie sicher, dass Remotedesktopverbindungen durch die Firewall zulässig sind.

## So aktivieren Sie Remotedesktop

Die einfachste Möglichkeit, den Zugriff auf Ihren PC von einem Remotegerät zulassen, wird der Remotedesktop-Optionen unter Einstellungen verwendet. Da diese Funktionalität in Windows 10 Fall Creators Update (1709), eine Separate herunterladbare hinzugefügt wurde, dass die app auch verfügbar ist bereitstellt, eine ähnliche Funktionalität für frühere Versionen von Windows. Sie können auch die ältere Methode zum Aktivieren von Remotedesktop verwenden, jedoch diese Methode weniger Funktionen und Validierung bereitstellt.

### Windows 10 Fall creators Update (1709) oder höher

Sie können Ihren PC für den Remotezugriff mit einigen einfachen Schritten konfigurieren.
1. Sie möchten eine Verbindung herstellen möchten, markieren Sie **Starten** und dann auf das Symbol " **Einstellungen** " auf der linken Seite, auf dem Gerät.
2. Wählen Sie die **System** -Gruppe, gefolgt von den [**Remotedesktop**](ms-settings:remotedesktop) -Element.
3. Verwenden Sie den Schieberegler, um Remote Desktop zu aktivieren.
4. Es wird auch empfohlen, um den PC länger aktiviert und für Verbindungen zu erleichtern sichtbar zu schützen. Klicken Sie auf **Einstellungen anzeigen** , um zu aktivieren.
5. Wenn notwendig, fügen Sie Benutzer, die eine Remoteverbindung herstellen können, indem Sie **wählen, die diesen PC Remotezugriff können, Benutzer**auf.
   1. Mitglieder der Gruppe der Administratoren haben automatisch Zugriff.
6. Notieren Sie den Namen eines dieser PC unter **diesem PC Herstellen einer Verbindung**. Sie benötigen diese Option, um die Clients konfiguriert werden.

### Windows 7 und frühe Version von Windows 10

Um Ihren PC für den Remotezugriff zu konfigurieren, herunterladen Sie, und führen Sie den- [Microsoft Remote Desktop-Assistenten](https://www.microsoft.com/download/details.aspx?id=50042). Dieser Assistent aktualisiert die Systemeinstellungen, um zu aktivieren, wird sichergestellt, dass Ihre Computer länger für Verbindungen aktiviert, und überprüft, ob Ihre Firewall Remotedesktopverbindungen ermöglicht. 

### Alle Versionen von Windows (Legacy-Methode)

Um Remotedesktop mit älteren Systemeigenschaften zu aktivieren, führen Sie die Anweisungen zum [Verbinden mit einem anderen Computer, die mithilfe einer Remotedesktopverbindung](https://windows.microsoft.com/windows/remote-desktop-connection-faq).

## Sollte ich Remotedesktop aktivieren?

Wenn Sie Ihren PC zuzugreifen, wenn Sie physisch direkten sind nur verwenden möchten, müssen Sie Remotedesktop zu aktivieren. Aktivieren von Remotedesktop öffnet einen Port auf Ihrem PC, auf Ihrem lokalen Netzwerk sichtbar ist. Remotedesktop sollte nur in vertrauenswürdigen Netzwerken, z. B. Ihre Home aktiviert werden. Sie möchten nicht auch Remotedesktop auf jedem PC aktivieren, in denen der Zugriff eng gesteuert wird.

Beachten Sie, wenn Sie Zugriff auf Remotedesktop, aktivieren Sie Mitglied der Gruppe Administratoren erteilen sowie alle weiteren Benutzer auszuwählen, die Möglichkeit, ihre Konten auf dem Computer Remote zuzugreifen.

Sie sollten sicherstellen, dass jedes Konto mit Zugriff auf Ihren PC durch ein sicheres Kennwort konfiguriert ist.

## Warum erlauben Verbindungen nur mit Authentifizierung auf Netzwerkebene? 
 
Wenn Sie möchten einschränken, wer auf Ihrem PC zugreifen können, bieten Sie Zugriff nur mit Netzwerk Ebene Authentifizierung (Authentifizierung auf Netzwerkebene). Wenn Sie diese Option aktivieren, müssen Benutzer authentifizieren sich mit dem Netzwerk, bevor sie an Ihren PC anschließen können. Ermöglicht Verbindungen nur von Computern, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebene ausgeführt wird, ist eine sicherere Authentifizierungsmethode, die und Schutz Ihres Computers vor böswilligen Benutzern und Software. Weitere Informationen zu Authentifizierung auf Netzwerkebene und Remote Desktop, sehen Sie sich [Konfigurieren Authentifizierung auf Netzwerkebene für RDS-Verbindungen](https://technet.microsoft.com/library/cc732713(v=ws.11).aspx). 

Wenn Sie Remote auf einem PC im Heimnetzwerk von außerhalb dieses Netzwerk herstellen, wählen Sie diese Option nicht.
