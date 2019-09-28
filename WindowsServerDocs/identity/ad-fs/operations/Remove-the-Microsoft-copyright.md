---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: Entfernen des Microsoft-Copyright
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0c24173dd03e03f9e8a19ef5981a6dc1259d62d7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407513"
---
# <a name="remove-the-microsoft-copyright"></a>Entfernen des Microsoft-Copyright 


 
Standardmäßig enthalten die AD FS Seiten das Copyright von Microsoft. Sie können diesen Copyrighthinweis mit dem folgenden Verfahren von Ihren benutzerdefinierten Seiten entfernen. 

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

3. Suchen Sie die Datei "`Style.css`", die sich im Ausgabeordner befindet. Wenn Sie das vorherige Beispiel verwenden, wäre der Pfad `C:\CustomWebTheme\Css\Style.css.`
  
4. Öffnen Sie die Datei `Style.css` mit einem Editor, z. b. Notepad.  
  
5. Suchen Sie nach dem `#copyright` -Teil, und ändern Sie diesen dann wie folgt:  

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. Erstellen Sie ein benutzerdefiniertes Design, das auf der neuen `Style.css`-Datei basiert.  

   ```powershell
   Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}
   ```

7. Aktivieren Sie das neue Design.  

   ```powershell
   Set-AdfsWebConfig -ActiveThemeName custom
   ```

Nun sollte das Copyright unten auf der Anmeldeseite nicht mehr angezeigt werden.

![Copyright entfernen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md) 
