---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: Anpassen von anzeigen Amen und Beschreibungen für Authentifizierungsmethoden
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cc0da10858ca6924a516fbf825206e376294209d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407567"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>Anpassen von anzeigen Amen und Beschreibungen für Authentifizierungsmethoden 


Sie können zum Anpassen der Anzeigenamen und Beschreibungen für die Authentifizierungsmethoden das PowerShell-Cmdlet `Set-AdfsAuthenticationProviderWebContent` verwenden.  Um dieses Cmdlet verwenden zu können, benötigen Sie zunächst den Namen der Authentifizierungsmethode, die Sie anpassen möchten.  Verwenden Sie hierzu `Get-AdfsGlobalAuthenticationPolicy`.  Im folgenden Beispiel sehen Sie, dass auf der Seite Sign @ no__t-0in Folgendes angezeigt wird:  „Sign in using an X.509 certificate.“  Wir möchten dies für die Benutzer vereinfachen.  
  
![Display Name anpassen](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)  
  
Wir rufen zuerst den Namen der Authentifizierungsmethode ab und bearbeiten dann den angezeigten Text.  
  
 
    Get-AdfsGlobalAuthenticationPolicy  
      
    AdditionalAuthenticationProvider  : {}  
    DeviceAuthenticationEnabled   : False  
    PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    WindowsIntegratedFallbackEnabled  : True  
      
    Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"  
  
  
![Display Name anpassen](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)  
  
Wie Sie sehen, hat sich die angezeigte Meldung geändert.  
  
![Display Name anpassen](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md) 
