---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: Federated-Web-SSO-Entwurf
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b85f49ac0556bf9b3542a23514d7fcbf82d2d88e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="federated-web-sso-design"></a>Federated-Web-SSO-Entwurf

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Das Design Federated-Web-Single\-Sign\-On \(SSO\) in Active Directory Federation Services \(AD FS\) umfasst die sicheren Kommunikation, die mehrere Firewalls, Umkreisnetzwerke und Tokentypen Auflösung Server umfasst – zusätzlich zu den gesamten Routinginfrastruktur Internet.  
  
Dieser Entwurf wird in der Regel verwendet, wenn zwei Organisationen die Einrichtung eine verbundvertrauensstellung, damit Benutzer in einer Organisation können erstellen \ (das Konto Partner Organization\) zum Zugriff auf webbasierte Anwendungen oder Dienste, die von AD FS in der anderen Organisation geschützt sind \ (die Ressource Partner Organization\).  
  
Anders ausgedrückt, ist eine verbundvertrauensstellung die verkörperung einer Business\ Vereinbarung oder Partnerschaft zwischen zwei Organisationen. Wie in der folgenden Abbildunggezeigt, können Sie eine verbundvertrauensstellung zwischen zwei Unternehmen, die Ergebnisse in einem Verbundszenario zur Implementierung-zu-Ende-einrichten.  
  
![Federated-Web-sso](media/adfs2_FederatedWebSSODesign.gif)  
  
Der einmaligen-Wege-Pfeil in der Abbildunggibt die Richtung der verbundvertrauensstellung an vertrauen, die – wie die Richtung von Windows-Vertrauensstellungen: Zeigt immer auf die Kontoseite der Gesamtstruktur. Dies bedeutet, dass die Authentifizierung von der Kontopartnerorganisation zur Ressourcenpartnerorganisation fließt.  
  
In diesem Federated-Web-SSO-Entwurf, zwei Verbundserver \ (in Fabrikam und der andere in Contoso\) weiterleiten Authentifizierungsanforderungen von Benutzerkonten in Fabrikam zu webbasierten Anwendungen oder Diensten in Contoso.  
  
> [!NOTE]  
> Zur Erhöhung der Sicherheit können Sie Verbundserverproxys Relay-Anfragen an Verbundserver, die nicht direkt über das Internet zugänglich sind.  
  
In diesem Beispiel ist Fabrikam der Identitäts- bzw.,-Anbieter. Der Fabrikam-Teil des Federated-Web-SSO-Entwurf verwendet die folgenden AD FS-Bereitstellungsziele:  
  
-   [Bereitstellen der Active Directory-Benutzern den Zugriff auf die Anwendungen und Dienste anderer Organisationen](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
Contoso ist der Ressourcenanbieter. Der Contoso-Teil des Federated-Web-SSO-Entwurf werden die folgenden AD FS-Bereitstellungsziele erreicht:  
  
-   [Bieten Sie Benutzern in einer anderen Organisationszugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Bereitstellen der Active Directory-Benutzern den Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
Eine detaillierte Liste der Aufgaben, die Sie zum Planen und Bereitstellen der Federated-Web-SSO-Entwurfs verwenden können, finden Sie unter [Checklist: Implementing a Federated Web SSO Design ](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
