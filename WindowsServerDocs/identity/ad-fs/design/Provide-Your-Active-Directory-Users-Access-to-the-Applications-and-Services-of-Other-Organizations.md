---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 13b8c3650442ac85b8b248b58372448543c8ba02
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858583"
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer

Diese Active Directory-Verbunddienste (AD FS) \(AD FS\) Bereitstellungs Ziel baut auf dem Ziel auf [, den Active Directory Benutzern den Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste zu ermöglichen](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md).  
  
Wenn Sie Administrator der Kontopartnerorganisation sind und ihr Bereitstellungsziel darin besteht, Mitarbeitern Verbundzugriff auf Ressourcen zu ermöglichen, die in einer anderen Organisation gehostet werden, lesen Sie bitte Folgendes:  
  
-   Mitarbeiter, die bei einer Active Directory Domäne im Unternehmensnetzwerk angemeldet sind, können die einmalige\-Sign\-auf \(SSO-\) Funktionalität verwenden, um auf mehrere auf Web\-basierende Anwendungen oder Dienste zuzugreifen, die durch AD FS gesichert sind, wenn sich die Anwendungen oder Dienste in einer anderen Organisation befinden. Weitere Informationen finden Sie unter [Federated Web SSO Design](Federated-Web-SSO-Design.md).  
  
    Beispielsweise könnte Fabrikam fordern, dass Mitarbeiter im Unternehmensnetzwerk Verbundzugriff auf Webdienste erhalten, die von Contoso gehostet werden.  
  
-   Remote Mitarbeiter, die bei einer Active Directory Domäne angemeldet sind, können AD FS Token vom Verbund Server in Ihrer Organisation erhalten, um Verbund Zugriff auf AD FS – gesicherte, auf Web\-basierende Anwendungen oder Dienste zu erhalten, die in einer anderen Organisation gehostet werden.  
  
    Fabrikam könnte z. b. wünschen, dass die Remote Mitarbeiter Verbund Zugriff auf AD FS – gesicherte Dienste erhalten, die in "Configuration Manager" gehostet werden, ohne dass sich die Fabrikam-Mitarbeiter im Unternehmensnetzwerk von Fabrikam befinden müssen.  
  
Zusätzlich zu den grundlegenden Komponenten, die in [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) beschrieben und in der folgenden Abbildung schattiert dargestellt werden, sind für dieses Bereitstellungsziel folgende Komponenten erforderlich:  
  
-   **Konto Partner Verbund Server Proxy:** Mitarbeiter, die über das Internet auf den Verbund Dienst oder die Anwendung zugreifen, können diese AD FS Komponente zum Durchführen der Authentifizierung verwenden. Standardmäßig führt diese Komponente Formularauthentifizierung durch, kann jedoch auch Standardauthentifizierung durchführen. Sie können diese Komponente auch so konfigurieren, dass Sie Secure Sockets Layer \(SSL-\) Client Authentifizierung ausführt, wenn Mitarbeiter in Ihrer Organisation über Zertifikate verfügen, die Sie vorweisen können. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
-   **Umkreis-DNS:** Diese Implementierung von Domain Name System \(DNS-\) stellt die Hostnamen für das Umkreis Netzwerk bereit. Weitere Informationen zum Konfigurieren des Umkreis-DNS für einen Verbund Server Proxy finden Sie unter [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.  
  
-   **Remote Mitarbeiter:** Der Remote Mitarbeiter greift über einen unterstützten Webbrowser\) oder einen Web\-basierten Dienst, der über eine Anwendungs \(\), mit gültigen Anmelde Informationen aus dem Unternehmensnetzwerk auf eine auf Web\-basierende Anwendung zu \(, während der Mitarbeiter über das Internet übertragen wird. Der Client Computer des Mitarbeiters am Remote Standort kommuniziert direkt mit dem Verbund Server Proxy, um ein Token zu generieren und sich bei der Anwendung oder dem Dienst zu authentifizieren.  
  
Nach Einsicht der Informationen in den verknüpften Themen können Sie anhand der Schritte in [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)beginnen, dieses Ziel bereitstellen.  
  
Die folgende Abbildung zeigt die einzelnen erforderlichen Komponenten für dieses AD FS Bereitstellungs Ziel.  
  
![Zugriff auf Ihre apps](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
