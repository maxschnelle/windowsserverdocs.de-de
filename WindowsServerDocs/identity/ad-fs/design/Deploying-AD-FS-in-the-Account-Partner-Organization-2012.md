---
ms.assetid: 9aaca9c5-ce44-495c-aad6-61aede87a83f
title: Bereitstellen von AD FS in der Kontopartnerorganisation
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3a668659f375f7fe96d676e7018e9e9315e35be5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814441"
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>Bereitstellen von AD FS in der Kontopartnerorganisation

>Gilt für: Windows Server 2012

Kontopartner in Active Directory Federation Services \(AD FS\) stellt die Organisation in der verbundvertrauensstellung, die physisch Benutzerkonten in einem unterstützten Attributspeicher speichert dar. Weitere Informationen zu den unterstützten attributspeichern finden Sie unter [The Role of Attribute Stores](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).  
  
Der Verbundserver in der Kontopartnerorganisation authentifiziert lokale Benutzer und erstellt Sicherheitstoken, die vom Ressourcenpartner für Entscheidungen für die Autorisierung verwendet werden. Vertrauende Seiten wie Websites und Webdienste können dann einfach registrieren sich mit den Verbundserver und ausgestellte Token für die Authentifizierung und Zugriffssteuerung.  
  
In Szenarien, in denen Sie Ihren Benutzern den Zugriff auf mehrere verbundanwendungen oder-Dienste bereitstellen müssen, wenn jede Anwendung oder ein Dienst von einer anderen Organisation gehostet wird, konfigurieren Sie die Konto-Partnerverbundserver, sodass Sie bereitstellen können mehrere vertrauende Seiten.  
  
Weitere Informationen über das Einrichten und Konfigurieren von kontopartnerorganisationen finden Sie unter [Prüfliste: Konfigurieren der Kontopartnerorganisation](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md).  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Überprüfen der Rolle des Verbundservers beim Kontopartner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [Überprüfen Sie die Rolle des Verbundserverproxys beim Kontopartner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [Vorbereiten von Clientcomputern des Kontopartners](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
