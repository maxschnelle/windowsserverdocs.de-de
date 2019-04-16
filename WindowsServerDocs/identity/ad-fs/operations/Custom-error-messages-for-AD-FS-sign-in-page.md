---
ms.assetid: 1df78c2a-5054-4b54-8310-c48ea62e6e0b
title: "Benutzerdefinierte Fehlermeldungen für AD FS-Anmeldeseite"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3a015c27f784d5b1f488f984450612820d4a06b1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="custom-error-messages-for-ad-fs-sign-in-page"></a>Benutzerdefinierte Fehlermeldungen für AD FS-Anmeldeseite  

>Gilt für: Windows Server 2016, Windows Server2012 R2

Sie können benutzerdefinierte Fehlermeldungen, die angepasst werden können in Ihrer Organisation konfigurieren. Die folgende Abbildungzeigt eine benutzerdefinierte fehlerseitenbeschreibung und eine allgemeine Fehlermeldung an. Verwenden Sie die folgenden Windows PowerShell-Cmdlets zum Anpassen von Fehlermeldungen.  
  
![Benutzerdefinierte Fehler](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom3.png)  
  
## <a name="customize-the-error-page-description"></a>Anpassen der fehlerseitenbeschreibung  
Verwenden Sie zum Anpassen der fehlerseitenbeschreibung das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  

`Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" ` 

  
## <a name="customize-a-generic-error-message"></a>Anpassen einer generischen Fehlermeldung  
Verwenden Sie zum Anpassen der generischen Fehlermeldung das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageGenericErrorMessage "This is a generic error message.  Contact Contoso IT for assistance." ` 

  
## <a name="customize-an-authorization-error-message"></a>Anpassen einer autorisierungsfehlermeldung  
Verwenden Sie zum Anpassen der autorisierungsfehlermeldung das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  

    Set-AdfsGlobalWebContent -ErrorPageAuthorizationErrorMessage "You have received an Authorization error.  Contact Contoso IT for assistance."  

  
## <a name="customize-a-device-authentication-error-message"></a>Anpassen einer Fehlermeldung zur Geräteauthentifizierung  
Verwenden Sie zum Anpassen der Fehlermeldung zur Geräteauthentifizierung das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageDeviceAuthenticationErrorMessage "Your device is not authorized.  Contact Contoso IT for assistance."`  
 
  
## <a name="customize-a-support-email-error-message"></a>Anpassen einer Fehlermeldung für Support-E-Mail  
Sie können eine E-Mail-Adresse für Unterstützung in AD FS konfigurieren. Wenn konfiguriert, wird AD FS automatisch einen Link für Endbenutzer die Fehlerdetails per E-Mail gesendet.  
  
Verwenden Sie zum Anpassen der Fehlermeldung die Support-E-Mail das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  

    Set-AdfsGlobalWebContent -ErrorPageSupportEmail  "admin@contoso.com"  

  
## <a name="customize-a-relying-party-authorization-message"></a>Passen Sie die Meldung ein der vertrauenden Seite zur Autorisierung  
Sie können eine der vertrauenden Seite Meldung zur Autorisierung in AD FS konfigurieren.  
  
Verwenden Sie zum Anpassen der relying Party-Fehlermeldung das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  

    Set-AdfsRelyingPartyWebContent -Name fedpassive -ErrorPageAuthorizationErrorMessage "<p> You need to be a member of Security Auditors to access this site. Click <A href='http://accessrequest/'>here</A> for more information.</p>“  


## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)    
