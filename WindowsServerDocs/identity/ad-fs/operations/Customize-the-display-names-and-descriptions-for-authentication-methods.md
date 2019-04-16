---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: "Anpassen der Anzeigenamen und Beschreibungen für Authentifizierungsmethoden"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 699622a8a075dd6c78ab1b536dce2abfee642e9e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>Anpassen der Anzeigenamen und Beschreibungen für Authentifizierungsmethoden 

>Gilt für: Windows Server 2016, Windows Server2012 R2

Anpassen der Anzeigenamen und Beschreibungen für Authentifizierungsmethoden können Sie die `Set-AdfsAuthenticationProviderWebContent`PowerShell-Cmdlet.  Um dieses Cmdlet verwenden, benötigen Sie zunächst den Namen der Authentifizierungsmethode, die Sie anpassen möchten.  Dies kann mit `Get-AdfsGlobalAuthenticationPolicy`.  Im folgenden Beispiel wir sehen, dass auf unsere Anmeldeseite Folgendes angezeigt: "Melden Sie sich mit einem x. 509-Zertifikat".  Wir möchten dies für die Benutzer zu vereinfachen.  
  
![Displayname anpassen](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)  
  
Daher zuerst erhalten wir den Namen der Authentifizierungsmethode, und bearbeiten dann den angezeigten Text.  
  
 
    Get-AdfsGlobalAuthenticationPolicy  
      
    AdditionalAuthenticationProvider  : {}  
    DeviceAuthenticationEnabled   : False  
    PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    WindowsIntegratedFallbackEnabled  : True  
      
    Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"  
  
  
![Displayname anpassen](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)  
  
Jetzt sehen wir, dass die angezeigte Meldung geändert hat.  
  
![Displayname anpassen](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md) 
