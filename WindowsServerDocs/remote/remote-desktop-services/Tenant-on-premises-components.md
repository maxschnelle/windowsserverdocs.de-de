---
title: Lokale Komponenten von Mandanten
description: Dieser Artikel beschreibt die lokalen Komponenten deiner RDS-Bereitstellung.
ms.author: elizapo
ms.date: 08/01/2016
ms.topic: article
ms.assetid: b3eebb38-a835-4fa6-9e41-1966014bf2cb
author: lizap
manager: dongill
ms.openlocfilehash: e2a06368bea88a9b746242da5a0281b465804c62
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958118"
---
# <a name="tenant-on-premises-components"></a>Lokale Komponenten von Mandanten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Die folgenden Informationen beschreiben die lokalen Komponenten, aus denen die Desktophostingbereitstellung besteht.

##  <a name="clients"></a>Clients
Für den Zugriff auf die gehosteten Desktops und Anwendungen müssen Benutzer Remotedesktopclients verwenden, die das Remotedesktopprotokoll (RDP) 7.1 oder höher unterstützen. Insbesondere muss der Client das Remotedesktopgateway und den Remotedesktop-Verbindungsbroker unterstützen. Um Anwendungen für den lokalen Desktop bereitstellen zu können, muss der Client auch das RemoteApp-Feature unterstützen. Um eine hohe Gatewayverfügbarkeit zu erzielen, muss der Client reine HTTP-Übertragungsverbindungen mit dem Remotedesktopgateway unterstützen.

Weitere Informationen: [Neuerungen im Remotedesktopgateway für Windows Server 2012 R2](https://techcommunity.microsoft.com/t5/microsoft-security-and/what-8217-s-new-in-windows-server-2012-remote-desktop-gateway/ba-p/247611)
[Microsoft-Remotedesktopclients](./clients/remote-desktop-clients.md)
[Remotedesktop-App für Windows im Microsoft Store](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)
[Microsoft-Remotedesktop: Android-Apps bei Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)
[Mac App Store: Microsoft-Remotedesktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417?mt=12)
[Microsoft-Remotedesktop im App Store](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8)

##  <a name="active-directory-domain-services"></a>Active Directory-Domänendienste (AD DS)
Einige größere und komplexere Mandanten entscheiden sich möglicherweise dafür, einen AD DS-Server (Active Directory Domain Services) lokal zu hosten. In diesem Fall ist der AD DS-Server in der Umgebung des Mandanten in der Regel ein Replikat eines lokalen AD DS-Servers des Mandanten. Dies wird unterstützt, indem ein virtuelles Netzwerk in der Umgebung des Mandanten erstellt wird. Dann wird über das Azure-VPN eine Site-to-Site-Verbindung zwischen dem lokalen Mandantennetzwerk zum virtuellen Mandantennetzwerk im Azure-Rechenzentrum erstellt.

Weitere Informationen: [Überblick über Microsoft Azure Virtual Network](/azure/virtual-network/virtual-networks-overview)
[Erstellen einer Site-to-Site-Verbindung im Azure-Portal](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
