---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: "Beschreibung der Anmeldeseite hinzufügen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 128a4ffd8d4b9dfcfe5f0e8e2df8a0e1505cbb24
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="add-sign-in-page-description"></a>Beschreibung der Anmeldeseite hinzufügen

>Gilt für: Windows Server 2016, Windows Server2012 R2

## <a name="to-add-sign-in-page-description"></a>Beschreibung der Anmeldeseite hinzufügen  
Verwenden Sie zum Hinzufügen einer beschreibungs Anmeldeseite auf der Anmeldeseite das folgende Windows PowerShell-PowerShell-Cmdlet und die folgende Syntax.  

![Protokoll in der Beschreibung hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> Die Zeichenfolge für die `SignInPageDescriptionText` -Parameter unterstützt reines HTML mit den Tags und ohne. Aus diesem Grund können Sie auch das folgende Cmdlet ausführen, ohne die &lt;p&gt; Tag.  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

Nachdem die Anmeldeseite angepasst ist, hat die Anpassung Vorrang vor; aus diesem Grund sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, sie sollten konfiguriert werden mit einem Gebietsschema Country\ weniger zuerst, z.B. "En", bevor Sie z.B. das Land und Region\ Gebietsschema konfigurieren "En\-us".  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
