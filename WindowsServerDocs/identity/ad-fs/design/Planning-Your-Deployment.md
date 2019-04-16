---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: Planen der Bereitstellung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5c7cec9ad92605f3dc98f8ce8fb7853a7ae61299
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="planning-your-deployment"></a>Planen der Bereitstellung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Sie Cross\ organisationsübergreifende \(federation\-based\) Zusammenarbeit mithilfe von Active Directory Federation Services \(AD FS\) planen, ermitteln Sie zunächst, wenn Ihre Organisation eine Webressource von anderen Organisationen über das Internet zugegriffen werden gehostet wird, oder wenn Sie den Zugriff auf die Webressource für Mitarbeiter in Ihrer Organisation bereitstellen werden. Dies wirkt sich wie für die Bereitstellung von AD FS, und es ist wesentlich bei der Planung der AD FS-Infrastruktur.  
  
> [!NOTE]  
> Stellen Sie sicher, dass die Rolle, die Organisation in der verbundvereinbarung spielt alle Parteien eindeutig angesehen wird.  
  
Für die [Federated Web SSO Design](Federated-Web-SSO-Design.md), AD FS verwendet Begriffe wie z.B. *Kontopartner* \ (auch bezeichnet als *Identitätsanbieter* in der AD FS-Verwaltungs-Snap-Taste) und *Ressourcenpartner* \ (auch bezeichnet als *vertrauende* in der AD FS-Verwaltungs-Snap-Taste) um die Organisation zu unterscheiden, die die Konten hostet \(the account Partner\) aus der Organisation, die die webbasierten Ressourcen hostet \(the resource Partner\).  
  
In der [Web-SSO-Entwurf](Web-SSO-Design.md), die Organisation fungiert in sowohl das Konto Partner auch die Ressourcenpartnerrolle, da es die Benutzer mit Zugriff auf ihre Anwendungen bereitstellt.  
  
Die folgenden Themen wird erläutert, dass einige der AD FS Organisation Konzepte Partner. Sie enthalten auch Links zu Themen im Bereitstellungshandbuch für AD FS, die Informationen zum Einrichten und Konfigurieren von Konto- und ressourcenpartnerorganisationen basierend auf der AD FS-Bereitstellungsziele enthalten.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)  
  
-   [Planen der Interoperabilität mit AD FS 1.x](Planning-for-Interoperability-with-AD-FS-1.x.md)  
  
-   [Wenn für Identitätsdelegierung](When-to-Use-Identity-Delegation.md)  
  
-   [Bereitstellen von AD FS in der Kontopartnerorganisation](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)  
  
-   [Bereitstellen von AD FS in der Ressourcenpartnerorganisation](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)


