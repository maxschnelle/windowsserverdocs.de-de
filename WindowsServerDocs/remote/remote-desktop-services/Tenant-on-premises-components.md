---
title: Lokale Komponenten von Mandanten
description: Dieser Artikel beschreibt die lokalen Komponenten deiner RDS-Bereitstellung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3eebb38-a835-4fa6-9e41-1966014bf2cb
author: lizap
manager: dongill
ms.openlocfilehash: 191d2247af5d5f63a203415af13f8d3370b3c6f6
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546477"
---
# <a name="tenant-on-premises-components"></a>Lokale Komponenten von Mandanten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Die folgenden Informationen beschreiben die lokalen Komponenten, aus denen die Desktophostingbereitstellung besteht.  
  
##  <a name="clients"></a>Clients  
Für den Zugriff auf die gehosteten Desktops und Anwendungen müssen Benutzer Remotedesktopclients verwenden, die das Remotedesktopprotokoll (RDP) 7.1 oder höher unterstützen. Insbesondere muss der Client das Remotedesktopgateway und den Remotedesktop-Verbindungsbroker unterstützen. Um Anwendungen für den lokalen Desktop bereitstellen zu können, muss der Client auch das RemoteApp-Feature unterstützen. Um eine hohe Gatewayverfügbarkeit zu erzielen, muss der Client reine HTTP-Übertragungsverbindungen mit dem Remotedesktopgateway unterstützen.  
  
Weitere Informationen:  
[RemoteFX Enabled Devices](https://social.technet.microsoft.com/wiki/contents/articles/14534.remotefx-enabled-devices.aspx) (RemoteFX-fähige Geräte)  
[What's new in Windows Server 2012 R2 Remote Desktop Gateway](https://blogs.technet.microsoft.com/enterprisemobility/2013/03/14/whats-new-in-windows-server-2012-remote-desktop-gateway/#transport) (Neues beim Windows Server 2012 R2-Remotedesktopgateway)  
[Microsoft-Remotedesktopclients](https://technet.microsoft.com/library/dn473009.aspx)  
[Remotedesktop-App für Windows im Microsoft Store](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)  
[Microsoft-Remotedesktop – Android-Apps in Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)  
[Mac App Store – Microsoft-Remotedesktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417?mt=12)  
[Microsoft-Remotedesktop im App Store](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8)  
  
##  <a name="active-directory-domain-services"></a>Active Directory Domain Services  
Einige größere und komplexere Mandanten entscheiden sich möglicherweise dafür, einen AD DS-Server (Active Directory Domain Services) lokal zu hosten. In diesem Fall ist der AD DS-Server in der Umgebung des Mandanten in der Regel ein Replikat eines lokalen AD DS-Servers des Mandanten. Dies wird unterstützt, indem ein virtuelles Netzwerk in der Umgebung des Mandanten erstellt wird. Dann wird über das Azure-VPN eine Site-to-Site-Verbindung zwischen dem lokalen Mandantennetzwerk zum virtuellen Mandantennetzwerk im Azure-Rechenzentrum erstellt.  
  
Weitere Informationen:  
[Übersicht über das Microsoft Azure Virtual Network](https://azure.microsoft.com/documentation/articles/virtual-networks-overview/)  
[Erstellen einer Site-to-Site-Verbindung im Azure-Portal](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  


