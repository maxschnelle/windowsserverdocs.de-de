---
ms.assetid: a8558c9d-0606-4881-93b2-f2d2716b18e7
title: AD FS-Entwurfshandbuch in Windows Server 2012 R2
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 614bc2b4571dd8a1b35c075ae1dec6934e77e148
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408168"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>AD FS Entwurfs Handbuch in Windows Server 

Active Directory-Verbunddienste (AD FS) \(AD FS\) bietet einen vereinfachten, gesicherten Identitäts Verbund und Web-SSO-\-für \(SSO-\) Funktionen für Endbenutzer, die in einem AD FS\-gesicherten Unternehmen, in Verbund Partnerorganisationen oder in der Cloud auf Anwendungen zugreifen möchten.  
  
In Windows Server® 2012 R2 umfasst AD FS einen Verbund Dienst-Rollen Dienst, der als Identitäts Anbieter fungiert \(die Benutzer authentifiziert, um Sicherheits Token für Anwendungen bereitzustellen, die AD FS\) oder als Verbund Anbieter als vertrauenswürdig eingestuft werden \(die Token von anderen Identitäts Anbietern nutzt und Sicherheits Token für Anwendungen bereitstellt, die AD FS\)Vertrauen.  
  
Die Funktion der Bereitstellung von Extranetzugriff auf Anwendungen und Dienste, die von AD FS in Windows Server 2012 R2 geschützt sind, erfolgt jetzt durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy. Dies ist eine Abweichung von früheren Versionen von Windows Server, in denen diese Funktion von einem AD FS-Verbundserverproxys übernommen wurde. Webanwendungsproxy ist eine Server Rolle, die den Zugriff auf die AD FS\-verwandten Extranetszenarios und andere Extranetszenarien ermöglicht. Weitere Informationen zum webanwendungsproxy finden Sie unter Exemplarische Vorgehensweise zum [webanwendungsproxy](https://technet.microsoft.com/library/dn280944.aspx)  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Dieses Handbuch enthält Empfehlungen zum Planen einer neuen Bereitstellung von AD FS, basierend auf den Anforderungen Ihrer Organisation. Dieses Handbuch ist für die Verwendung durch einen Infrastrukturspezialisten oder Systemarchitekten vorgesehen. Es hebt die wichtigsten Entscheidungspunkte hervor, wenn Sie Ihre AD FS Bereitstellung planen. Bevor Sie dieses Handbuch lesen, sollten Sie wissen, wie AD FS auf einer Funktionsebene funktioniert. Weitere Informationen finden Sie unter [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md).  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung  
  
-   [Identifizieren der AD FS-Bereitstellungsziele](Identify-Your-AD-FS-Deployment-Goals.md)  
  
-   [Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
  
-   [AD FS-Anforderungen](AD-FS-Requirements.md)  
  
  
## <a name="see-also"></a>Weitere Informationen  
[AD FS-Entwurf](../../ad-fs/AD-FS-Design.md)  
  

