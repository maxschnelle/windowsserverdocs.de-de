---
ms.assetid: 41d6b897-1e72-4522-aad6-eece1154a154
title: Bereitstellen von AD FS in der Ressourcenpartnerorganisation
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4a556c07e7d6e0bec4c947ea9d1a75eef9964cef
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-ad-fs-in-the-resource-partner-organization"></a>Bereitstellen von AD FS in der Ressourcenpartnerorganisation

>Gilt für: Windows Server 2016, Windows Server2012 R2

Der Ressourcenpartnerorganisation in Active Directory Federation Services \(AD FS\) steht für die Organisation, deren Webserver durch Resource\ clientseitigen Verbundserver geschützt werden können. Der Verbundserver an den Ressourcenpartner verwendet die Sicherheitstoken, die der Kontopartner Ansprüche an den Webserver bereitstellen, die beim Ressourcenpartner befinden erzeugt werden.  
  
In Szenarien, in denen Sie Zugriff auf verbundene Dienste oder Anwendungen für viele verschiedene Benutzer bereitstellen müssen, wenn einige Benutzer in verschiedenen Organisationen befinden – Sie können den Ressourcenverbundserver konfigurieren, sodass Sie mehrere Kontopartner bereitstellen können.  
  
Weitere Informationen zum Einrichten und Konfigurieren der Ressourcenpartnerorganisation finden Sie unter [Prüfliste: Konfigurieren der Ressourcenpartnerorganisation](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Überprüfen der Rolle des Verbundservers beim Ressourcenpartner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)  
  
-   [Review the Role of the Federation Serverproxy in the Resource Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)  
  
-   [Bestimmen der Verbundanwendungsstrategie im Ressourcenpartner](Determine-Your-Federated-Application-Strategy-in-the-Resource-Partner.md)  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
