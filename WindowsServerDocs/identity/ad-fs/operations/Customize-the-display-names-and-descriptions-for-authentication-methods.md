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
ms.openlocfilehash: 699622a8a075dd6c78ab1b536dce2abfee642e9e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855191"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>Anpassen der Anzeigenamen und Beschreibungen für Authentifizierungsmethoden 

>Gilt für: Windows Server 2016, Windows Server 2012 R2

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
