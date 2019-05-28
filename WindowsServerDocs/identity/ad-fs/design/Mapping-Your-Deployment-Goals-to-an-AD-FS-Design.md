---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: Zuordnen der Bereitstellungsziele zu einem AD FS-Entwurf
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13d8ae8b8f3e4c8160f61284e5fb97e21b6a51b6
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191249"
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>Zuordnen der Bereitstellungsziele zu einem AD FS-Entwurf


Nach Abschluss der Überprüfung der vorhandenen Active Directory Federation Services \(AD FS\) Bereitstellungsziele und Sie bestimmen, welche Ziele für Ihre Bereitstellung in Beziehung stehen, können Sie diese Ziele einem bestimmten AD FS-Entwurf zuordnen. Weitere Informationen zu AD FS-Bereitstellungsziele vordefinierte, finden Sie unter [Identifizieren der AD FS-Bereitstellungsziele](Identifying-Your-AD-FS-Deployment-Goals.md).  
  
Verwenden Sie in der folgende Tabelle, um zu bestimmen, welcher AD FS-Entwurfs die geeignete Kombination von AD FS-Bereitstellungsziele Ihrer Organisation zugeordnet. In dieser Tabelle bezieht sich nur auf die zwei primären AD FS-Entwürfe, wie in diesem Handbuch beschrieben. Allerdings können Sie einer Hybrid- oder benutzerdefinierte AD FS-Entwurf erstellen, durch eine beliebige Kombination aus den AD FS-Bereitstellungsziele verwenden, um die Anforderungen Ihrer Organisation erfüllen.  
  
|Ziel für AD FS-Bereitstellung|[Web-SSO-Entwurf](Web-SSO-Design.md)|[Federated-Web-SSO-Entwurf](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|Nein|Ja, im Kontopartner|  
|[Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|Nein|Nein, optional im Kontopartner|  
|[Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für die Benutzer anderer Organisationen](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|Ja|Ja|  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

