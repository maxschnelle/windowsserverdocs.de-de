---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: Web-SSO-Entwurf
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d7f52cd36588a1e5de4536a760c38c147dd1e003
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407838"
---
# <a name="web-sso-design"></a>Web-SSO-Entwurf

Im Web Single @ no__t-0sign @ no__t-1On \(sso @ no__t-3 Design in Active Directory-Verbunddienste (AD FS) \(AD FS @ no__t-5 müssen Benutzer sich nur einmal authentifizieren, um auf mehrere AD FS geschützte Anwendungen oder Dienste zugreifen zu können. Bei diesem Entwurf sind alle Benutzer extern, und es gibt keine Verbundvertrauensstellung, da keine Partnerorganisationen vorhanden sind. In der Regel stellen Sie diesen Entwurf bereit, wenn Sie einzelnen Consumer oder Kunden Zugriff auf eine oder mehrere AD FS – gesicherte Dienste oder Anwendungen über das Internet bereitstellen möchten, wie in der folgenden Abbildung dargestellt.  
  
![Web-SSO-Entwurf](media/adfs2_WebSSODesign.gif)  
  
Beim Web-SSO-Entwurf kann eine Organisation, die in der Regel eine AD FS @ no__t-0gesicherte Anwendung oder einen gesicherten Dienst in einem Umkreis Netzwerk hostet, einen separaten Speicher mit Kundenkonten im Umkreis Netzwerk verwalten, was das Isolieren von Kundenkonten von Mitarbeiter Konten.  
  
Sie können die lokalen Konten für Kunden im Umkreis Netzwerk verwalten, indem Sie entweder Active Directory Domain Services \(ad DS @ no__t-1, SQL Server oder einen benutzerdefinierten Attribut Speicher verwenden.  
  
Dieser Entwurf stimmt mit dem Bereitstellungsziel in [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)überein.  
  
Eine Liste der detaillierten Aufgaben, die Sie zum Planen und Bereitstellen Ihres Web-SSO-Entwurfs verwenden können, finden Sie unter [checkliste: Implementieren eines Web-SSO-Entwurfs @ no__t-0.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
