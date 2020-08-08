---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 0d1bf60c276932a77573acff2e4e011831e65a05
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967567"
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer

Diese Active Directory-Verbunddienste (AD FS) \( AD FS \) Bereitstellungs Ziel baut auf dem Ziel auf [, Ihren Active Directory Benutzern den Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste zu ermöglichen](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md).

Wenn Sie Administrator der Kontopartnerorganisation sind und ihr Bereitstellungsziel darin besteht, Mitarbeitern Verbundzugriff auf Ressourcen zu ermöglichen, die in einer anderen Organisation gehostet werden, lesen Sie bitte Folgendes:

-   Mitarbeiter, die bei einer Active Directory Domäne im Unternehmensnetzwerk angemeldet sind, können SSO- \- Funktionen für einmaliges Anmelden verwenden, \- \( \) um auf mehrere webbasierte \- Anwendungen oder Dienste zuzugreifen, die durch AD FS gesichert werden, wenn sich die Anwendungen oder Dienste in einer anderen Organisation befinden. Weitere Informationen finden Sie unter [Federated Web SSO Design](Federated-Web-SSO-Design.md).

    Beispielsweise könnte Fabrikam fordern, dass Mitarbeiter im Unternehmensnetzwerk Verbundzugriff auf Webdienste erhalten, die von Contoso gehostet werden.

-   Remote Mitarbeiter, die bei einer Active Directory Domäne angemeldet sind, können AD FS Token vom Verbund Server in Ihrer Organisation erhalten, um Verbund Zugriff auf AD FS – gesicherte webbasierte \- Anwendungen oder Dienste zu erhalten, die in einer anderen Organisation gehostet werden.

    Fabrikam könnte z. b. wünschen, dass die Remote Mitarbeiter Verbund Zugriff auf AD FS – gesicherte Dienste erhalten, die in "Configuration Manager" gehostet werden, ohne dass sich die Fabrikam-Mitarbeiter im Unternehmensnetzwerk von Fabrikam befinden müssen.

Zusätzlich zu den grundlegenden Komponenten, die in [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) beschrieben und in der folgenden Abbildung schattiert dargestellt werden, sind für dieses Bereitstellungsziel folgende Komponenten erforderlich:

-   **Konto Partner Verbund Server Proxy:** Mitarbeiter, die über das Internet auf den Verbund Dienst oder die Anwendung zugreifen, können diese AD FS Komponente zum Durchführen der Authentifizierung verwenden. Standardmäßig führt diese Komponente Formularauthentifizierung durch, kann jedoch auch Standardauthentifizierung durchführen. Sie können diese Komponente auch so konfigurieren, dass Secure Sockets Layer \( SSL-Client Authentifizierung durchgeführt wird, \) Wenn Mitarbeiter in Ihrer Organisation über Zertifikate verfügen müssen. Weitere Informationen hierzu finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md) (Platzieren eines Verbundserverproxys).

-   **Umkreis-DNS:** Diese Implementierung von Domain Name System \( DNS \) stellt die Hostnamen für das Umkreis Netzwerk bereit. Weitere Informationen zum Konfigurieren des Umkreis-DNS für einen Verbund Server Proxy finden Sie unter [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.

-   **Remote Mitarbeiter:** Der Remote Mitarbeiter greift über \- \( einen unterstützten Webbrowser \) oder einen webbasierten Dienst über eine Anwendung auf eine webbasierte Anwendung zu \- \( , wobei \) die gültigen Anmelde Informationen aus dem Unternehmensnetzwerk verwendet werden, während der Mitarbeiter über das Internet verfügt. Der Client Computer des Mitarbeiters am Remote Standort kommuniziert direkt mit dem Verbund Server Proxy, um ein Token zu generieren und sich bei der Anwendung oder dem Dienst zu authentifizieren.

Nach Durchlesen der Informationen in den verknüpften Themen können Sie anhand der Schritte in [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)mit der Umsetzung dieses Bereitstellungsziels beginnen.

Die folgende Abbildung zeigt die einzelnen erforderlichen Komponenten für dieses AD FS Bereitstellungs Ziel.

![Zugriff auf Ihre apps](media/50af4837-31e0-451f-a942-e705c2300065.gif)

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
