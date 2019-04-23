---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d50d26c5c654e5c91b82f6f209e21f257221c12d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843581"
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diese Active Directory Federation Services \(AD FS\) -Bereitstellungsziel baut auf das Ziel in [Provide Your Active Directory Users Access auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md).  
  
Wenn Sie Administrator der Kontopartnerorganisation sind und ihr Bereitstellungsziel darin besteht, Mitarbeitern Verbundzugriff auf Ressourcen zu ermöglichen, die in einer anderen Organisation gehostet werden, lesen Sie bitte Folgendes:  
  
-   Mitarbeiter, die Active Directory-Domäne im Unternehmensnetzwerk angemeldet sind, können einzelne\-anmelden\-auf \(SSO\) Funktionalität für den Zugriff auf mehrere Web\-basierte Anwendungen oder Dienste, die werden durch AD FS geschützt bei der Anwendungen oder Dienste in einer anderen Organisation sind. Weitere Informationen finden Sie unter [Federated Web SSO Design](Federated-Web-SSO-Design.md).  
  
    Beispielsweise könnte Fabrikam fordern, dass Mitarbeiter im Unternehmensnetzwerk Verbundzugriff auf Webdienste erhalten, die von Contoso gehostet werden.  
  
-   Remotemitarbeiter, die Active Directory-Domäne angemeldet sind, können AD FS-Token erhalten, von dem Verbundserver in Ihrer Organisation, um verbundzugriff auf AD FS-gesicherte Web zu erhalten\-basierte Anwendungen oder Dienste, die in einem anderen gehostet werden die Organisation.  
  
    Fabrikam sollten z. B. Remotemitarbeiter, die Zugriff auf AD FS-gesicherte Dienste verbunden haben, die in Contoso gehostet werden, ohne die Fabrikam-Mitarbeiter im Unternehmensnetzwerk von Fabrikam sein.  
  
Zusätzlich zu den grundlegenden Komponenten, die in [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) beschrieben und in der folgenden Abbildung schattiert dargestellt werden, sind für dieses Bereitstellungsziel folgende Komponenten erforderlich:  
  
-   **Partner Kontoverbundserverproxy:** Mitarbeiter, die den Verbunddienst oder die Anwendung über das Internet zugreifen können diese AD FS-Komponente verwenden, um die Authentifizierung durchzuführen. Standardmäßig führt diese Komponente Formularauthentifizierung durch, kann jedoch auch Standardauthentifizierung durchführen. Sie können auch konfigurieren, diese Komponente zum Ausführen von Secure Sockets Layer \(SSL\) Clientauthentifizierung, wenn Mitarbeitern Ihrer Organisation Zertifikate vorliegen. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
-   **Umkreis-DNS:** Diese Implementierung des Domain Name System \(DNS\) bietet die Hostnamen für das Umkreisnetzwerk. Weitere Informationen zum Konfigurieren des Umkreis-DNS für einen Verbundserverproxy finden Sie unter [Namensauflösungsanforderungen für Verbundserverproxys](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  
-   **Remotemitarbeiter:** Der Remotemitarbeiter greift auf eine Web\--basierten Anwendung \(über einen unterstützten Webbrowser\) oder eines Webdiensts\--basierten Diensts \(durch eine Anwendung\), mit gültigen Anmeldeinformationen aus dem Unternehmensnetzwerk, während er sich außerhalb des Standorts im Internet befindet. Clientcomputer des Mitarbeiters am Remotestandort kommuniziert direkt mit dem Verbundserverproxy Token generieren und an die Anwendung oder Dienst zu authentifizieren.  
  
Nach dem Durchlesen der Informationen in den verknüpften Themen können Sie beginnen können, Umsetzung dieses Bereitstellungsziels anhand der Schritte in [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md).  
  
Die folgende Abbildung zeigt jede der erforderlichen Komponenten für dieses Bereitstellungsziel für AD FS.  
  
![der Zugriff auf Ihre apps](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
