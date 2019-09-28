---
ms.assetid: 9aaca9c5-ce44-495c-aad6-61aede87a83f
title: Bereitstellen von AD FS in der Kontopartnerorganisation
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 62d7549f124b96cd7addf7e54cc5d0c1d9897098
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408123"
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>Bereitstellen von AD FS in der Kontopartnerorganisation

Ein Konto Partner in Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 stellt die Organisation in der Verbund Vertrauensstellung dar, die Benutzerkonten physisch in einem unterstützten Attribut Speicher speichert. Weitere Informationen zu den unterstützten Attribut speichern finden Sie unter [der Rolle von Attribut speichern](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).  
  
Der Verbund Server in der Konto Partnerorganisation authentifiziert lokale Benutzer und erstellt Sicherheits Token, die vom Ressourcen Partner verwendet werden, um Autorisierungs Entscheidungen zu treffen. Vertrauende Seiten wie Websites und Webdienste können sich dann problemlos beim Verbund Server registrieren und ausgestellte Token für die Authentifizierung und Zugriffs Steuerung nutzen.  
  
In Szenarien, in denen Sie Ihren Benutzern Zugriff auf mehrere Verbund Anwendungen oder-Dienste gewähren müssen – wenn jede Anwendung oder jeder Dienst von einer anderen Organisation gehostet wird – können Sie den Konto Partner Verbund Server so konfigurieren, dass Sie mehrere vertrauende Seiten.  
  
Weitere Informationen zum Einrichten und Konfigurieren von Konto Partnerorganisationen finden Sie unter [checkliste: Konfigurieren der Konto Partner Organisation @ no__t-0.  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Überprüfen der Rolle des Verbundservers beim Kontopartner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [Überprüfen der Rolle des Verbundserverproxys beim Kontopartner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [Vorbereiten von Client Computern im Konto Partner](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
