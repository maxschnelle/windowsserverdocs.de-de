---
ms.assetid: a8558c9d-0606-4881-93b2-f2d2716b18e7
title: AD FS-Entwurfshandbuch in Windows Server2012 R2
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 498b399818fb8c9e463f9990fa13c87648c0a33d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-design-guide-in-windows-server-2012-r2"></a>AD FS-Entwurfshandbuch in Windows Server2012 R2

>Gilt für: Windows Server 2016, Windows Server2012 R2

Active Directory-Verbunddienste \(AD FS\) bietet einen vereinfachten und sicheren Identitätsverbund sowie einzelne Standardparameter auf \(SSO\) Funktionen für Endbenutzer, die in einem AD FS\-gesicherten Unternehmen, in verbundpartnerorganisationen oder in der Cloud auf Anwendungen zugreifen möchten.  
  
In Windows Server® 2012 R2 umfasst AD FS einen Verbunddienst-Rollendienst, der als Identitätsanbieter agiert \ (Benutzer authentifiziert, um Sicherheitstoken für Anwendungen bereitzustellen, die AD-FS\ vertrauen) oder als verbundanbieter \ (nimmt Token anderer Identitätsanbieter entgegen und stellt Sicherheitstoken für Anwendungen, die AD-FS\ vertrauen).  
  
Die Funktion der Bereitstellung von Extranetzugriff auf Anwendungen und Dienste, die von AD FS unter Windows Server2012 R2 geschützt sind erfolgt jetzt durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy. Hierbei handelt es sich um eine Abweichung von früheren Versionen von Windows Server, in dem diese Funktion von einem AD FS-Verbundserverproxys übernommen wurde. Webanwendungsproxy ist eine Serverrolle, die Zugriff für die AD-FS\-bezogene Extranetszenario und sonstige Extranetszenarios bereitstellt. Weitere Informationen zu Web Application Proxy, finden Sie unter [Web Application Proxy exemplarischen](https://technet.microsoft.com/library/dn280944.aspx).  
  
## <a name="about-this-guide"></a>Informationen zum Handbuch  
Dieses Handbuch enthält Empfehlungen helfen Ihnen beim Planen einer neuen Bereitstellung von AD FS, je nach den Erfordernissen Ihrer Organisation. Dieses Handbuch ist für die Verwendung von einem infrastrukturspezialisten oder einem Systemarchitekten vorgesehen. Lassen sich die wesentlichen Entscheidungspunkte hervorheben, mit denen Sie Ihre AD FS-Bereitstellung planen. Bevor Sie dieses Handbuch lesen, sollten Sie ein gutes Verständnis der Funktionsweise von AD FS auf einer Funktionsebene verfügen. Weitere Informationen finden Sie unter [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md).  
  
## <a name="in-this-guide"></a>In diesem Handbuch  
  
-   [Identifizieren der AD FS-Bereitstellungsziele](Identify-Your-AD-FS-Deployment-Goals.md)  
  
-   [Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
  
-   [AD FS-Anforderungen](AD-FS-Requirements.md)  
  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Entwurf](../../ad-fs/AD-FS-Design.md)  
  

