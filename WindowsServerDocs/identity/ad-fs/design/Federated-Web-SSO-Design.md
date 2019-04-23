---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: Federated-Web-SSO – Entwurf
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b85f49ac0556bf9b3542a23514d7fcbf82d2d88e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865141"
---
# <a name="federated-web-sso-design"></a>Federated-Web-SSO – Entwurf

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federated Web Single\-anmelden\-auf \(SSO\) Entwurf in Active Directory Federation Services \(AD FS\) umfasst die sichere Kommunikation, die mehrere Firewalls, umfasst Umkreisnetzwerk Netzwerke und Namen\-Auflösung-Server – zusätzlich zu den gesamten Routinginfrastruktur im Internet.  
  
Dieser Entwurf wird in der Regel verwendet, wenn zwei Organisationen die Einrichtung eine verbundvertrauensstellung, damit Benutzer in einer Organisation erstellen \(der Kontopartnerorganisation\) für Zugriff auf\-basierte Anwendungen oder Dienste , die AD FS, in der anderen Organisation geschützt werden \(der Ressourcenpartnerorganisation\).  
  
Anders ausgedrückt, ist eine verbundvertrauensstellung die verkörperung einer geschäftlichen\-Servicelevel-Vereinbarung oder Partnerschaft zwischen zwei Organisationen. Wie in der folgenden Abbildung gezeigt, können Sie eine verbundvertrauensstellung zwischen zwei Unternehmen, die Ergebnisse in einem End herstellen\-zu\-End Verbundszenario.  
  
![Federated-Web-sso](media/adfs2_FederatedWebSSODesign.gif)  
  
Die\-Form eines Pfeils in der Abbildung gibt die Richtung der verbundvertrauensstellung an vertrauen, die – wie die Richtung von Windows-Vertrauensstellungen – verweist immer auf die Kontoseite der Gesamtstruktur. Dies bedeutet, dass die Authentifizierung von der Kontopartnerorganisation zur Ressourcenpartnerorganisation verläuft.  
  
In diesem Verbundweb-SSO-Entwurf, zwei Verbundserver \(einer in Fabrikam und der andere in Contoso\) Weiterleiten von authentifizierungsanforderungen von Benutzerkonten in Fabrikam Web\-basierte Anwendungen oder Diensten in Contoso.  
  
> [!NOTE]  
> Zur Erhöhung der Sicherheit können Sie Verbundserverproxys Relayanforderungen für Verbundserver, die nicht direkt über das Internet zugänglich sind.  
  
In diesem Beispiel ist Fabrikam der Identitäts- bzw. Kontoanbieter. Der Teil "Fabrikam" Federated-Web-SSO-Entwurf verwendet das folgende Ziel des AD FS-Bereitstellung:  
  
-   [Geben Sie Ihre Active Directory-Benutzerzugriff auf die Anwendungen und Dienste anderer Organisationen](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
Contoso ist der Ressourcenanbieter. Der Teil "Contoso" Federated-Web-SSO-Entwurf werden die folgenden AD FS-Bereitstellungsziele erreicht:  
  
-   [Geben Sie Benutzern in einer anderen Organisationszugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Geben Sie Ihre Active Directory-Benutzerzugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
Eine detaillierte Liste der Aufgaben, die Sie zum Planen und Bereitstellen der Verbundweb-SSO-Entwurfs verwenden können, finden Sie unter [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
