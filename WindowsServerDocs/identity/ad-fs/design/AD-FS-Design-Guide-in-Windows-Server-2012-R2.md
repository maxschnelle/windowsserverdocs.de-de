---
ms.assetid: a8558c9d-0606-4881-93b2-f2d2716b18e7
title: AD FS-Entwurfshandbuch in Windows Server 2012 R2
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2d15f680f28c54da75100a03f7b85e880442d9be
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191740"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>AD FS-Entwurfshandbuch in WindowsServer 

Active Directory-Verbunddienste \(AD FS\) bietet vereinfachten und sicheren Identitätsverbund sowie Web-SSO\-auf \(SSO\) Funktionen für Endbenutzer, die auf Anwendungen zugreifen möchten in einem AD FS\-Unternehmen, in verbundpartnerorganisationen oder in der Cloud gesichert.  
  
In Windows Server® 2012 R2 umfasst AD FS einen Verbunddienst-Rollendienst, der als Identitätsanbieter agiert \(Benutzer authentifiziert, um Sicherheitstoken für Anwendungen bereitzustellen, die AD FS-Vertrauensstellung\) oder als verbundanbieter \( nimmt Token anderer Identitätsanbieter entgegen und stellt Sicherheitstoken für Anwendungen, die AD FS-Vertrauensstellung bereit\).  
  
Die Funktion der Bereitstellung von Extranetzugriff auf Anwendungen und Dienste, die von AD FS in Windows Server 2012 R2 geschützt sind, erfolgt jetzt durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy. Dies ist eine Abweichung von früheren Versionen von Windows Server, in denen diese Funktion von einem AD FS-Verbundserverproxys übernommen wurde. Webanwendungsproxy ist eine Serverrolle, die für die AD FS Zugang bietet\-bezogene Extranetszenario und sonstige Extranetszenarios. Weitere Informationen zum Webanwendungsproxy finden Sie unter [Web Application Proxy-Handbuch mit exemplarischer Vorgehensweise](https://technet.microsoft.com/library/dn280944.aspx).  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Dieses Handbuch bietet Empfehlungen helfen Ihnen beim Planen einer neuen Bereitstellung von AD FS, basierend auf den Anforderungen Ihrer Organisation. Dieses Handbuch ist für die Verwendung durch einen Infrastrukturspezialisten oder Systemarchitekten vorgesehen. Planen der AD FS-Bereitstellung lassen sich die wesentlichen Entscheidungspunkte hervorheben. Bevor Sie dieses Handbuch lesen, sollten Sie ein gutes Verständnis der Funktionsweise von AD FS auf einer Funktionsebene verfügen. Weitere Informationen finden Sie unter [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md).  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung  
  
-   [Identifizieren der AD FS-Bereitstellungsziele](Identify-Your-AD-FS-Deployment-Goals.md)  
  
-   [Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
  
-   [AD FS-Anforderungen](AD-FS-Requirements.md)  
  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Entwurf](../../ad-fs/AD-FS-Design.md)  
  

