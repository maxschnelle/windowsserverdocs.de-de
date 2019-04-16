---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: Web-SSO-Entwurf
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1b8344594c9fc477ed8424c716ec8d7f7fd91ef3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="web-sso-design"></a>Web-SSO-Entwurf

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Im Web Singlethread-Standardparameter auf \(SSO\) Design in Active Directory Federation Services \(AD FS\) müssen Benutzer nur einmal authentifizieren, um mehrere AD FS\ geschützte Anwendungen oder Dienste zuzugreifen. Bei diesem Entwurf sind alle Benutzer extern, und keine verbundvertrauensstellung vorhanden ist, da keine Partnerorganisationen vorhanden sind. In der Regel stellen Sie diesen Entwurf bereit, wenn Sie einzelnen Kunden Zugriff auf eine AD FS-gesicherte Dienste oder Anwendungen über das Internet bereitstellen, wie in der folgenden Abbildung dargestellt möchten.  
  
![Web-Sso-Entwurf](media/adfs2_WebSSODesign.gif)  
  
Mit der Web-SSO-Entwurf kann eine Organisation, die in der Regel eine AD-FS\-gesicherte Anwendung hostet oder Dienst in einem Umkreisnetzwerk einen separaten Speicher mit Kundenkonten im Umkreisnetzwerk, mit dessen Hilfe Kundenkonten von Mitarbeiterkonten isoliert leichter verwalten kann.  
  
Sie können die lokalen Konten für Kunden im Umkreisnetzwerk mithilfe von Active Directory-Domänendienste \(AD DS\), SQL Server oder eines benutzerdefinierten Attributspeichers verwalten.  
  
Dieser Entwurf stimmt mit dem Bereitstellungsziel in [bieten Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md).  
  
Eine detaillierte Liste der Aufgaben, die Sie zum Planen und Bereitstellen Ihres Web-SSO-Entwurfs verwenden können, finden Sie unter [Prüfliste: Implementieren eines Web-SSO-Entwurfs](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
