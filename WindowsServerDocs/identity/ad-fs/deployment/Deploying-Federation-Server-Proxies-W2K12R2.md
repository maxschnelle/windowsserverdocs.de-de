---
ms.assetid: 222e9f93-7c41-4527-8a98-8f7fbc7a58af
title: Bereitstellen von Verbundserverproxys
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 04837c8b38f1f6cdf048f7d8744d9cd0f61ebb0d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855453"
---
# <a name="deploying-federation-server-proxies"></a>Bereitstellen von Verbundserverproxys

In Active Directory-Verbunddienste (AD FS) \(AD FS\) in Windows Server 2012 R2 wird die Rolle eines Verbund Server Proxys von einem neuen Remote Zugriffs-Rollen Dienst namens webanwendungsproxy behandelt. Um Ihre AD FS für den Zugriff von außerhalb des Unternehmensnetzwerks zu aktivieren. Dies war der Zweck der Bereitstellung eines Verbund Server Proxys in Legacy Versionen von AD FS, wie z. b. AD FS 2,0 und AD FS in Windows Server 2012, Sie können einen oder mehrere webanwendungsproxys für AD FS in Windows Server 2012 R2 bereitstellen.  
  
Im Kontext von AD FS fungiert der webanwendungsproxy als AD FS Verbund Server Proxy. Darüber hinaus bietet der Webanwendungsproxy Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können. Weitere Informationen zum Webanwendungsproxy-Rollendienst finden Sie unter „Übersicht über den Webanwendungsproxy“.  
  
Bei der Planung die Bereitstellung von Web Application Proxy können Sie die Informationen in den folgenden Themen lesen:  
  
-   [Planen der Infrastruktur für den webanwendungsproxy (WAP)](https://technet.microsoft.com/library/dn383648.aspx)  
  
-   [Planen des webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383647.aspx)  
  
Sie können zum Bereitstellen eines Webanwendungsproxys die Schritte in den folgenden Themen ausführen:  
  
-   [Konfigurieren der webanwendungsproxy-Infrastruktur](https://technet.microsoft.com/library/dn383644.aspx)  
  
-   [Installieren und Konfigurieren des webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383662.aspx)  
  
 
## <a name="see-also"></a>Weitere Informationen 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS Bereitstellungs Handbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

