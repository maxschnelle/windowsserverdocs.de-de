---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: Planen Ihrer Bereitstellung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 9ada8872c7d74e4a0a10504ffaf34a235536dcbb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954316"
---
# <a name="planning-your-deployment"></a>Planen Ihrer Bereitstellung

Wenn Sie eine Verbund übergreifende \- Verbund \( \- basierte \) Zusammenarbeit mit Active Directory-Verbunddienste (AD FS) \( AD FS planen, müssen Sie \) zuerst feststellen, ob Ihre Organisation eine Webressource hostet, auf die von anderen Organisationen über das Internet zugegriffen werden soll, oder ob Sie Zugriff auf die Webressourcen für Mitarbeiter in Ihrer Organisation bereitstellen. Diese Bestimmung wirkt sich darauf aus, wie Sie AD FS bereitstellen, und ist für die Planung Ihrer AD FS-Infrastruktur von grundlegender Bedeutung.

> [!NOTE]
> Stellen Sie sicher, dass alle Parteien eindeutig verstehen, welche Rolle die Organisation in der Verbundvereinbarung spielt.

Für den [Federated-Web-SSO-Entwurf](Federated-Web-SSO-Design.md)verwendet AD FS Bedingungen wie z. b. den *Konto Partner* , \( der im Snap-in AD FS Verwaltung auch als *Identitäts Anbieter* bezeichnet wird, sowie den \- \) *Ressourcen Partner* , der \( im Snap-in AD FS Verwaltung auch als vertrauende *Seite* bezeichnet wird, \- \) um die Organisation zu unterscheiden, die die Konten \( des Konto Partners \) von der Organisation \- \( \) hostet, die den Ressourcen Partner

Beim [Web SSO Design](Web-SSO-Design.md)übernimmt die Organisation sowohl die Kontopartnerrolle als auch die Ressourcenpartnerrolle, da die Organisation den eigenen Benutzern Zugriff auf ihre Anwendungen gewährt.

In den folgenden Themen werden einige der AD FS Partner Organisationskonzepte erläutert. Sie enthalten auch Links zu Themen im AD FS Bereitstellungs Handbuch, die Informationen zum Einrichten und Konfigurieren von Konto Partnerorganisationen und Ressourcen Partnerorganisationen auf Grundlage Ihrer AD FS Bereitstellungs Ziele enthalten.

## <a name="in-this-section"></a>In diesem Abschnitt

-   [Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)

-   [Planen der Interoperabilität mit AD FS 1.x](Planning-for-Interoperability-with-AD-FS-1.x.md)

-   [Verwendungszwecke der Identitäts Delegierung](When-to-Use-Identity-Delegation.md)

-   [Bereitstellen von AD FS in der Kontopartnerorganisation](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)

-   [Bereitstellen von AD FS in der Ressourcenpartnerorganisation](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)


