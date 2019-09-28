---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: Add Sign @ no__t-0in Page Description
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3b34a4e54aebd5b9dc3655eecd770a25f7ea97cf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407745"
---
# <a name="add-sign-in-page-description"></a>Add Sign @ no__t-0in Page Description


## <a name="to-add-sign-in-page-description"></a>Zum Hinzufügen von Sign @ no__t-0in Page Description  
Verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax, um der Seite Sign @ no__t-1In das Zeichen @ no__t-0in Page Description hinzuzufügen.  

![Anmelde Beschreibung hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> Die Zeichenfolge für den `SignInPageDescriptionText`-Parameter unterstützt reines HTML mit und ohne Tags. Daher können Sie das folgende Cmdlet auch ohne das Tag &lt;p @ no__t-1 ausführen.  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

Nachdem die Seite Sign @ no__t-0in angepasst ist, hat die Anpassung Vorrang. Daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, sollten diese zunächst mit einem Gebiets Schema (@ no__t-0less) konfiguriert werden, z. b. "en", bevor Sie das Gebiets Schema "Country" und "Region @ no__t-1specific" wie z. b. "en @ no__t-2US" konfigurieren.  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
