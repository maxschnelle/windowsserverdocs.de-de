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
ms.openlocfilehash: 9a6bce383e04a892203c38cadc7ec2b7388b23a6
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965412"
---
# <a name="customization-for-localization"></a>Anpassung für die Lokalisierung 


Eine Lokalisierung von Webinhalten in andere Sprachen als Englisch ist möglich. Berücksichtigen bei der Lokalisierung die folgenden Überlegungen.  
  
Nachdem die Inhalte angepasst sind, hat die Anpassung Vorrang, daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, konfigurieren Sie Sie zunächst mit einem \- Gebiets Schema ohne Land, z. b. "en", bevor Sie ein Gebiets Schema für Länder und Regionen \- wie z. b. "en \- US" konfigurieren.  
  
Im Folgenden sind einige weitere Codebeispiele aufgeführt.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}  
      
    Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}  

  
Im Folgenden sind einige weitere Codebeispiele aufgeführt.  
  
 
    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"  
  
  

    Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"  
 
  
Wenn Sie die Webinhalte an andere Sprachen als Englisch anpassen möchten, für die die Eingabe von Unicode erforderlich ist, empfiehlt es sich, dass Sie die Windows PowerShell ISE verwenden. Weitere Informationen finden Sie [unter Einführung in die Windows PowerShell ISE](/previous-versions/mt707506(v=msdn.10)).  

## <a name="additional-references"></a>Zusätzliche Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md) 
