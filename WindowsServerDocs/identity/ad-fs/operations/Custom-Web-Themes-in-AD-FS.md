---
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: Benutzerdefinierte Webdesigns in AD FS
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 300c9fda84285ddfc52a4f47ea0198deb6fd33ef
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="custom-web-themes-in-ad-fs"></a>Benutzerdefinierte Webdesigns in AD FS 

>Gilt für: Windows Server 2016, Windows Server2012 R2

Das Design, das ausgeliefert Out-Of\-The\-Feld ist standardmäßig aufgerufen. Sie können das Standarddesign exportieren und verwenden Sie es, damit Sie schnell beginnen können. Passen Sie das Aussehen und Verhalten, die das Layout enthält, durch Ändern der CSS-Datei, importieren und das neue Design anwenden, und anschließend können Sie verwenden das angepasste Aussehen und Verhalten. Verwenden die CSS-Datei erleichtert auch Ihren Webdesignern zusammenarbeiten.  
  
Das folgende Cmdlet erstellt ein benutzerdefiniertes Webdesign, das das standardwebdesign dupliziert.  
  
  
`New-AdfsWebTheme –Name custom –SourceName default ` 

  
Sie können die CSS-Datei ändern, und konfigurieren das neue Webdesign mithilfe der neuen CSS-Datei. Verwenden Sie zum Exportieren eines Webdesigns das folgende Cmdlet.  
  

    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  

  
Verwenden Sie zum Anwenden der CSS-Datei auf das neue Design das folgende Cmdlet.  
  

    Set-AdfsWebTheme –TargetName custom –StyleSheet @{path=”c:\NewTheme.css”}  
  
  
Das folgende Cmdlet erstellt ein benutzerdefiniertes Webdesign über ein neues Stylesheet.  
  
  
`New-AdfsWebTheme –Name custom –StyleSheet @{path=”c:\NewTheme.css”} –RTLStyleSheetPath c:\NewRtlTheme.css ` 
  
  
  
Zum Anwenden des benutzerdefinierten Webdesigns auf AD FS verwenden Sie das folgende Cmdlet.  
  

`Set-AdfsWebConfig -ActiveThemeName custom`  

  
Verwenden Sie das folgende Cmdlet, um Informationen zum Hinzufügen von JavaScript zu AD FS.  
  
 
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’ /adfs/portal/script/onload.js’;path="D:\inetpub\adfsassets\script\onload.js"}  


## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
