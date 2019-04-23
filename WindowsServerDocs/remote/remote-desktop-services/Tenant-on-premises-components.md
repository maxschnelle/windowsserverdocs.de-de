---
title: Lokale Komponenten von Mandanten
description: Beschreibt die lokalen Komponenten in Ihre RDS-Bereitstellung.
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
ms.openlocfilehash: a01dbd12d76b1efa84e38f2ded38cfd613fb2ac4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857401"
---
# <a name="tenant-on-premises-components"></a>Lokale Komponenten von Mandanten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die folgenden Informationen beschreiben die lokalen Komponenten, aus denen die desktophostingbereitstellung.  
  
##  <a name="clients"></a>Clients  
Um die gehostete Desktops und Anwendungen zuzugreifen, müssen die Benutzer Remotedesktopclients verwenden, die Remote Desktop Protocol (RDP) 7.1 oder höher unterstützen. Insbesondere muss der Client Remotedesktopgateway und Remote Desktop Connection Broker unterstützen. Der Client muss auch die RemoteApp-Funktion unterstützen, zum Übermitteln von Anwendungen auf dem lokalen Desktop. Um hohe Verfügbarkeit für Gateways zu erreichen, muss der Client die reinen HTTP-Transport-Verbindungen mit RD-Gateway unterstützen.  
  
Weitere Informationen:  
[RemoteFX-fähige Geräte](https://social.technet.microsoft.com/wiki/contents/articles/14534.remotefx-enabled-devices.aspx)  
[Neuerungen in Windows Server 2012 R2 Remotedesktopgateway](https://blogs.technet.microsoft.com/enterprisemobility/2013/03/14/whats-new-in-windows-server-2012-remote-desktop-gateway/#transport)  
[Microsoft-Remotedesktopclients](https://technet.microsoft.com/library/dn473009.aspx)  
[Remotedesktop-app für Windows in Microsoft Store](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)  
[Microsoft Remote Desktop – Android-Apps in Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)  
[Mac App Store - Microsoft-Remotedesktopclient](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12)  
[Microsoft Remote Desktop in den App Store](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8)  
  
##  <a name="active-directory-domain-services"></a>Active Directory Domain Services  
Einige größeren und komplexeren Mandanten können auch einen Active Directory Domain Services (AD DS)-Server lokal hosten. In diesem Fall werden die AD DS-Server in der Mandanten-Umgebung ein Replikat der AD DS-Server in der Regel, die auf dem Firmengelände des Mandanten ist. Dies wird unterstützt, indem Sie ein virtuelles Netzwerk erstellen, in der Mandanten-Umgebung und mithilfe der Azure-VPN-um Standort-zu-Standort-Verbindung von des Mandanten im lokalen Netzwerk mit virtuellen Netzwerk des Mandanten, in das Azure-Rechenzentrum zu erstellen.  
  
Weitere Informationen:  
[Übersicht über die Microsoft Azure Virtual Network](https://azure.microsoft.com/documentation/articles/virtual-networks-overview/)  
[Erstellen Sie eine Resource Manager-VNet mit einer Standort-zu-Standort-VPN-Verbindung über das Azure-Portal](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  


