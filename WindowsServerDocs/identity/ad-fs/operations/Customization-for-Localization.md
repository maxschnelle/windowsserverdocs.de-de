---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: "Anpassung für die Lokalisierung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ac206d5aa8af970b65a014955ac66a8cf2835eb6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="customization-for-localization"></a>Anpassung für die Lokalisierung 

>Gilt für: Windows Server 2016, Windows Server2012 R2

Eine Lokalisierung von Webinhalten in andere Sprachen als Englisch ist möglich. Achten Sie darauf, Folgendes, wenn Sie lokalisieren.  
  
Nachdem die Inhalte angepasst ist, hat die Anpassung Vorrang vor; aus diesem Grund sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, konfigurieren Sie ihn mit einem Country\ Gebietsschema ohne zuerst, z.B. "En", bevor Sie ein Landes- und Region\ Gebietsschema wie z.B. konfigurieren "En\-us".  
  
Im folgenden sehen einige weitere Codebeispiele.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}  
      
    Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}  

  
Im folgenden sehen einige weitere Codebeispiele.  
  
 
    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"  
  
  

    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"  
 
  
Wenn Sie möchten die Webinhalte an andere Sprachen als Englisch anpassen, die die Eingabe von Unicode erforderlich ist, empfehlen wir, dass Sie die Windows PowerShell ISE verwenden. Weitere Informationen finden Sie unter [Einführung in die Windows PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md) 
