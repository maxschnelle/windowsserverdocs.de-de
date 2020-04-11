---
title: 'Remotedesktopclient: unterstützte Konfiguration'
description: Hier erfährst du, auf welche PCs du mithilfe von Remotedesktopclients zugreifen kannst.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: bb932dad-6f74-484f-8f7b-dd957b615d44
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1480a2a14a1c3fc23c4e5122e366741d37d9091f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856013"
---
# <a name="remote-desktop-client---supported-configuration"></a>Remotedesktopclient: unterstützte Konfiguration

## <a name="supported-pcs"></a>Unterstützte PCs
Du kannst eine Verbindung mit PCs unter den folgenden Windows-Betriebssystemen herstellen:
- Windows 10 Pro
- Windows 10 Enterprise
- Windows 8 Enterprise
- Windows 8 Professional
- Windows 7 Professional
- Windows 7 Enterprise
- Windows 7 Ultimate
- Windows 7 Ultimate
- WindowsServer 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows MultiPoint Server 2011
- Windows MultiPoint Server 2012
- Windows Small Business Server 2008
- Windows Small Business Server 2011

Auf den folgenden Computern kann das Remotedesktopgateway ausgeführt werden:

- WindowsServer 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Small Business Server 2011

Die folgenden Betriebssysteme können als Server mit Web Access für Remotedesktop oder als RemoteApp-Server fungieren:
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

## <a name="unsupported-windows-versions-and-editions"></a>Nicht unterstützte Windows-Versionen und -Editionen

Der Remotedesktopclient stellt keine Verbindung mit den folgenden Windows-Versionen und -Editionen her:

- Windows 7 Starter
- Windows 7 Home
- Windows 8 Home
- Windows 8.1 Home
- Windows 10 Home

Falls du auf Computer mit einer dieser Windows-Versionen zugreifen möchtest, wird ein Upgrade auf eine Windows-Version empfohlen, die RDP unterstützt.

## <a name="rd-gateway-messaging-is-not-supported"></a>RD-Gateway-Messaging wird nicht unterstützt.
Remotedesktopclient unterstützt das RD-Gateway-Messaging nicht. Vergewissere dich, dass in der Remotedesktop-Ressourcenzugriffsrichtlinie (Remote Desktop Resource Access Policy, RD RAP) für deinen RD-Gateway-Server nicht **Only allow computers with support for RD Gateway Messaging** (Nur Computer mit Unterstützung für RD-Gateway-Messaging zulassen) angegeben ist. Andernfalls kannst du keine Verbindung herstellen.