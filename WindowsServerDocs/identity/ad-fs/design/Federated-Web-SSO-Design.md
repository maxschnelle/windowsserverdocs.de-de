---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: Federated-Web-SSO – Entwurf
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: f3f34aca7f7a316ff714b88209e3bf81de420ecb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942764"
---
# <a name="federated-web-sso-design"></a>Federated-Web-SSO – Entwurf

Der Entwurf für einmaliges Anmelden mit Verbund \- \- \( \) -SSO in Active Directory-Verbunddienste (AD FS) \( AD FS \) umfasst eine sichere Kommunikation, die mehrere Firewalls, Umkreis Netzwerke und namens \- Auflösungs Server umfasst – zusätzlich zur gesamten Internet Routing Infrastruktur.

Dieser Entwurf wird in der Regel verwendet, wenn zwei Organisationen eine Verbund Vertrauensstellung erstellen, damit Benutzer in einer Organisation \( der Konto Partnerorganisation \) auf webbasierte \- Anwendungen oder Dienste zugreifen können, die durch AD FS in der anderen Organisation \( der Ressourcen Partnerorganisation geschützt sind \) .

Anders ausgedrückt: eine Verbund Vertrauensstellung ist die Verkörperung einer Vereinbarung zum Geschäfts \- Level oder einer Partnerschaft zwischen zwei Organisationen. Wie in der folgenden Abbildung gezeigt, können Sie eine Verbund Vertrauensstellung zwischen zwei Unternehmen einrichten, die zu einem End-to-End-Verbund \- \- Szenario führt.

![Verbund-Web-SSO](media/adfs2_FederatedWebSSODesign.gif)

Der unidirektionale \- Pfeil in der Abbildung gibt die Richtung der Verbund Vertrauensstellung an, die – wie die Richtung von Windows-Vertrauens Stellungen – stets auf die Kontoseite der Gesamtstruktur zeigt. Dies bedeutet, dass die Authentifizierung von der Kontopartnerorganisation zur Ressourcenpartnerorganisation verläuft.

In diesem Federated-Web-SSO-Entwurf leiten zwei Verbund Server \( in Fabrikam und der andere in "" von "" von "" von "" die \) Authentifizierungsanforderungen von Benutzerkonten in Fabrikam zu \- webbasierten Anwendungen oder Diensten in "Configuration Manager" weiter.

> [!NOTE]
> Zur zusätzlichen Sicherheit können Sie Verbund Server Proxys verwenden, um Anforderungen an Verbund Server weiterzuleiten, auf die nicht direkt über das Internet zugegriffen werden kann.

In diesem Beispiel ist Fabrikam der Identitäts- bzw. Kontoanbieter. Der Fabrikam-Teil des Entwurfs "Federated-Web-SSO" verwendet das folgende AD FS Bereitstellungs Ziel:

-   [Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)

Contoso ist der Ressourcenanbieter. Der Teil "" von "Federated-Web-SSO" erreicht die folgenden AD FS Bereitstellungs Ziele:

-   [Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für die Benutzer anderer Organisationen](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)

-   [Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)

Eine detaillierte Liste der Aufgaben, die Sie zum Planen und Bereitstellen des Entwurfs "Federated-Web-SSO" verwenden können, finden Sie unter [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md).

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
