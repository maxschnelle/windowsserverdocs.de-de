---
ms.assetid: bb9b9e18-bf2f-4115-be77-9a165944db41
title: Planen Ihrer Bereitstellung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5c7cec9ad92605f3dc98f8ce8fb7853a7ae61299
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863691"
---
# <a name="planning-your-deployment"></a>Planen Ihrer Bereitstellung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beim Planen plattformübergreifende\-Organisation \(Verbund\-basierend\) Zusammenarbeit mithilfe von Active Directory Federation Services \(AD FS\), zuerst zu bestimmen, ob Ihre Organisation Hosten eine Webressource, die von anderen Organisationen, die über das Internet zugegriffen werden soll, oder wenn Sie den Zugriff auf die Webressource für Mitarbeiter in Ihrer Organisation bereitstellen. Diese Entscheidung wirkt sich auf, wie Sie AD FS bereitstellen, und es ist überaus wichtig, bei der Planung der AD FS-Infrastruktur.  
  
> [!NOTE]  
> Stellen Sie sicher, dass alle Parteien eindeutig verstehen, welche Rolle die Organisation in der Verbundvereinbarung spielt.  
  
Für die [Federated Web SSO Design](Federated-Web-SSO-Design.md), AD FS werden Begriffe verwendet, z. B. *Kontopartner* \(so genannte *Identitätsanbieter* im AD FS-Verwaltungs-Snap-\-in\) und *Ressourcenpartner* \(so genannte *vertrauende* im AD FS-Verwaltungs-Snap-\-in\) auf erleichtern die Unterscheidung von der Organisationsstatus, die die Konten hostet \(Kontopartner\) aus der Organisation, die im Web gehostet\-Ressourcen \(Ressourcenpartner\).  
  
Beim [Web SSO Design](Web-SSO-Design.md)übernimmt die Organisation sowohl die Kontopartnerrolle als auch die Ressourcenpartnerrolle, da die Organisation den eigenen Benutzern Zugriff auf ihre Anwendungen gewährt.  
  
Die folgenden Themen wird erläutert, dass einige der AD FS erläutert partner. Es enthält auch Links zu Themen im Bereitstellungshandbuch für AD FS, die Informationen über das Einrichten und Konfigurieren von Konto- und ressourcenpartnerorganisationen basierend auf der AD FS-Bereitstellungsziele enthalten.  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)  
  
-   [Planen der Interoperabilität mit AD FS 1.x](Planning-for-Interoperability-with-AD-FS-1.x.md)  
  
-   [Verwenden Sie die Identitätsdelegierung](When-to-Use-Identity-Delegation.md)  
  
-   [Bereitstellen von AD FS in der Kontopartnerorganisation](Deploying-AD-FS-in-the-Account-Partner-Organization-2012.md)  
  
-   [Bereitstellen von AD FS in der Ressourcenpartnerorganisation](Deploying-AD-FS-in-the-Resource-Partner-Organization-2012.md)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)


