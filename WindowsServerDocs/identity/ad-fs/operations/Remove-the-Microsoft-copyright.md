---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: Entfernen des Microsoft-Copyright
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: ec7d9cb02508fc046ce3e8f0378e63c82eecca8d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949774"
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

3. Suchen Sie die `Style.css` Datei, die sich im Ausgabeordner befindet. Wenn Sie das vorherige Beispiel verwenden, lautet der Pfad.`C:\CustomWebTheme\Css\Style.css.`

4. Öffnen Sie die `Style.css` Datei mit einem Editor, z. b. Notepad.

5. Suchen Sie nach dem `#copyright` -Teil, und ändern Sie diesen dann wie folgt:

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. Erstellen Sie ein benutzerdefiniertes Design, das auf der neuen `Style.css` Datei basiert.

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
