---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: Anpassen von anzeigen Amen und Beschreibungen für Authentifizierungsmethoden
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 679f60d1328795ef4f272f0159c6be5185428d59
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954266"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>Anpassen von anzeigen Amen und Beschreibungen für Authentifizierungsmethoden

Sie können zum Anpassen der Anzeigenamen und Beschreibungen für die Authentifizierungsmethoden das PowerShell-Cmdlet `Set-AdfsAuthenticationProviderWebContent` verwenden.  Um dieses Cmdlet verwenden zu können, benötigen Sie zunächst den Namen der Authentifizierungsmethode, die Sie anpassen möchten.  Verwenden Sie hierzu `Get-AdfsGlobalAuthenticationPolicy`.  Im folgenden Beispiel sehen Sie, dass auf \- der Anmeldeseite Folgendes angezeigt wird: "Anmelden mit einem X. 509-Zertifikat".  Wir möchten dies für die Benutzer vereinfachen.

![Display Name anpassen](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)

Wir rufen zuerst den Namen der Authentifizierungsmethode ab und bearbeiten dann den angezeigten Text.

```powershell
Get-AdfsGlobalAuthenticationPolicy

AdditionalAuthenticationProvider  : {}
DeviceAuthenticationEnabled   : False
PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}
PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}
WindowsIntegratedFallbackEnabled  : True

Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"
 ```

![Display Name anpassen](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)

Wie Sie sehen, hat sich die angezeigte Meldung geändert.

![Display Name anpassen](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)

## <a name="additional-references"></a>Weitere Verweise

[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
