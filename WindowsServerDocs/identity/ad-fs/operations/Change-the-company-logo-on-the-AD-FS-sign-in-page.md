---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: Ändern das Firmenlogo auf den AD FS-Anmeldeseite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fe5c138466ea288b5dfb8c7c284603150ab9d874
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190027"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>Ändern das Firmenlogo auf den AD FS-Anmeldeseite

#### <a name="change-company-logo"></a>Ändern des Unternehmenslogos  
So ändern Sie das Logo des Unternehmens, die auf die Anmeldeseite angezeigt wird\-auf der Seite verwenden Sie die folgenden PowerShell-Windows-PowerShell-Cmdlets und Syntax.  

![Logo ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> Wir empfehlen für das Logo die Maße 260x35 bei 96 dpi mit einer Dateigröße von höchstens 10 KB.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}  

  
> [!NOTE]  
> Der `TargetName` -Parameter ist erforderlich. Das mit AD FS veröffentlichte Standarddesign heißt *Standard*.  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
