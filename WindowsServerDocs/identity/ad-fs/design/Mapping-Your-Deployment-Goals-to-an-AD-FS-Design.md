---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: Zuordnen der Bereitstellungsziele zu einem AD FS-Entwurf
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 048bce75c52895b2d9e215bdccef9cb13dc23533
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>Zuordnen der Bereitstellungsziele zu einem AD FS-Entwurf

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nachdem Sie die Überprüfung der vorhandenen Active Directory Federation Services \(AD FS\) Bereitstellungsziele abgeschlossen haben, und Sie bestimmen, welche Ziele im Zusammenhang mit der Bereitstellung, können Sie diese Ziele einem bestimmten AD FS-Entwurf zuordnen. Weitere Informationen zu AD FS-Bereitstellungsziele vordefinierte, finden Sie unter [Identifizieren der AD FS-Bereitstellungsziele](Identifying-Your-AD-FS-Deployment-Goals.md).  
  
Verwenden Sie in der folgende Tabelle, um zu bestimmen, welche AD FS-Entwurfs, der Kombination von AD FS-Bereitstellungsziele für Ihre Organisation zugeordnet ist. In dieser Tabelle bezieht sich nur auf die zwei primären AD FS-Entwürfe, wie in diesem Handbuch beschrieben. Sie jedoch können einen Hybriden oder benutzerdefinierten AD FS-Entwurf erstellen, mit einer beliebigen Kombination der AD FS-Bereitstellungsziele den Bedürfnissen Ihrer Organisation.  
  
|AD FS-Bereitstellungsziele|[Web-SSO-Entwurf](Web-SSO-Design.md)|[Federated-Web-SSO-Entwurf](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[Bereitstellen der Active Directory-Benutzern den Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|Nein|Ja, im Kontopartner|  
|[Bereitstellen der Active Directory-Benutzern den Zugriff auf die Anwendungen und Dienste anderer Organisationen](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|Nein|Nein, optional im Kontopartner|  
|[Bieten Sie Benutzern in einer anderen Organisationszugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|Ja|Ja|  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

