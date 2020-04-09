---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: Web-SSO-Entwurf
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 47c946ac617cc64c224c1bc3153fcaf55c2d069c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858513"
---
# <a name="web-sso-design"></a>Web-SSO-Entwurf

Im Web-SSO-\-Sign\-on \(SSO\) Design in Active Directory-Verbunddienste (AD FS) \(AD FS\)müssen Benutzer sich nur einmal authentifizieren, um auf mehrere AD FS\-gesicherten Anwendungen oder Dienste zuzugreifen. Bei diesem Entwurf sind alle Benutzer extern, und es gibt keine Verbundvertrauensstellung, da keine Partnerorganisationen vorhanden sind. In der Regel stellen Sie diesen Entwurf bereit, wenn Sie einzelnen Consumer oder Kunden Zugriff auf eine oder mehrere AD FS – gesicherte Dienste oder Anwendungen über das Internet bereitstellen möchten, wie in der folgenden Abbildung dargestellt.  
  
![Web-SSO-Entwurf](media/adfs2_WebSSODesign.gif)  
  
Beim Web-SSO-Entwurf kann eine Organisation, die in der Regel eine AD FS\-gesicherten Anwendung oder einen Dienst in einem Umkreis Netzwerk hostet, einen separaten Speicher von Kundenkonten im Umkreis Netzwerk verwalten, was das Isolieren von Kundenkonten von Mitarbeiter Konten vereinfacht.  
  
Sie können die lokalen Konten für Kunden im Umkreis Netzwerk verwalten, indem Sie entweder Active Directory Domain Services \(AD DS\), SQL Server oder einen benutzerdefinierten Attribut Speicher verwenden.  
  
Dieser Entwurf stimmt mit dem Bereitstellungsziel in [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)überein.  
  
Eine detaillierte Liste der Aufgaben, die Sie zum Planen und Bereitstellen Ihres Web-SSO-Entwurfs verwenden können, finden Sie unter [Checklist: Implementing a Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md).  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
