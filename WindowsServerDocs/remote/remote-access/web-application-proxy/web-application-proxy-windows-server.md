---
ms.assetid: d8adcb68-18e0-41bf-a817-d57344bf2e7d
title: Webanwendungsproxy in Windows Server 2016
ms.author: kgremban
author: eross-msft
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server
ms.technology: web-app-proxy
ms.openlocfilehash: 660915a9fc704a01b59b4eeb1107ef56599ecac7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818573"
---
# <a name="web-application-proxy-in-windows-server-2016"></a>Webanwendungsproxy in Windows Server 2016

>Gilt für: Windows Server 2016

**Diese Inhalte sind für die lokale Version des webanwendungsproxys relevant. Informationen zum Aktivieren des sicheren Zugriffs auf lokale Anwendungen über die Cloud finden Sie in den [Azure AD Anwendungs Proxy-Inhalt](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/).**  
  
In diesem Abschnitt werden die Neuerungen und Änderungen im webanwendungsproxy für Windows Server 2016 beschrieben. Die hier aufgeführten neuen Features und Änderungen haben bei der Arbeit mit der Vorschau wahrscheinlich die größten Auswirkungen.  
  
## <a name="web-application-proxy-new-features-in-windows-server-2016"></a>Neue Features des webanwendungsproxys in Windows Server 2016
  
- Vorauthentifizierung für http-Basis Anwendungs Veröffentlichung  
  
  HTTP Basic ist das Autorisierungs Protokoll, das von vielen Protokollen verwendet wird, einschließlich ActiveSync, um Rich-Clients, einschließlich Smartphones, mit Ihrem Exchange-Postfach zu verbinden. Der webanwendungsproxy interagiert traditionell mit AD FS mithilfe von Umleitungen, die auf ActiveSync-Clients nicht unterstützt werden. Diese neue Version des webanwendungsproxys unterstützt das Veröffentlichen einer App mithilfe von HTTP Basic, indem es der http-App ermöglicht, eine nicht anspruchsvolle Vertrauensstellung der vertrauenden Seite für die Anwendung für die Verbunddienst zu empfangen.  
  
  Weitere Informationen zur HTTP-Basis Veröffentlichung finden [Sie unter Veröffentlichen von Anwendungen mit AD FS Vorauthentifizierung](Publishing-Applications-using-AD-FS-Preauthentication.md#publish-an-application-that-uses-http-basic) .  
  
- Platzhalter Domänen Veröffentlichung von Anwendungen  
  
  Zur Unterstützung von Szenarien wie SharePoint 2013 kann die externe URL für die Anwendung nun einen Platzhalter enthalten, mit dem Sie mehrere Anwendungen in einer bestimmten Domäne veröffentlichen können, z. b. https://*. SP-apps. Configuration. com. Dadurch wird die Veröffentlichung von SharePoint-apps vereinfacht.  
  
- Umleitung von http zu https  
  
  Um sicherzustellen, dass Ihre Benutzer auf Ihre App zugreifen können, unterstützt der webanwendungsproxy nun die Umleitung von http zu HTTPS, auch wenn Sie den Typ "https" in der URL vernachlässigen.  
  
- HTTP-Veröffentlichung  
  
  Es ist jetzt möglich, HTTP-Anwendungen mit Passthrough-Vorauthentifizierung zu veröffentlichen.  
  
- Veröffentlichen von Remotedesktop Gateway-apps  
  
  Weitere Informationen zu RDG im webanwendungsproxy finden Sie unter [Veröffentlichen von Anwendungen mit SharePoint, Exchange und RDG](../web-application-proxy/Publishing-Applications-with-SharePoint,-Exchange-and-RDG.md) .  
  
- Neues Debugprotokoll zur besseren Problembehandlung und zum verbesserten Dienst Protokoll für einen kompletten Überwachungs Pfad und eine verbesserte Fehlerbehandlung  
  
  Weitere Informationen zur Problembehandlung finden Sie unter Problembehandlung für [Webanwendungs Proxy](https://technet.microsoft.com/library/dn770156.aspx)  
  
- Verbesserungen der Administratorkonsole  
  
- Weitergabe von Client-IP-Adressen an Back-End  
  
## <a name="see-also"></a>Weitere Informationen  
  
-   [Neuerungen in Windows Server 2016](https://technet.microsoft.com/library/dn765472.aspx)  
  
-   [Veröffentlichen von Anwendungen mit AD FS-Vorauthentifizierung](../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)  
  
-   [Problembehandlung: Webanwendungsproxy](https://technet.microsoft.com/library/dn770156.aspx)  
  


