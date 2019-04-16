---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: Bereitstellen der Active Directory-Benutzern den Zugriff auf die Anwendungen und Dienste anderer Organisationen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d50d26c5c654e5c91b82f6f209e21f257221c12d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Bereitstellen der Active Directory-Benutzern den Zugriff auf die Anwendungen und Dienste anderer Organisationen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Bereitstellungsziel für Active Directory Federation Services \(AD FS\) baut auf das Ziel in [bieten Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md).  
  
Wenn Sie ein Administrator in der Kontopartnerorganisation sind und Sie haben ein Bereitstellungsziel darin besteht, verbundzugriff für Mitarbeiter bereitstellen gehosteten Ressourcen in einer anderen Organisation:  
  
-   Singlethread-Standardparameter auf \(SSO\) Funktionen können Mitarbeiter, die Active Directory-Domäne im Unternehmensnetzwerk angemeldet sind Zugriff auf mehrere webbasierte Anwendungen oder Dienste, die von AD FS geschützt sind, wenn die Programme oder Dienste in einer anderen Organisation befinden. Weitere Informationen finden Sie unter [Federated Web SSO Design](Federated-Web-SSO-Design.md).  
  
    Fabrikam möchte z.B. Mitarbeiter Unternehmensnetzwerk Zugriff auf Webdienste verbunden haben, die von Contoso gehostet werden.  
  
-   Remotemitarbeiter, die Active Directory-Domäne angemeldet sind, können AD FS-Token abrufen, von dem Verbundserver in Ihrer Organisation verbundzugriff auf AD FS-gesicherte webbasierte Anwendungen oder Dienste, die in einer anderen Organisation gehostet werden zu erhalten.  
  
    Fabrikam möchte z.B. Remotemitarbeiter AD FS-gesicherte Services verbundzugriff auf, die Contoso gehostet werden, ohne dass die Fabrikam-Mitarbeiter im Unternehmensnetzwerk von Fabrikam sein.  
  
Zusätzlich zu den grundlegenden Komponenten, die in beschriebenen [bieten Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) und, der in der folgenden Abbildungschattiert dargestellt werden, die folgenden Komponenten sind für dieses Bereitstellungsziel erforderlich:  
  
-   **Partner-Verbundserverproxy zu berücksichtigen:** Mitarbeiter, die den Verbunddienst oder die Anwendung aus dem Internet zugreifen können diese AD FS-Komponente verwenden, um die Authentifizierung durchführen. Standardmäßig führt diese Komponente Formularauthentifizierung, aber sie können auch Standardauthentifizierung durchführen. Sie können auch konfigurieren, dass diese Komponente um \(SSL\) Secure Sockets Layer-Clientauthentifizierung durchzuführen, wenn Mitarbeitern Ihrer Organisation Zertifikate vorliegen. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
-   **Umkreis-DNS:** diese Implementierung des Domain Name System \(DNS\) bietet die Hostnamen für das Umkreisnetzwerk. Weitere Informationen zum Konfigurieren des Umkreis-DNS für einen Verbundserverproxy finden Sie unter [Name Resolution Requirements for Federation Server Proxies](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  
-   **Remotemitarbeiter:** der Remotemitarbeiter greift auf einer webbasierten Anwendung \ (über einen unterstützten Web-Browser\) oder einen webbasierten Dienst \ mithilfe von gültigen Anmeldeinformationen aus dem Unternehmensnetzwerk (über eine Application\), während er sich außerhalb des Standorts im Internet befindet. Clientcomputer des Mitarbeiters am Remotestandort kommuniziert direkt mit der Verbundserverproxy ein Token zu generieren und an die Anwendung oder den Dienst zu authentifizieren.  
  
Nach dem Überprüfen der Informationen in den verknüpften Themen können Sie beginnen, Umsetzung dieses Bereitstellungsziels anhand der Schrittein [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md).  
  
Die folgende Abbildungzeigt die einzelnen der erforderlichen Komponenten für dieses Bereitstellungsziel für AD FS.  
  
![Der Zugriff auf Ihre Apps](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
