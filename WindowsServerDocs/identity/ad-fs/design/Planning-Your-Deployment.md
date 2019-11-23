---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: Planen Ihrer Bereitstellung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 607dc34c8f44d8d96a8dc0c9d1ed004edc799167
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407992"
---
# <a name="planning-your-deployment"></a>Planen Ihrer Bereitstellung

Wenn Sie für Cross\-Organization \(Verbund\-basierend\) Zusammenarbeit mithilfe Active Directory-Verbunddienste (AD FS) \(AD FS\)planen, müssen Sie zunächst feststellen, ob Ihre Organisation eine Webressource hostet, auf die von anderen Organisationen über das Internet zugegriffen werden soll, oder ob Sie Zugriff auf die Webressourcen für Mitarbeiter in Ihrer Organisation bereitstellen. Diese Bestimmung wirkt sich darauf aus, wie Sie AD FS bereitstellen, und ist für die Planung Ihrer AD FS-Infrastruktur von grundlegender Bedeutung.  
  
> [!NOTE]  
> Stellen Sie sicher, dass alle Parteien eindeutig verstehen, welche Rolle die Organisation in der Verbundvereinbarung spielt.  
  
Für den [Federated-Web-SSO-Entwurf](Federated-Web-SSO-Design.md)verwendet AD FS Bedingungen wie z. b. den *Konto Partner* \(auch als *Identitäts Anbieter* im AD FS Verwaltungs-Snap\-in\) und *Ressourcen Partner* \(auch als vertrauende *Seite* im AD FS Verwaltungs-Snap-in\-bezeichnet, um die Organisation zu unterscheiden, die die Konten\) dem Konto Partner \(der Organisation hostet\) der Ressourcen Partner\).\-\(  
  
Beim [Web SSO Design](Web-SSO-Design.md)übernimmt die Organisation sowohl die Kontopartnerrolle als auch die Ressourcenpartnerrolle, da die Organisation den eigenen Benutzern Zugriff auf ihre Anwendungen gewährt.  
  
In den folgenden Themen werden einige der AD FS Partner Organisationskonzepte erläutert. Sie enthalten auch Links zu Themen im AD FS Bereitstellungs Handbuch, die Informationen zum Einrichten und Konfigurieren von Konto Partnerorganisationen und Ressourcen Partnerorganisationen auf Grundlage Ihrer AD FS Bereitstellungs Ziele enthalten.  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)  
  
-   [Planen der Interoperabilität mit AD FS 1.x](Planning-for-Interoperability-with-AD-FS-1.x.md)  
  
-   [Verwendungszwecke der Identitäts Delegierung](When-to-Use-Identity-Delegation.md)  
  
-   [Bereitstellen von AD FS in der Kontopartnerorganisation](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)  
  
-   [Bereitstellen von AD FS in der Ressourcenpartnerorganisation](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)


