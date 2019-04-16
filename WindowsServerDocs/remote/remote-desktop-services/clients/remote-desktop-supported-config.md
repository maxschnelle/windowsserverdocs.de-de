---
title: Remote Desktop Client - unterstützte Konfiguration
description: Hier erfahren Sie, welche PCs Sie über Remotedesktop-Clients zugreifen können
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
ms.sourcegitcommit: 96e968bbe8dc50ebb1535ae1c8ce92fa73c83171
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2018
ms.locfileid: "1978047"
---
# <a name="remote-desktop-client---supported-configuration"></a>Remote Desktop Client - unterstützte Konfiguration

## <a name="supported-pcs"></a>Unterstützte PCs
Sie können mit PCs verbinden, die den folgenden Windows-Betriebssystemen ausgeführt werden:
- Windows10 Pro
- Windows 10 Enterprise
- Windows 8 Enterprise
- Windows 8 Professional
- Windows 7 Professional
- Windows 7 Enterprise
- Windows 7 Ultimate
- Windows 7 Ultimate
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Multipoint Server 2011
- Windows Multipoint Server 2012
- Windows Small Business Server 2008
- Windows Small Business Server2011

Das Gateway Remote Desktop können die folgenden Computern ausgeführt werden:

- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Small Business Server2011

Die folgenden Betriebssysteme können als RD-Webzugriff oder RemoteApp-Server verwendet werden:
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

## <a name="unsupported-windows-versions-and-editions"></a>Nicht unterstützte Windows-Versionen und Editionen

Remotedesktop-Clients wird nicht auf diese Windows-Versionen und Editionen verbunden:

- Windows7 Starter
- Windows 7-Startseite
- Windows 8-Startseite
- Windows 8.1-Startseite
- Windows10 Home

Wenn Sie möchten Computer zugreifen, die eine der folgenden Windows-Versionen installiert haben, wird empfohlen, dass Sie auf einem Windows-Version aktualisieren, RDP unterstützt.

## <a name="rd-gateway-messaging-is-not-supported"></a>RD-Gateway messaging wird nicht unterstützt.
Remotedesktopverbindungs-Client unterstützt keine messaging RD-Gateway. Stellen Sie sicher, dass die Remote Desktop Access Ressourcenrichtlinie (RD-RAS-Richtlinien) für Ihren Server RD-Gateway gibt keinen **Computer mit Unterstützung für RD-Gateway Messaging nur erlauben** , oder Sie nicht möglich ist, eine Verbindung herzustellen.