---
ms.assetid: 25f5aff1-6abf-4dea-b531-f1d9943bc181
title: AD FS-Anpassung in Windows Server 2016
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e4d463f5f25fe85dc95d767c9c75b722e60b012
ms.sourcegitcommit: a2699e93a0a19cb138c1fde0c9af36774a12f865
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2017
---
# <a name="ad-fs-customization-in-windows-server-2016"></a>AD FS-Anpassung in Windows Server 2016

>Gilt für: Windows Server 2016

Reaktion auf Feedback von Organisationen, die mit AD FS-haben wir zusätzliche Tools zum Anpassen des Benutzers in Erfahrung für einzelne von AD FS geschützte Anwendungen melden hinzugefügt.  
Zusätzlich zur Angabe pro Anwendung Webinhalte, z.B. Beschreibungstext und Links, können Sie jetzt gesamte Webdesigns pro Anwendung angeben.  Dazu gehören das Logo, Abbildung, Stylesheets oder eine Datei für die gesamte onload.js.  
  
## <a name="global-settings"></a>Globale Einstellungen    
Allgemeine globale Einstellungen finden Sie unter zu [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx), die im Lieferumfang von AD FS unter Windows Server2012 R2.  
  
## <a name="pre-requisites"></a>Voraussetzungen  
Die folgenden erforderlichen Komponenten sind erforderlich, bevor Sie versuchen, die in diesem Dokument beschriebenen Verfahren.  
  
-   AD FS in Windows Server2016 Technical Preview 4 oder höher  
  
## <a name="configure-ad-fs-relying-parties"></a>Konfigurieren von AD FS-vertrauenden  
Pro relying Party-Anmeldung Web können Elemente und Designs konfiguriert werden mit den folgenden PowerShell-Beispielen:  
  
### <a name="customize-messages"></a>Anpassen von Nachrichten  
  
```  
PS C:\>Set-AdfsRelyingPartyWebContent  
    -TargetRelyingPartyName "<RP trust Name>"  
    -CompanyName "This text appears in place of the federation service display name"  
    -OrganizationalNameDescriptionText "This text appears right below the company name"  
    -SignInPageDescription "This text appears below the credential prompt"  
```  
  
### <a name="customize-company-name-logo-and-image"></a>Firmenname, Logo und Image Anpassen  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -Logo @{path="C:\Images\applogo.png"}  
    -Illustration @{path="C:\Images\appillustration.jpg"}  
```  
  
### <a name="customize-entire-page"></a>Passen Sie die gesamte Seite  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -OnLoadScriptPath @{path="c:\scripts\adfstheme\onload.js"}  
```  
  
## <a name="custom-themes-and-advanced-custom-themes"></a>Benutzerdefinierte Designs und erweiterte benutzerdefinierte Designs  
  
Benutzerdefinierte Designs finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx) und [Advanced Customization of AD FS Sign-in Pages.](https://technet.microsoft.com/library/dn636121.aspx)  
  
## <a name="assigning-custom-web-themes-per-rp"></a>Zuweisen von benutzerdefinierten Webdesigns pro RP  
  
Verwenden Sie zum Zuweisen ein benutzerdefiniertes Designs pro RP das folgende Verfahren:  
  
1. Erstellen Sie ein neues Design als Kopie für die standardmäßige globale AD FS-Design  
<code>New-AdfsWebTheme -Name AppSpecificTheme -SourceName default</code>  
2.  Exportieren Sie das Design für die Anpassung <code>Export-AdfsWebTheme -Name AppSpecificTheme -DirectoryPath c:\appspecifictheme</code>3.Designdateien (Bilder, Css, onload.js) in Ihrem bevorzugten Editor anpassen oder Ersetzen Sie die Datei 4. Importieren von angepassten Dateien aus dem Dateisystem auf AD FS (für das neue Design) <code>Set-AdfsWebTheme -TargetName AppSpecificTheme -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';Path="c:\appspecifictheme\script\onload.js"}</code>5.neue, benutzerdefinierte Design für bestimmte RP (oder den RP) übernehmen
<code>Set-AdfsRelyingPartyWebTheme -TargetRelyingPartyName urn:app1 -SourceWebThemeName AppSpecificTheme</code>  
  
## <a name="home-realm-discovery"></a>Startbereichsermittlung  
Dicovery Startbereich Anpassung finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).  
  
## <a name="updated-password-page"></a>Aktualisierte Seite  
Weitere Informationen zum Anpassen der Update-Seite "Kennwort" finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).  
  
## <a name="customizing-and-alternate-ids"></a>Anpassen und alternative-IDs  
Benutzer können sich anmelden, um Active Directory-Verbunddienste (AD FS)-fähigen Anwendungen mit einer Benutzer-ID, die von Active Directory-Domänendienste (AD DS) akzeptiert wird. Dazu gehören Benutzerprinzipalnamen (UPNs) (johndoe@contoso.com) oder Domäne qualifiziert Sam-Kontonamen (Contoso\johndoe oder contoso.com\johndoe).  Weitere Informationen zu diesem finden Sie unter [Konfigurieren von alternativen Anmelde-ID.](Configuring-Alternate-Login-ID.md)  
  
Sie sollten außerdem Anpassen der AD FS-Anmeldeseite um End-Benutzern einige Hinweis auf die alternativen Anmelde-ID Können Sie dies tun, indem Sie die angepasste Anmeldeseite Beschreibung Weitere Informationen finden Sie unter Hinzufügen [Customizing the AD FS Sign-in Pages.](https://technet.microsoft.com/library/dn280950.aspx)   
  
Sie können dazu auch Feld "Benutzername" Zeichenfolge "Melden Sie sich mit Organisations-Konto" anpassen.  Informationen hierzu finden Sie unter [Advanced Customization of AD FS Sign-in Pages](https://technet.microsoft.com/library/dn636121.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
