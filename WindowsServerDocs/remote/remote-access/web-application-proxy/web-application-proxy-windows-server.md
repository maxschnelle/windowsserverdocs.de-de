---
ms.assetid: d8adcb68-18e0-41bf-a817-d57344bf2e7d
title: Webanwendungsproxy in Windows Server 2016
description: ''
author: kgremban
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: c4e4eb73b7d50c7618ad2c998ee484e660bcfef1
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446763"
---
# <a name="web-application-proxy-in-windows-server-2016"></a>Webanwendungsproxy in Windows Server 2016

>Gilt für: Windows Server 2016

**Dieser Inhalt ist für die lokale Version des Webanwendungsproxys relevant. Zum Aktivieren des sicheren Zugriffs auf lokale Anwendungen über die Cloud finden Sie unter den [Azure AD-Anwendungsproxy-Inhalt](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/).**  
  
In diesem Abschnitt Informationen zu Neuheiten und Änderungen in der Web Application Proxy für Windows Server 2016. Die neuen Features und die hier aufgeführten Änderungen sind wahrscheinlich am stärksten auswirken, wie Sie die Preview-Version arbeiten.  
  
## <a name="web-application-proxy-new-features-in-windows-server-2016"></a>Web Application Proxy, neuen Features in Windows Server 2016
  
- Vorauthentifizierung für die Veröffentlichung von HTTP-Standardauthentifizierung  
  
  HTTP-Standardauthentifizierung ist die Authorization-Protokoll von viele Protokolle, einschließlich von ActiveSync zum Verbinden von rich-Clients, einschließlich Smartphones mit Ihrem Exchange-Postfach verwendet. Webanwendungsproxy interagiert traditionell mit AD FS mithilfe von umleitungen von ActiveSync-Clients nicht unterstützt wird. Diese neue Version des Webanwendungsproxys bietet Unterstützung zum Veröffentlichen einer app mithilfe von HTTP basic durch Aktivieren der HTTP-app zum Empfangen von einer nicht anspruchsbasierten Vertrauensstellung der vertrauenden für die Anwendung für den Verbunddienst.  
  
  Weitere Informationen zu grundlegenden HTTP-Veröffentlichung, finden Sie unter [Veröffentlichen von Anwendungen mit AD FS-Vorauthentifizierung](Publishing-Applications-using-AD-FS-Preauthentication.md#publish-an-application-that-uses-http-basic)  
  
- Veröffentlichen von Domänen mit Platzhalter von Anwendungen  
  
  Um Szenarien wie z. B. SharePoint 2013 zu unterstützen, zählen die externe URL für die Anwendung nun einen Platzhalter, damit Sie mehrere Anwendungen in einer bestimmten Domäne, z. B. https://*.sp-apps.contoso.com veröffentlichen können. Dadurch wird die Veröffentlichung von SharePoint-Anwendungen vereinfacht.  
  
- HTTP, HTTPS-Umleitung  
  
  Um sicherzustellen, dass Sie, dass Ihre Benutzer Ihre app zugreifen können, selbst wenn sie nicht in der URL HTTPS eingeben, unterstützt Web Application Proxy nun HTTP, HTTPS-Umleitung.  
  
- HTTP-Veröffentlichung  
  
  Es ist jetzt möglich, die HTTP-Anwendungen mit Passthrough-Vorauthentifizierung veröffentlichen.  
  
- Veröffentlichen von Remotedesktopgateway-apps  
  
  Weitere Informationen zu RDG in Web Application Proxy, finden Sie unter [Veröffentlichen von Anwendungen mit SharePoint, Exchange und RDG](../web-application-proxy/Publishing-Applications-with-SharePoint,-Exchange-and-RDG.md)  
  
- Neue Debugprotokoll für die Problembehandlung und das höhere Servicelevel-Protokoll für vollständige Audit-Trail und verbesserter Fehlerbehandlung  
  
  Weitere Informationen zur Problembehandlung finden Sie unter [zur Problembehandlung von Web Application Proxy](https://technet.microsoft.com/library/dn770156.aspx)  
  
- Verbesserungen der Administrator-Konsole-Benutzeroberfläche  
  
- Weitergabe von IP-Adresse des Clients auf Back-End-Anwendungen  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Neuerungen in Windows Server 2016](https://technet.microsoft.com/library/dn765472.aspx)  
  
-   [Veröffentlichen von Anwendungen mit AD FS-Vorauthentifizierung](../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)  
  
-   [Problembehandlung: Webanwendungsproxy](https://technet.microsoft.com/library/dn770156.aspx)  
  


