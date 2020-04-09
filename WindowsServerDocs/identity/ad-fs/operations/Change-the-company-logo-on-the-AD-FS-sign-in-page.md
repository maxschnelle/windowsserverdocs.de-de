---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: Ändern des Unternehmens Logos auf der AD FS-Anmeldeseite
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d12429b22265495cb8168ce3e5993a5cf3e74a0c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859973"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>Ändern des Unternehmens Logos auf der AD FS-Anmeldeseite

#### <a name="change-company-logo"></a>Ändern des Unternehmenslogos  
Verwenden Sie das folgende PowerShell-Windows PowerShell-Cmdlet und die folgende Syntax, um das Logo des Unternehmens zu ändern, das auf der Seite Sign\-in angezeigt wird.  

![Logo ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> Wir empfehlen für das Logo die Maße 260x35 bei 96 dpi mit einer Dateigröße von höchstens 10 KB.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}  

  
> [!NOTE]  
> Der `TargetName` -Parameter ist erforderlich. Das Standarddesign, das mit AD FS freigegeben wird, hat den Namen *default*.  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
