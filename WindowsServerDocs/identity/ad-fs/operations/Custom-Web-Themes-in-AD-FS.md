---
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: Benutzerdefinierte Webdesigns in AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: affcc8b7d6aed56c37ddf00dd1c962c0d82fd85b
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865775"
---
# <a name="custom-web-themes-in-ad-fs"></a>Benutzerdefinierte Webdesigns in AD FS 

Das Design, das standardmäßig\-versendet\-\-wird, wird als Standard bezeichnet. Sie können das Standarddesign exportieren und verwenden, um schnell anzufangen. Sie können das Aussehen und Verhalten anpassen, unter anderem das Layout, indem Sie die CSS-Datei ändern, das neue Design importieren und anwenden und dann das angepasste Aussehen und Verhalten verwenden. Wenn Sie die CSS-Datei verwenden, können Sie zudem einfacher mit Ihren Webdesignern zusammenarbeiten.  
  
Mit dem folgenden Cmdlet erstellen Sie ein benutzerdefiniertes Webdesign, das das Standardwebdesign dupliziert.  
  
  
`New-AdfsWebTheme –Name custom –SourceName default ` 

  
Sie können die CSS-Datei ändern und das neue Webdesign durch Verwendung der neuen CSS-Datei konfigurieren. Verwenden Sie zum Exportieren eines Webdesigns das folgende Cmdlet.  
  

    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  

  
Verwenden Sie zum Anwenden der CSS-Datei auf das neue Design das folgende Cmdlet.  
  

    Set-AdfsWebTheme –TargetName custom –StyleSheet @{path=”c:\NewTheme.css”}  
  
  
Mit dem folgenden Cmdlet erstellen Sie ein benutzerdefiniertes Webdesign über ein neues Stylesheet.  
  
  
`New-AdfsWebTheme –Name custom –StyleSheet @{path=”c:\NewTheme.css”} –RTLStyleSheetPath c:\NewRtlTheme.css ` 
  
  
  
Verwenden Sie das folgende Cmdlet, um das benutzerdefinierte Webdesign auf AD FS anzuwenden.  
  

`Set-AdfsWebConfig -ActiveThemeName custom`  

  
Verwenden Sie das folgende Cmdlet, um AD FS JavaScript hinzuzufügen.  
  
 
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=' /adfs/portal/script/onload.js';path="D:\inetpub\adfsassets\script\onload.js"}  


## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
