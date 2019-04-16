---
ms.assetid: 8c3536b7-d091-4ee6-ad04-24713f070862
title: Bereitstellen von AD FS in der Kontopartnerorganisation
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5b4ba00aa9fed1022d9c0137d05ac6240b44b276
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>Bereitstellen von AD FS in der Kontopartnerorganisation

>Gilt für: Windows Server 2016, Windows Server2012 R2

Kontopartner in Active Directory Federation Services \(AD FS\) steht für die Organisation in der verbundvertrauensstellung, die physisch Benutzerkonten in einem unterstützten Attributspeicher gespeichert werden. Weitere Informationen zu den Stores unterstützt werden, finden Sie unter [The Role of Attribute Stores](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).  
  
Der Verbundserver in der Kontopartnerorganisation authentifiziert lokale Benutzer und erstellt Sicherheitstoken, die vom Ressourcenpartner für Entscheidungen für die Autorisierung verwendet werden. Vertrauende Seiten ausgestellte wie Websites und Webdienste werden dann einfach registrieren sich mit den Verbundserver und verarbeiten können Token für die Authentifizierung und Zugriffssteuerung.  
  
In Szenarien, in denen Sie Ihre Benutzer mit Zugriff auf mehrere verbundanwendungen oder -Dienste bereitstellen müssen, wenn jede Anwendung oder ein Dienst von einer anderen Organisation gehostet wird, können Sie der Kontoverbundserver Partner konfigurieren, sodass Sie mehrere vertrauende Seiten bereitstellen können.  
  
Weitere Informationen zum Einrichten und Konfigurieren von kontopartnerorganisationen finden Sie unter [Prüfliste: Konfigurieren der Kontopartnerorganisation](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Überprüfen der Rolle des Verbundservers beim Kontopartner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [Review the Role of the Federation Serverproxy in the Account Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [Vorbereiten von Clientcomputern des Kontopartners](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
