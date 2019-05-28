---
ms.assetid: 1df78c2a-5054-4b54-8310-c48ea62e6e0b
title: Benutzerdefinierte Fehlermeldungen für AD FS-Anmeldeseite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8bcc653cc9eb9adb6d31331463d01774d4faec1a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189220"
---
# <a name="custom-error-messages-for-ad-fs-sign-in-page"></a>Benutzerdefinierte Fehlermeldungen für AD FS-Anmeldeseite  


Sie können benutzerdefinierte Fehlermeldungen konfigurieren, die auf Ihre Organisation zugeschnitten sind. In der folgenden Abbildung sind eine benutzerdefinierte Fehlerseitenbeschreibung und eine generische Fehlermeldung gezeigt. Verwenden Sie die folgenden Windows PowerShell-Cmdlets, um das Anpassen von Fehlermeldungen.  
  
![benutzerdefinierte Fehler](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom3.png)  
  
## <a name="customize-the-error-page-description"></a>Anpassen der Fehlerseitenbeschreibung  
Verwenden Sie zum Anpassen der fehlerseitenbeschreibung das folgende Windows PowerShell-Cmdlet und die Syntax.  
  

`Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" ` 

  
## <a name="customize-a-generic-error-message"></a>Anpassen einer generischen Fehlermeldung  
Verwenden Sie zum Anpassen der generischen Fehlermeldung der folgenden Windows PowerShell-Cmdlets und Syntax ein.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageGenericErrorMessage "This is a generic error message.  Contact Contoso IT for assistance." ` 

  
## <a name="customize-an-authorization-error-message"></a>Anpassen einer Autorisierungsfehlermeldung  
Verwenden Sie zum Anpassen der autorisierungsfehlermeldung das folgende Windows PowerShell-Cmdlet und die Syntax.  
  

    Set-AdfsGlobalWebContent -ErrorPageAuthorizationErrorMessage "You have received an Authorization error.  Contact Contoso IT for assistance."  

  
## <a name="customize-a-device-authentication-error-message"></a>Anpassen einer Fehlermeldung zur Geräteauthentifizierung  
Verwenden Sie zum Anpassen der Fehlermeldung zur Geräteauthentifizierung das folgende Windows PowerShell-Cmdlet und die Syntax.  
  
 
`Set-AdfsGlobalWebContent -ErrorPageDeviceAuthenticationErrorMessage "Your device is not authorized.  Contact Contoso IT for assistance."`  
 
  
## <a name="customize-a-support-email-error-message"></a>Anpassen einer Fehlermeldung zu einer Support-E-Mail  
Sie können eine Support-e-Mail-Adresse in AD FS konfigurieren. Wenn konfiguriert haben, zeigt die AD FS automatisch eine Verknüpfung für die Endbenutzer die Fehlerdetails per e-Mail zu senden.  
  
Verwenden Sie zum Anpassen der Support-e-Mail-Fehlermeldung der folgenden Windows PowerShell-Cmdlets und Syntax ein.  
  

    Set-AdfsGlobalWebContent -ErrorPageSupportEmail  "admin@contoso.com"  

  
## <a name="customize-a-relying-party-authorization-message"></a>Anpassung einer Meldung zur Autorisierung der vertrauenden Seite  
Sie können eine Fehlermeldung zur vertrauenden Seite Autorisierung in AD FS konfigurieren.  
  
Verwenden Sie zum Anpassen der Fehlermeldung der vertrauenden Seite, die folgenden Windows PowerShell-Cmdlets und Syntax.  

    Set-AdfsRelyingPartyWebContent -Name fedpassive -ErrorPageAuthorizationErrorMessage "<p> You need to be a member of Security Auditors to access this site. Click <A href='http://accessrequest/'>here</A> for more information.</p>“  


## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)    
