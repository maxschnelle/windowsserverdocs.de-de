---
ms.assetid: 0b3587b2-219f-43d8-88b4-1254eaa8b910
title: Web Application Proxy in Windows Server
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: ''
ms.suite: na
ms.technology: web-app-proxy
ms.tgt_pltfrm: na
ms.topic: article
author: kgremban
ms.openlocfilehash: 056e833a2c030b2fdb96b00e7e55996656e2fec2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886041"
---
# <a name="web-application-proxy-in-windows-server"></a>Web Application Proxy in Windows Server

>Gilt für: Windows Server&reg; 2016

**Dieser Inhalt ist für die lokale Version des Webanwendungsproxys relevant. Zum Aktivieren des sicheren Zugriffs auf lokale Anwendungen über die Cloud finden Sie unter den [Azure AD-Anwendungsproxy-Inhalt](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/).**  
  
In diesem Abschnitt Informationen zu Neuheiten und Änderungen in der Web Application Proxy für Windows Server 2016. Die neuen Features und die hier aufgeführten Änderungen sind wahrscheinlich am stärksten auswirken, wie Sie die Preview-Version arbeiten.  
  
## <a name="web-application-proxy-new-features"></a>Web Application Proxy neue Features  
  
-   Vorauthentifizierung für die Veröffentlichung von HTTP-Standardauthentifizierung  
  
    HTTP-Standardauthentifizierung ist die Authorization-Protokoll von viele Protokolle, einschließlich von ActiveSync zum Verbinden von rich-Clients, einschließlich Smartphones mit Ihrem Exchange-Postfach verwendet. Webanwendungsproxy interagiert traditionell mit AD FS mithilfe von umleitungen von ActiveSync-Clients nicht unterstützt wird. Diese neue Version des Webanwendungsproxys bietet Unterstützung zum Veröffentlichen einer app mithilfe von HTTP basic durch Aktivieren der HTTP-app zum Empfangen von einer nicht anspruchsbasierten Vertrauensstellung der vertrauenden für die Anwendung für den Verbunddienst.  
  
    Weitere Informationen zu grundlegenden HTTP-Veröffentlichung, finden Sie unter [Veröffentlichen von Anwendungen mit AD FS-Vorauthentifizierung](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)  
  
-   Veröffentlichen von Domänen mit Platzhalter von Anwendungen  
  
    Um Szenarien wie z. B. SharePoint 2013 zu unterstützen, zählen die externe URL für die Anwendung nun einen Platzhalter, damit Sie mehrere Anwendungen in einer bestimmten Domäne, z. B. https://*.sp-apps.contoso.com veröffentlichen können. Dadurch wird die Veröffentlichung von SharePoint-Anwendungen vereinfacht.  
  
-   HTTP, HTTPS-Umleitung  
  
    Um sicherzustellen, dass Sie, dass Ihre Benutzer Ihre app zugreifen können, selbst wenn sie nicht in der URL HTTPS eingeben, unterstützt Web Application Proxy nun HTTP, HTTPS-Umleitung.  
  
-   HTTP-Veröffentlichung  
  
    Es ist jetzt möglich, die HTTP-Anwendungen mit Passthrough-Vorauthentifizierung veröffentlichen.  
  
-   Veröffentlichen von Remotedesktopgateway-apps  
  
    Weitere Informationen zu RDG in Web Application Proxy, finden Sie unter [Veröffentlichen von Anwendungen mit SharePoint, Exchange und RDG](../web-application-proxy/Publishing-Applications-with-SharePoint,-Exchange-and-RDG.md)  
  
-   Neue Debugprotokoll für die Problembehandlung und das höhere Servicelevel-Protokoll für vollständige Audit-Trail und verbesserter Fehlerbehandlung  
  
    Weitere Informationen zur Problembehandlung finden Sie unter [zur Problembehandlung von Web Application Proxy](https://technet.microsoft.com/library/dn770156.aspx)  
  
-   Verbesserungen der Administrator-Konsole-Benutzeroberfläche  
  
-   Weitergabe von IP-Adresse des Clients auf Back-End-Anwendungen  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Was ist neu in WindowsServer 2016](https://technet.microsoft.com/library/dn765472.aspx)  
  
-   [Veröffentlichen von Anwendungen mit AD FS-Vorauthentifizierung](../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)  
  
-   [Problembehandlung des Webanwendungsproxys](https://technet.microsoft.com/library/dn770156.aspx)  
  


