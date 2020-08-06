---
ms.assetid: 222e9f93-7c41-4527-8a98-8f7fbc7a58af
title: Bereitstellen von Verbund Server Proxys in AD FS für Windows Server 2012 R2
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: eaf33a1f5398adc1237eaed5c8b418ccbebed9fe
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864168"
---
# <a name="deploying-federation-server-proxies"></a>Bereitstellen von Verbundserverproxys

In Active Directory-Verbunddienste (AD FS) \( AD FS \) in Windows Server 2012 R2 wird die Rolle eines Verbund Server Proxys von einem neuen Remote Zugriffs Rollen Dienst namens webanwendungsproxy behandelt. Um Ihre AD FS für den Zugriff von außerhalb des Unternehmensnetzwerks zu aktivieren. Dies war der Zweck der Bereitstellung eines Verbund Server Proxys in Legacy Versionen von AD FS, wie z. b. AD FS 2,0 und AD FS in Windows Server 2012, Sie können einen oder mehrere webanwendungsproxys für AD FS in Windows Server 2012 R2 bereitstellen.  
  
Im Kontext von AD FS fungiert der webanwendungsproxy als AD FS Verbund Server Proxy. Darüber hinaus bietet der Webanwendungsproxy Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können. Weitere Informationen zum Webanwendungsproxy-Rollendienst finden Sie unter „Übersicht über den Webanwendungsproxy“.  
  
Bei der Planung die Bereitstellung von Web Application Proxy können Sie die Informationen in den folgenden Themen lesen:  
  
-   [Planen der Infrastruktur für den webanwendungsproxy (WAP)](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))  
  
-   [Planen des Webanwendungsproxy-Servers](/previous-versions/orphan-topics/ws.11/dn383647(v=ws.11))  
  
Sie können zum Bereitstellen eines Webanwendungsproxys die Schritte in den folgenden Themen ausführen:  
  
-   [Konfigurieren der Infrastruktur für den Webanwendungsproxy](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383644(v=ws.11))  
  
-   [Installieren und Konfigurieren des Webanwendungsproxy-Servers](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383662(v=ws.11))  
  
 
## <a name="see-also"></a>Weitere Informationen 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
