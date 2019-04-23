---
ms.assetid: 25f5aff1-6abf-4dea-b531-f1d9943bc181
title: AD FS-Anpassung unter WindowsServer 2016
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e4d463f5f25fe85dc95d767c9c75b722e60b012
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852031"
---
# <a name="ad-fs-customization-in-windows-server-2016"></a>AD FS-Anpassung unter WindowsServer 2016

>Gilt für: Windows Server 2016

Als Reaktion auf Feedback von Organisationen, die mithilfe von AD FS haben wir hinzugefügt, dass weitere Tools zum Anpassen des Benutzers auf die Oberfläche für einzelne Anwendungen, die von AD FS geschützt anmelden.  
Zusätzlich zum Angeben von pro Anwendung Webinhalte wie Beschreibungstext und Links, können Sie jetzt gesamte Webdesigns pro Anwendung angeben.  Dies schließt das Logo, Abbildung, Stylesheets oder eine gesamte onload.js-Datei.  
  
## <a name="global-settings"></a>Globale Einstellungen    
Allgemeine globale Einstellungen finden Sie in [Anpassen der AD FS-Sign-in-Webseiten](https://technet.microsoft.com/library/dn280950.aspx) , die im Lieferumfang von AD FS unter Windows Server 2012 R2.  
  
## <a name="pre-requisites"></a>Voraussetzungen  
Die folgenden Voraussetzungen sind erforderlich, bevor Sie versuchen, die in diesem Dokument beschriebenen Verfahren.  
  
-   AD FS in Windows Server 2016 TP4 oder höher  
  
## <a name="configure-ad-fs-relying-parties"></a>Konfigurieren von AD FS vertrauenden Seiten  
Pro relying Party-Anmeldung Web können Elemente und Designs konfiguriert werden mit den folgenden PowerShell-Beispielen:  
  
### <a name="customize-messages"></a>Anpassen von Nachrichten  
  
```  
PS C:\>Set-AdfsRelyingPartyWebContent  
    -TargetRelyingPartyName "<RP trust Name>"  
    -CompanyName "This text appears in place of the federation service display name"  
    -OrganizationalNameDescriptionText "This text appears right below the company name"  
    -SignInPageDescription "This text appears below the credential prompt"  
```  
  
### <a name="customize-company-name-logo-and-image"></a>Anpassen von Firmennamen, Logo und image  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -Logo @{path="C:\Images\applogo.png"}  
    -Illustration @{path="C:\Images\appillustration.jpg"}  
```  
  
### <a name="customize-entire-page"></a>Anpassen der gesamten Seite  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -OnLoadScriptPath @{path="c:\scripts\adfstheme\onload.js"}  
```  
  
## <a name="custom-themes-and-advanced-custom-themes"></a>Benutzerdefinierte Designs und erweiterte benutzerdefinierte Designs  
  
Benutzerdefinierte Designs finden Sie unter [Anpassen der AD FS-Sign-in-Webseiten](https://technet.microsoft.com/library/dn280950.aspx) und [Advanced Customization of AD FS-Sign-in-Webseiten.](https://technet.microsoft.com/library/dn636121.aspx)  
  
## <a name="assigning-custom-web-themes-per-rp"></a>Zuweisen von benutzerdefinierten Webdesigns pro vertrauende Seite  
  
Verwenden Sie zum Zuweisen ein benutzerdefiniertes Designs pro vertrauende Seite wie folgt vor:  
  
1. Erstellen Sie ein neues Design als eine Kopie für den Standard, globale Design in AD FS  
<code>New-AdfsWebTheme -Name AppSpecificTheme -SourceName default</code> 2.  Exportieren Sie das Design für die Anpassung <code>Export-AdfsWebTheme -Name AppSpecificTheme -DirectoryPath c:\appspecifictheme</code>  
3. Passen Sie an (Bilder, Css, onload.js) - Dateien in Ihrem bevorzugten Editor, oder Ersetzen Sie die Datei 4. Importieren Sie benutzerdefinierte Dateien aus dem Dateisystem zu AD FS (mit Ausrichtung auf das neue Design) <code>Set-AdfsWebTheme -TargetName AppSpecificTheme -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';Path="c:\appspecifictheme\script\onload.js"}</code>  
5. Wenden Sie neue, benutzerdefinierte Designs an, die bestimmte vertrauende Seite (oder die RP) <code>Set-AdfsRelyingPartyWebTheme -TargetRelyingPartyName urn:app1 -SourceWebThemeName AppSpecificTheme</code>  
  
## <a name="home-realm-discovery"></a>Startbereichsermittlung  
Startbereich Ermittlungsdaten Anpassung finden Sie unter [Anpassen der AD FS-Sign-in-Webseiten](https://technet.microsoft.com/library/dn280950.aspx).  
  
## <a name="updated-password-page"></a>Seite "aktualisierte Kennwort"  
Informationen zum Anpassen der Seite für die Aktualisierung finden Sie unter [Anpassen der AD FS-Sign-in Webseiten](https://technet.microsoft.com/library/dn280950.aspx).  
  
## <a name="customizing-and-alternate-ids"></a>Anpassen und alternative IDs  
Benutzer können sich anmelden, um Active Directory-Verbunddienste (AD FS)-aktivierten Anwendungen, die mit keinerlei Benutzer-ID, die von Active Directory Domain Services (AD DS) akzeptiert wird. Dazu gehören Benutzerprinzipalnamen (UPNs) (johndoe@contoso.com) oder Domäne qualifiziert Sam-Kontonamen (Contoso\johndoe oder contoso.com\johndoe).  Weitere Informationen zu dieser finden Sie unter [konfigurieren alternativer Anmelde-ID an.](Configuring-Alternate-Login-ID.md)  
  
Sie sollten außerdem zum Anpassen der AD FS-Anmeldeseite zum Endbenutzer ein Hinweis über die alternative Anmelde-ID. Sie können dazu die Beschreibung der benutzerdefinierten Anmeldeseite Weitere Informationen finden Sie unter Hinzufügen [Anpassen der AD FS-Sign-in Webseiten.](https://technet.microsoft.com/library/dn280950.aspx)   
  
Sie können dazu auch Anpassen der Zeichenfolge "Mit Unternehmenskonto anmelden", über das Feld "Username".  Informationen zu diesen finden Sie [Advanced Customization of AD FS-Sign-in-Webseiten](https://technet.microsoft.com/library/dn636121.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
