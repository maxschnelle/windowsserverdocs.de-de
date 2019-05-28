---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: Hinzufügen der\-in der Beschreibung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 94ad9889ce78ba77f016210ee478a301babdf307
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190051"
---
# <a name="add-sign-in-page-description"></a>Hinzufügen der\-in der Beschreibung


## <a name="to-add-sign-in-page-description"></a>Add Sign\-in der Beschreibung  
Hinzufügen einer Anmeldung\-in der Beschreibung für die Anmeldung\-auf der Seite verwenden Sie die folgenden Windows PowerShell-Cmdlets und Syntax.  

![in der Beschreibung hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> Die Zeichenfolge für den `SignInPageDescriptionText`-Parameter unterstützt reines HTML mit und ohne Tags. Aus diesem Grund können Sie auch das folgende Cmdlet ausführen, ohne die &lt;p&gt; Tag.  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

nach der Anmeldefunktion\-Seite wird angepasst, die Anpassung Vorrang, daher sollten Sie für alle Sprachen, die Sie unterstützen möchten anpassen. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierten Inhalte konfigurieren, sollten sie mit einem Land konfiguriert sein\-weniger Gebietsschema erste, z. B. "En", bevor Sie Land und Region konfigurieren\-spezifische Gebietsschema wie "En\-us".  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
