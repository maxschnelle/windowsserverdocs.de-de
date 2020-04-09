---
ms.assetid: 1df78c2a-5054-4b54-8310-c48ea62e6e0b
title: Benutzerdefinierte Fehlermeldungen für AD FS Anmeldeseite
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 31da3e65e69910817a78ab1007e897fb5a9ad683
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816433"
---
# <a name="custom-error-messages-for-ad-fs-sign-in-page"></a>Benutzerdefinierte Fehlermeldungen für AD FS Anmeldeseite  


Sie können benutzerdefinierte Fehlermeldungen konfigurieren, die auf Ihre Organisation zugeschnitten sind. In der folgenden Abbildung sind eine benutzerdefinierte Fehlerseitenbeschreibung und eine generische Fehlermeldung gezeigt. Verwenden Sie die folgenden Windows PowerShell-Cmdlets zum Anpassen der Fehlermeldungen.  
  
![benutzerdefinierter Fehler](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom3.png)  
  
## <a name="customize-the-error-page-description"></a>Anpassen der Fehlerseitenbeschreibung  
Verwenden Sie zum Anpassen der Fehlerseiten Beschreibung das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  

`Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" ` 

  
## <a name="customize-a-generic-error-message"></a>Anpassen einer generischen Fehlermeldung  
Verwenden Sie zum Anpassen der generischen Fehlermeldung das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageGenericErrorMessage "This is a generic error message.  Contact Contoso IT for assistance." ` 

  
## <a name="customize-an-authorization-error-message"></a>Anpassen einer Autorisierungsfehlermeldung  
Verwenden Sie zum Anpassen der Autorisierungs Fehlermeldung das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  

    Set-AdfsGlobalWebContent -ErrorPageAuthorizationErrorMessage "You have received an Authorization error.  Contact Contoso IT for assistance."  

  
## <a name="customize-a-device-authentication-error-message"></a>Anpassen einer Fehlermeldung zur Geräteauthentifizierung  
Verwenden Sie zum Anpassen der Fehlermeldung zur Geräte Authentifizierung das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageDeviceAuthenticationErrorMessage "Your device is not authorized.  Contact Contoso IT for assistance."`  
 
  
## <a name="customize-a-support-email-error-message"></a>Anpassen einer Fehlermeldung zu einer Support-E-Mail  
Sie können eine Support-e-Mail-Adresse in AD FS konfigurieren. Bei der Konfiguration zeigt AD FS automatisch einen Link an, mit dem Endbenutzer die Fehlerdetails per e-Mail senden können.  
  
Verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax, um die Support-e-Mail-Fehlermeldung anzupassen.  
  

    Set-AdfsGlobalWebContent -ErrorPageSupportEmail  "admin@contoso.com"  

  
## <a name="customize-a-relying-party-authorization-message"></a>Anpassung einer Meldung zur Autorisierung der vertrauenden Seite  
Sie können eine Fehlermeldung zur Autorisierung der vertrauenden Seite in AD FS konfigurieren.  
  
Verwenden Sie zum Anpassen der Fehlermeldung der vertrauenden Seite das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  

    Set-AdfsRelyingPartyWebContent -Name fedpassive -ErrorPageAuthorizationErrorMessage "<p> You need to be a member of Security Auditors to access this site. Click <A href='http://accessrequest/'>here</A> for more information.</p>"  


## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)    
