---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: "Ändern das Logo auf der AD FS-Anmeldeseite"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ca54abe7fe852b22f2f4d9a717e38d219fa50694
ms.sourcegitcommit: a00fc4426dc4ad0098257f01f0124d6c733d1aef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/09/2018
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>Ändern das Logo auf der AD FS-Anmeldeseite

>Gilt für: Windows Server 2016, Windows Server2012 R2

#### <a name="change-company-logo"></a>Ändern des Unternehmenslogos  
Zum Ändern des Unternehmens, die auf der Anmeldeseite angezeigt wird, verwenden Sie das folgende PowerShell Windows PowerShell-Cmdlet und die folgende Syntax.  

![Logo ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> Es wird empfohlen, die Größe des Logos in 260 x 350 bei 96dpi mit einer Dateigröße von höchstens 10KB sein.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}  

  
> [!NOTE]  
> Die `TargetName` -Parameter ist erforderlich. Ist das Standarddesign, die mit AD FS freigegeben ist mit dem Namen *Standard*.  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
