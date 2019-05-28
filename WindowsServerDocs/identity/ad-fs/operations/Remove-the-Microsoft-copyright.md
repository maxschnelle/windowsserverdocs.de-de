---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: Entfernen Sie den Microsoft-Copyrighthinweis
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6e15f9d1490ad62f1458cd32da6e78a6febec58d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189029"
---
# <a name="remove-the-microsoft-copyright"></a>Entfernen Sie den Microsoft-Copyrighthinweis 


 
Standardmäßig enthalten die AD FS-Seiten der Microsoft-Copyrighthinweis. Sie können diesen Copyrighthinweis mit dem folgenden Verfahren von Ihren benutzerdefinierten Seiten entfernen. 

![Copyright entfernen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png) 
  
## <a name="to-remove-the-microsoft-copyright"></a>So entfernen Sie den Microsoft-Copyrighthinweis  
  
1. Erstellen Sie ein benutzerdefiniertes Design, das auf dem Standarddesign basiert.

   ```powershell
   New-AdfsWebTheme –Name custom –SourceName default
   ```

2. Exportieren Sie das Design, indem Sie den Ausgabeordner angeben.  

   ```powershell
   Export-AdfsWebTheme -Name custom -DirectoryPath C:\CustomWebTheme
   ```

3. Suchen Sie die `Style.css` -Datei, die im Ausgabeordner befindet. Mithilfe der im vorherige Beispiel wäre der Pfad `C:\CustomWebTheme\Css\Style.css.`
  
4. Öffnen der `Style.css` -Datei mit einem Editor wie Editor.  
  
5. Suchen Sie nach dem `#copyright` -Teil, und ändern Sie diesen dann wie folgt:  

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. Erstellen Sie ein benutzerdefiniertes Design, das basierend auf den neuen `Style.css` Datei.  

   ```powershell
   Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}
   ```

7. Aktivieren Sie das neue Design.  

   ```powershell
   Set-AdfsWebConfig -ActiveThemeName custom
   ```

Das Urheberrecht am unteren Rand der Seite "Anmeldung" sollte nun nicht mehr angezeigt werden.

![Copyright entfernen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md) 
