---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: Anmelde\-in Seiten Beschreibung hinzufügen
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8d3cc69bde1c9126f97926802b53d049ed1ef501
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859993"
---
# <a name="add-sign-in-page-description"></a>Anmelde\-in Seiten Beschreibung hinzufügen


## <a name="to-add-sign-in-page-description"></a>So fügen Sie den Anmelde\-in der Seiten Beschreibung hinzu  
Verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax, um der Seite Sign\-in einen Anmelde\-in der Seiten Beschreibung hinzuzufügen.  

![Anmelde Beschreibung hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> Die Zeichenfolge für den `SignInPageDescriptionText`-Parameter unterstützt reines HTML mit und ohne Tags. Daher können Sie auch das folgende Cmdlet ausführen, ohne das &lt;p&gt;-Tag zu verwenden.  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

Nachdem die Seite Sign\-in angepasst ist, hat die Anpassung Vorrang. Daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, sollten diese zunächst mit einem Land\-geringerem Gebiets Schema konfiguriert werden, z. b. "en", bevor Sie Land und Region\-bestimmtes Gebiets Schema wie "en\-US" konfigurieren.  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
