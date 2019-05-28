---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: Web-SSO-Entwurf
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 29d50a4d1855e609b6ac9ee627256201074a5033
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190722"
---
# <a name="web-sso-design"></a>Web-SSO-Entwurf

In den einzelnen Web\-anmelden\-auf \(SSO\) Entwurf in Active Directory Federation Services \(AD FS\), Benutzer müssen nur einmal authentifizieren, für den Zugriff auf mehrere AD FS\- geschützte Anwendungen oder Dienste. Bei diesem Entwurf sind alle Benutzer extern, und es gibt keine Verbundvertrauensstellung, da keine Partnerorganisationen vorhanden sind. In der Regel stellen Sie dieses Design, wenn Sie einzelne Kunden einen Zugriff auf eine oder mehrere AD FS-gesicherte Dienste oder Anwendungen über das Internet bereitstellen, wie in der folgenden Abbildung dargestellt möchten.  
  
![Web-Sso-Entwurf](media/adfs2_WebSSODesign.gif)  
  
Mit den Web-SSO-Entwurf einer Organisation, in der Regel die hostet eines AD FS\-gesicherte Anwendung oder Dienst in einem Umkreisnetzwerk kann einen separaten Speicher mit Kundenkonten im Umkreisnetzwerk, dadurch wird es einfacher zu isolieren von Kunden verwalten Konten von Mitarbeiterkonten.  
  
Sie können die lokalen Konten für Kunden im Umkreisnetzwerk mithilfe von entweder Active Directory-Domänendienste verwalten \(AD DS\), SQL Server oder einem benutzerdefinierten Attributspeicher.  
  
Dieser Entwurf stimmt mit dem Bereitstellungsziel in [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)überein.  
  
Eine detaillierte Liste der Aufgaben, die Sie zum Planen und Bereitstellen Ihrer Web-SSO-Entwurfs verwenden können, finden Sie unter [Prüfliste: Implementieren eines Web-SSO-Entwurfs](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
