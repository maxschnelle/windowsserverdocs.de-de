---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bcf9b9ec91c1757ad060747a6aa1589012c1ec14
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359028"
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer

Diese Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1-Bereitstellungs Ziel baut auf dem Ziel auf [, Ihren Active Directory Benutzern den Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste zu ermöglichen](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md).  
  
Wenn Sie Administrator der Kontopartnerorganisation sind und ihr Bereitstellungsziel darin besteht, Mitarbeitern Verbundzugriff auf Ressourcen zu ermöglichen, die in einer anderen Organisation gehostet werden, lesen Sie bitte Folgendes:  
  
-   Mitarbeiter, die bei einer Active Directory Domäne im Unternehmensnetzwerk angemeldet sind, können mit einem einzelnen @ no__t-0sign @ no__t-1On \(sso @ no__t-3-Funktionalität auf mehrere Web @ no__t-4based-Anwendungen oder-Dienste zugreifen, die durch AD FS gesichert sind, wenn die Anwendungen oder Dienste befinden sich in einer anderen Organisation. Weitere Informationen finden Sie unter [Federated Web SSO Design](Federated-Web-SSO-Design.md).  
  
    Beispielsweise könnte Fabrikam fordern, dass Mitarbeiter im Unternehmensnetzwerk Verbundzugriff auf Webdienste erhalten, die von Contoso gehostet werden.  
  
-   Remote Mitarbeiter, die bei einer Active Directory Domäne angemeldet sind, können AD FS Token vom Verbund Server in Ihrer Organisation erhalten, um Verbund Zugriff auf AD FS – gesicherte Web @ no__t-basierte Anwendungen oder Dienste zu erhalten, die in einer anderen Organisation gehostet werden.  
  
    Fabrikam könnte z. b. wünschen, dass die Remote Mitarbeiter Verbund Zugriff auf AD FS – gesicherte Dienste erhalten, die in "Configuration Manager" gehostet werden, ohne dass sich die Fabrikam-Mitarbeiter im Unternehmensnetzwerk von Fabrikam befinden müssen.  
  
Zusätzlich zu den grundlegenden Komponenten, die in [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) beschrieben und in der folgenden Abbildung schattiert dargestellt werden, sind für dieses Bereitstellungsziel folgende Komponenten erforderlich:  
  
-   **Konto Partner Verbund Server Proxy:** Mitarbeiter, die über das Internet auf den Verbund Dienst oder die Anwendung zugreifen, können diese AD FS Komponente zum Durchführen der Authentifizierung verwenden. Standardmäßig führt diese Komponente Formularauthentifizierung durch, kann jedoch auch Standardauthentifizierung durchführen. Sie können diese Komponente auch so konfigurieren, dass Sie Secure Sockets Layer \(ssl @ no__t-1-Client Authentifizierung ausführt, wenn Mitarbeiter in Ihrer Organisation über Zertifikate verfügen, die Sie vorweisen müssen. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
-   **Umkreis-DNS:** Diese Implementierung von Domain Name System \(dns @ no__t-1 stellt die Hostnamen für das Umkreis Netzwerk bereit. Weitere Informationen zum Konfigurieren des Umkreis-DNS für einen Verbund Server Proxy finden Sie unter [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.  
  
-   **Remotemitarbeiter:** Der Remote Mitarbeiter greift auf eine Web @ no__t-0based-Anwendung \(Durch einen unterstützten Webbrowser @ no__t-2 oder auf einen Web @ no__t-3based-Dienst \(through einer Anwendung @ no__t-5 mit gültigen Anmelde Informationen aus dem Unternehmensnetzwerk zu, während der Mitarbeiter Offsite über das Internet. Der Client Computer des Mitarbeiters am Remote Standort kommuniziert direkt mit dem Verbund Server Proxy, um ein Token zu generieren und sich bei der Anwendung oder dem Dienst zu authentifizieren.  
  
Nachdem Sie die Informationen in den verknüpften Themen überprüft haben, können Sie mit der Bereitstellung dieses Ziels beginnen, indem Sie die Schritte in [checkliste befolgen: Implementieren eines Federated-Web-SSO-Entwurfs @ no__t-0.  
  
Die folgende Abbildung zeigt die einzelnen erforderlichen Komponenten für dieses AD FS Bereitstellungs Ziel.  
  
![Zugriff auf Ihre apps](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
