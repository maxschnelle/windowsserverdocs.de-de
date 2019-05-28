---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: Anpassen der Anzeigenamen und Beschreibungen für Authentifizierungsmethoden
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b9702873d42e0a72e510ac022d8d7fb04b45dab9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189171"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>Anpassen der Anzeigenamen und Beschreibungen für Authentifizierungsmethoden 


Sie können zum Anpassen der Anzeigenamen und Beschreibungen für die Authentifizierungsmethoden das PowerShell-Cmdlet `Set-AdfsAuthenticationProviderWebContent` verwenden.  Um dieses Cmdlet verwenden zu können, benötigen Sie zunächst den Namen der Authentifizierungsmethode, die Sie anpassen möchten.  Verwenden Sie hierzu `Get-AdfsGlobalAuthenticationPolicy`.  Im folgenden Beispiel sehen Sie, dass unsere anmelden\-auf der Seite wird Folgendes angezeigt:  „Sign in using an X.509 certificate.“  Wir möchten dies für die Benutzer vereinfachen.  
  
![Anpassen von "DisplayName"](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)  
  
Wir rufen zuerst den Namen der Authentifizierungsmethode ab und bearbeiten dann den angezeigten Text.  
  
 
    Get-AdfsGlobalAuthenticationPolicy  
      
    AdditionalAuthenticationProvider  : {}  
    DeviceAuthenticationEnabled   : False  
    PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    WindowsIntegratedFallbackEnabled  : True  
      
    Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"  
  
  
![Anpassen von "DisplayName"](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)  
  
Wie Sie sehen, hat sich die angezeigte Meldung geändert.  
  
![Anpassen von "DisplayName"](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md) 
