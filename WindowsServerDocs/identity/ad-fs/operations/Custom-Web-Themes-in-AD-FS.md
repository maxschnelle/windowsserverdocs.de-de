---
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: Benutzerdefinierte Webdesigns in AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bdc39d3ceabce093940d325be93a9e2c50e670c8
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519759"
---
# <a name="custom-web-themes-in-ad-fs"></a>Benutzerdefinierte Webdesigns in AD FS

Das Design, das standardmäßig versendet wird, \- \- \- wird als Standard bezeichnet. Sie können das Standarddesign exportieren und verwenden, um schnell anzufangen. Sie können das Aussehen und Verhalten anpassen, unter anderem das Layout, indem Sie die CSS-Datei ändern, das neue Design importieren und anwenden und dann das angepasste Aussehen und Verhalten verwenden. Wenn Sie die CSS-Datei verwenden, können Sie zudem einfacher mit Ihren Webdesignern zusammenarbeiten.

Mit dem folgenden Cmdlet erstellen Sie ein benutzerdefiniertes Webdesign, das das Standardwebdesign dupliziert.

```powershell
New-AdfsWebTheme –Name custom –SourceName default
```

Sie können die CSS-Datei ändern und das neue Webdesign durch Verwendung der neuen CSS-Datei konfigurieren. Verwenden Sie zum Exportieren eines Webdesigns das folgende Cmdlet.

```powershell
Export-AdfsWebTheme –Name default –DirectoryPath c:\theme
```

Verwenden Sie zum Anwenden der CSS-Datei auf das neue Design das folgende Cmdlet.

```powershell
Set-AdfsWebTheme –TargetName custom –StyleSheet @{path="c:\NewTheme.css"}
```

Mit dem folgenden Cmdlet erstellen Sie ein benutzerdefiniertes Webdesign über ein neues Stylesheet.

```powershell
New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"} –RTLStyleSheetPath c:\NewRtlTheme.css
```

Verwenden Sie das folgende Cmdlet, um das benutzerdefinierte Webdesign auf AD FS anzuwenden.

```powershell
Set-AdfsWebConfig -ActiveThemeName custom
```

Verwenden Sie das folgende Cmdlet, um AD FS JavaScript hinzuzufügen.

```powershell
Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=' /adfs/portal/script/onload.js';path="D:\inetpub\adfsassets\script\onload.js"}
```

## <a name="additional-references"></a>Zusätzliche Verweise

[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
