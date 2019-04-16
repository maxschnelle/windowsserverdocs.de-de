---
ms.assetid: 222e9f93-7c41-4527-8a98-8f7fbc7a58af
title: Bereitstellen von Verbundserverproxys
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dc49d8f4b656fdbb92083aa3c60bc4ce81091e9b
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-federation-server-proxies"></a>Bereitstellen von Verbundserverproxys

>Gilt für: Windows Server 2016, Windows Server2012 R2

In Active Directory Federation Services \(AD FS\) in Windows Server2012 R2 wird die Rolle eines Verbundserverproxys durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy behandelt. Zum Aktivieren von AD FS ermöglichen den Zugriff von außerhalb des Unternehmensnetzwerks, war der Zweck der Bereitstellung eines Verbundserverproxys in Legacyversionen von AD FS, z.B. AD FS 2.0 und AD FS unter Windows Server2012 können Sie eine oder mehrere webanwendungsproxys für AD FS unter Windows Server2012 R2 bereitstellen.  
  
Im Kontext von AD FS funktioniert Web Application Proxy als ein AD FS-Verbundserverproxy. Darüber hinaus bietet Webanwendungsproxy Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk So ermöglichen Sie Benutzern auf einem beliebigen Gerät für den Zugriff darauf von außerhalb des Unternehmensnetzwerks. Weitere Informationen über den Webanwendungsproxy-Rollendienst finden Sie im Web Application Proxy (Übersicht).  
  
Bei der Planung die Bereitstellung von Web Application Proxy können Sie überprüfen, die Informationen in den folgenden Themen:  
  
-   [Planen der Infrastruktur für Webanwendungsproxy (WAP)](https://technet.microsoft.com/library/dn383648.aspx)  
  
-   [Planen der Webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383647.aspx)  
  
Zum Bereitstellen von Web Application Proxy führen Sie die Verfahren in den folgenden Themen:  
  
-   [Konfigurieren der Infrastruktur für den Webanwendungsproxy](https://technet.microsoft.com/library/dn383644.aspx)  
  
-   [Installieren Sie und konfigurieren Sie die Webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383662.aspx)  
  
 
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server2012 R2 ADFS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

