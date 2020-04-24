---
title: Lokale Komponenten von Mandanten
description: Dieser Artikel beschreibt die lokalen Komponenten deiner RDS-Bereitstellung.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.topic: article
ms.assetid: b3eebb38-a835-4fa6-9e41-1966014bf2cb
author: lizap
manager: dongill
ms.openlocfilehash: 849b0e3eb751c4e45a7c23da4230c7c4eb6bfcb1
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80854703"
---
# <a name="tenant-on-premises-components"></a>Lokale Komponenten von Mandanten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Die folgenden Informationen beschreiben die lokalen Komponenten, aus denen die Desktophostingbereitstellung besteht.  
  
##  <a name="clients"></a>Clients  
Für den Zugriff auf die gehosteten Desktops und Anwendungen müssen Benutzer Remotedesktopclients verwenden, die das Remotedesktopprotokoll (RDP) 7.1 oder höher unterstützen. Insbesondere muss der Client das Remotedesktopgateway und den Remotedesktop-Verbindungsbroker unterstützen. Um Anwendungen für den lokalen Desktop bereitstellen zu können, muss der Client auch das RemoteApp-Feature unterstützen. Um eine hohe Gatewayverfügbarkeit zu erzielen, muss der Client reine HTTP-Übertragungsverbindungen mit dem Remotedesktopgateway unterstützen.  
  
Weitere Informationen:  
[What's new in Windows Server 2012 R2 Remote Desktop Gateway](https://blogs.technet.microsoft.com/enterprisemobility/2013/03/14/whats-new-in-windows-server-2012-remote-desktop-gateway/#transport) (Neues beim Windows Server 2012 R2-Remotedesktopgateway)  
[Microsoft-Remotedesktopclients](https://technet.microsoft.com/library/dn473009.aspx)  
[Remotedesktop-App für Windows im Microsoft Store](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)  
[Microsoft-Remotedesktop – Android-Apps in Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)  
[Mac App Store – Microsoft-Remotedesktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417?mt=12)  
[Microsoft-Remotedesktop im App Store](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8)  
  
##  <a name="active-directory-domain-services"></a>Active Directory-Domänendienste (AD DS)  
Einige größere und komplexere Mandanten entscheiden sich möglicherweise dafür, einen AD DS-Server (Active Directory Domain Services) lokal zu hosten. In diesem Fall ist der AD DS-Server in der Umgebung des Mandanten in der Regel ein Replikat eines lokalen AD DS-Servers des Mandanten. Dies wird unterstützt, indem ein virtuelles Netzwerk in der Umgebung des Mandanten erstellt wird. Dann wird über das Azure-VPN eine Site-to-Site-Verbindung zwischen dem lokalen Mandantennetzwerk zum virtuellen Mandantennetzwerk im Azure-Rechenzentrum erstellt.  
  
Weitere Informationen:  
[Übersicht über das Microsoft Azure Virtual Network](https://azure.microsoft.com/documentation/articles/virtual-networks-overview/)  
[Erstellen einer Site-to-Site-Verbindung im Azure-Portal](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  


