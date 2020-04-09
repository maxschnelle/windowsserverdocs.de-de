---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: Anpassung für die Lokalisierung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: eab7062c6678c0e9f3ef970ef9cff97fa63dd868
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816393"
---
# <a name="customization-for-localization"></a>Anpassung für die Lokalisierung 


Eine Lokalisierung von Webinhalten in andere Sprachen als Englisch ist möglich. Berücksichtigen bei der Lokalisierung die folgenden Überlegungen.  
  
Nachdem die Inhalte angepasst sind, hat die Anpassung Vorrang, daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, konfigurieren Sie Sie zuerst mit einem Land\-weniger Gebiets Schema, z. b. "en", bevor Sie ein Land und eine Region\-bestimmtes Gebiets Schema wie "en\-US" konfigurieren.  
  
Im Folgenden sind einige weitere Codebeispiele aufgeführt.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}  
      
    Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}  

  
Im Folgenden sind einige weitere Codebeispiele aufgeführt.  
  
 
    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"  
  
  

    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"  
 
  
Wenn Sie die Webinhalte an andere Sprachen als Englisch anpassen möchten, für die die Eingabe von Unicode erforderlich ist, empfiehlt es sich, dass Sie die Windows PowerShell ISE verwenden. Weitere Informationen finden Sie unter [Introducing the Windows PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md) 
