---
title: Remotedesktop-Client - Konfiguration unterstützt
description: Erfahren Sie, welche PCs, die Sie mithilfe von Remotedesktop-Clients zugreifen können
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb932dad-6f74-484f-8f7b-dd957b615d44
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d38008b6387385917ad21ce7e169b8ff3f4d18ba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884691"
---
# <a name="remote-desktop-client---supported-configuration"></a>Remotedesktop-Client - Konfiguration unterstützt

## <a name="supported-pcs"></a>Unterstützte PCs
Sie können auf PCs verbinden, die die folgenden Windows-Betriebssysteme ausgeführt werden:
- Windows 10 Pro
- Windows 10 Enterprise
- Windows 8 Enterprise
- Windows 8 Professional
- Windows 7 Professional
- Windows 7 Enterprise
- Windows 7 Ultimate
- Windows 7 Ultimate
- WindowsServer 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Multipoint Server 2011
- Windows Multipoint Server 2012
- Windows Small Business Server 2008
- Windows Small Business Server 2011

Die folgenden Computer können mit das Remotedesktop-Gateway ausführen:

- WindowsServer 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Small Business Server 2011

Web Access für Remotedesktop "oder" RemoteApp-Server dienen den folgenden Betriebssystemen unterstützt:
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

## <a name="unsupported-windows-versions-and-editions"></a>Nicht unterstützte Windows-Versionen und Editionen

Der Remotedesktop-Client verbindet sich nicht auf diese Windows-Versionen und Editionen:

- Windows 7 Starter
- Windows 7-Startseite
- Windows 8 Home
- Windows 8.1 Home
- Windows 10 Home

Wenn Sie möchten Computer zuzugreifen, die eine dieser Windows-Versionen installiert haben, empfehlen wir, dass Sie auf eine Windows-Version aktualisieren, die RDP unterstützt.

## <a name="rd-gateway-messaging-is-not-supported"></a>RD-Gateway-messaging wird nicht unterstützt.
Remote Desktop-Client wird das RD-Gateway messaging nicht unterstützt. Stellen Sie sicher, dass Remote Desktop Resource Access Policy (RD-RAP) für den RD-Gateway-Server nicht angegeben werden **nur auf Computern mit Unterstützung für das RD-Gateway-Messaging zulassen** oder Sie werden nicht in der eine Verbindung herstellen können.