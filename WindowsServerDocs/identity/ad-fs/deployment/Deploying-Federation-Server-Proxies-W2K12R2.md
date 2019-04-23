---
ms.assetid: 222e9f93-7c41-4527-8a98-8f7fbc7a58af
title: Bereitstellen von Verbundserverproxys
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dc49d8f4b656fdbb92083aa3c60bc4ce81091e9b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890821"
---
# <a name="deploying-federation-server-proxies"></a>Bereitstellen von Verbundserverproxys

>Gilt für: Windows Server 2016, Windows Server 2012 R2

In Active Directory-Verbunddienste \(AD FS\) in Windows Server 2012 R2, ist die Rolle eines Verbundserverproxys durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy übernommen. Zum Aktivieren von AD FS für Zugriff von außerhalb des Unternehmensnetzwerks, das war der Zweck der Bereitstellung eines Verbundserverproxys in Legacyversionen von AD FS, z. B. AD FS 2.0 und AD FS unter Windows Server 2012 können Sie eine oder mehrere webanwendungsproxys für ein bereitstellen. D-FS unter Windows Server 2012 R2.  
  
Im Kontext von AD FS-Webanwendungsproxy als einen AD FS-Verbundserverproxy Funktionen. Darüber hinaus bietet der Webanwendungsproxy Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können. Weitere Informationen zum Webanwendungsproxy-Rollendienst finden Sie unter „Übersicht über den Webanwendungsproxy“.  
  
Bei der Planung die Bereitstellung von Web Application Proxy können Sie die Informationen in den folgenden Themen lesen:  
  
-   [Planen der Infrastruktur für Webanwendungsproxy (WAP)](https://technet.microsoft.com/library/dn383648.aspx)  
  
-   [Planen Sie die Webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383647.aspx)  
  
Sie können zum Bereitstellen eines Webanwendungsproxys die Schritte in den folgenden Themen ausführen:  
  
-   [Konfigurieren der Infrastruktur für den Webanwendungsproxy](https://technet.microsoft.com/library/dn383644.aspx)  
  
-   [Installieren Sie und konfigurieren Sie die Webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383662.aspx)  
  
 
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS-Bereitstellung geführt.](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

