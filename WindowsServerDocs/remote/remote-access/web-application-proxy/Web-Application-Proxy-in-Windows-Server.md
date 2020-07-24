---
ms.assetid: 0b3587b2-219f-43d8-88b4-1254eaa8b910
title: Webanwendungsproxy in Windows Server
ms.prod: windows-server
ms.technology: web-app-proxy
ms.topic: article
ms.author: kgremban
author: eross-msft
ms.openlocfilehash: 84c2c735ee3e6b19816acaa8810c297c487f5250
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961452"
---
# <a name="web-application-proxy-in-windows-server"></a>Webanwendungsproxy in Windows Server

>Gilt für: Windows Server&reg; 2016

**Diese Inhalte sind für die lokale Version des webanwendungsproxys relevant. Informationen zum Aktivieren des sicheren Zugriffs auf lokale Anwendungen über die Cloud finden Sie in den [Azure AD Anwendungs Proxy-Inhalt](/azure/active-directory/manage-apps/application-proxy).**  
  
In diesem Abschnitt werden die Neuerungen und Änderungen im webanwendungsproxy für Windows Server 2016 beschrieben. Die hier aufgeführten neuen Features und Änderungen haben bei der Arbeit mit der Vorschau wahrscheinlich die größten Auswirkungen.  
  
## <a name="web-application-proxy-new-features"></a>Neue Features für Webanwendungs Proxy  
  
- Vorauthentifizierung für http-Basis Anwendungs Veröffentlichung  
  
  HTTP Basic ist das Autorisierungs Protokoll, das von vielen Protokollen verwendet wird, einschließlich ActiveSync, um Rich-Clients, einschließlich Smartphones, mit Ihrem Exchange-Postfach zu verbinden. Der webanwendungsproxy interagiert traditionell mit AD FS mithilfe von Umleitungen, die auf ActiveSync-Clients nicht unterstützt werden. Diese neue Version des webanwendungsproxys unterstützt das Veröffentlichen einer App mithilfe von HTTP Basic, indem es der http-App ermöglicht, eine nicht anspruchsvolle Vertrauensstellung der vertrauenden Seite für die Anwendung für die Verbunddienst zu empfangen.  
  
  Weitere Informationen zur HTTP-Basis Veröffentlichung finden [Sie unter Veröffentlichen von Anwendungen mit AD FS Vorauthentifizierung](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md) .  
  
- Platzhalter Domänen Veröffentlichung von Anwendungen  
  
  Zur Unterstützung von Szenarien wie SharePoint 2013 kann die externe URL für die Anwendung nun einen Platzhalter enthalten, mit dem Sie mehrere Anwendungen in einer bestimmten Domäne veröffentlichen können, z. b. https://*. SP-apps. Configuration. com. Dadurch wird die Veröffentlichung von SharePoint-apps vereinfacht.  
  
- HTTP-HTTPS-Umleitung  
  
  Um sicherzustellen, dass Ihre Benutzer auf Ihre App zugreifen können, unterstützt der webanwendungsproxy nun die Umleitung von http zu HTTPS, auch wenn Sie den Typ "https" in der URL vernachlässigen.  
  
- HTTP-Veröffentlichung  
  
  Es ist jetzt möglich, HTTP-Anwendungen mit Passthrough-Vorauthentifizierung zu veröffentlichen.  
  
- Veröffentlichen von Remotedesktop Gateway-apps  
  
  Weitere Informationen zu RDG im webanwendungsproxy finden Sie unter [Veröffentlichen von Anwendungen mit SharePoint, Exchange und RDG](../web-application-proxy/Publishing-Applications-with-SharePoint,-Exchange-and-RDG.md) .  
  
- Neues Debugprotokoll zur besseren Problembehandlung und zum verbesserten Dienst Protokoll für einen kompletten Überwachungs Pfad und eine verbesserte Fehlerbehandlung  
  
  Weitere Informationen zur Problembehandlung finden Sie unter Problembehandlung für [Webanwendungs Proxy](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))  
  
- Verbesserungen der Administratorkonsole  
  
- Weitergabe von Client-IP-Adressen an Back-End  
  
## <a name="see-also"></a>Weitere Informationen  
  
-   [Neuerungen in Windows Server 2016](../../../get-started/whats-new-in-windows-server-2016.md)  
  
-   [Veröffentlichen von Anwendungen mit AD FS-Vorauthentifizierung](../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)  
  
-   [Problembehandlung: Webanwendungsproxy](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))  
  
