---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: Federated-Web-SSO – Entwurf
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6a3e7eb6c42c8190da799c88c1e947e6aef1c29f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408104"
---
# <a name="federated-web-sso-design"></a>Federated-Web-SSO – Entwurf

Das Federated Web Single @ no__t-0sign @ no__t-1On \(sso @ no__t-3 Design in Active Directory-Verbunddienste (AD FS) \(AD FS @ no__t-5 umfasst eine sichere Kommunikation, die mehrere Firewalls, Umkreis Netzwerke und den Namen @ no__t-6resolution umfasst. Server – zusätzlich zur gesamten Internet Routing Infrastruktur.  
  
Dieser Entwurf wird in der Regel verwendet, wenn zwei Organisationen eine Verbund Vertrauensstellung erstellen, damit Benutzer in einer Organisation \(der Konto Partnerorganisation @ no__t-1 auf Web @ no__t-basierte Anwendungen oder Dienste zugreifen können, die durch geschützt sind. AD FS in der anderen Organisation \(the Resource Partner Organization @ no__t-4.  
  
Anders ausgedrückt: eine Verbund Vertrauensstellung ist die Verkörperung einer Geschäfts-@ no__t-Vereinbarung oder Partnerschaft zwischen zwei Organisationen. Wie in der folgenden Abbildung gezeigt, können Sie eine Verbund Vertrauensstellung zwischen zwei Unternehmen einrichten, die zu einem Verbund Szenario @ no__t-0to @ no__t-1End führt.  
  
![Verbund-Web-SSO](media/adfs2_FederatedWebSSODesign.gif)  
  
Der einen @ no__t-0way-Pfeil in der Abbildung gibt die Richtung der Verbund Vertrauensstellung an, die – wie die Richtung von Windows-Vertrauens Stellungen – immer auf die Kontoseite der Gesamtstruktur zeigt. Dies bedeutet, dass die Authentifizierung von der Kontopartnerorganisation zur Ressourcenpartnerorganisation verläuft.  
  
In diesem Federated-Web-SSO-Entwurf leiten zwei Verbund Server \(one in Fabrikam und der andere in "no__t" von "-1" Authentifizierungsanforderungen von Benutzerkonten in Fabrikam an Web @ no__t-2based-Anwendungen oder-Dienste in "Configuration Manager" weiter.  
  
> [!NOTE]  
> Zur zusätzlichen Sicherheit können Sie Verbund Server Proxys verwenden, um Anforderungen an Verbund Server weiterzuleiten, auf die nicht direkt über das Internet zugegriffen werden kann.  
  
In diesem Beispiel ist Fabrikam der Identitäts- bzw. Kontoanbieter. Der Fabrikam-Teil des Entwurfs "Federated-Web-SSO" verwendet das folgende AD FS Bereitstellungs Ziel:  
  
-   [Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
Contoso ist der Ressourcenanbieter. Der Teil "" von "Federated-Web-SSO" erreicht die folgenden AD FS Bereitstellungs Ziele:  
  
-   [Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für die Benutzer anderer Organisationen](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
Eine Liste der detaillierten Aufgaben, die Sie zum Planen und Bereitstellen des Entwurfs für Federated-Web-SSO verwenden können, finden Sie unter [checkliste: Implementieren eines Federated-Web-SSO-Entwurfs @ no__t-0.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
