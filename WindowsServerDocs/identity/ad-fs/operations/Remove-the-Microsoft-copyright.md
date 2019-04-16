---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: Entfernen Sie den Microsoft-Copyrighthinweis
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c2e6f9445e53a5b5867a763d58ad4a6ca3600cbe
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="remove-the-microsoft-copyright"></a>Entfernen Sie den Microsoft-Copyrighthinweis 

>Gilt für: Windows Server 2016, Windows Server2012 R2
 
Die AD FS-Seiten enthalten standardmäßig den Microsoft-Copyrighthinweis. Um diesen Copyrighthinweis aus Ihren benutzerdefinierten Seiten entfernen, können Sie das folgende Verfahren verwenden. 

![Copyright entfernen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png) 
  
## <a name="to-remove-the-microsoft-copyright"></a>So entfernen Sie den Microsoft-Copyrighthinweis  
  
1.  Erstellen Sie ein benutzerdefiniertes Design, das auf dem standardmäßigen basiert.  
  

    `New-AdfsWebTheme –Name custom –SourceName default ` 
 
  
2.  Exportieren Sie das Design, indem Sie den Ausgabeordner angeben.  

    `Export-AdfsWebTheme -Name custom -DirectoryPath C:\customWebTheme ` 

  
3.  Suchen Sie die Style.css-Datei, die sich im Ausgabeordner befindet. Mithilfe der im vorherige Beispiel wäre der Pfad C:\\CustomWebTheme\\Css\\Style.css.  
  
4.  Öffnen Sie die Style.css-Datei in einem Editor wie Editor.  
  
5.  Suchen Sie nach dem `#copyright` Teil, und ändern sie die folgenden:  
  `#copyright {color:#696969; display:none;} ` 
 
6.  Erstellen Sie ein benutzerdefiniertes Design, das auf der neuen Style.css-Datei basiert.  
  
    `Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}  `

7.  Aktivieren Sie das neue Design.  
  

    `Set-AdfsWebConfig -ActiveThemeName custom ` 


Das Urheberrecht am unteren Rand der Seite "Anmelden" sollte nun nicht mehr angezeigt werden.

![Copyright entfernen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md) 
