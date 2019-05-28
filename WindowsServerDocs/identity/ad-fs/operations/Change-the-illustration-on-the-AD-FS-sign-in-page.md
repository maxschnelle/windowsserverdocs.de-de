---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: Ändern Sie in der Abbildung auf der AD FS-Anmeldeseite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a182b6243777d119394615008cee63b5e5a71ab8
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189950"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>Ändern Sie in der Abbildung auf der AD FS-Anmeldeseite

## <a name="change-the-illustration"></a>Ändern Sie in der Abbildung  


So ändern Sie in der Abbildung, wechselt die gatewaygrafik auf der linken Seite, die auf die Anmeldeseite angezeigt wird\-auf der Seite verwenden Sie die folgenden Windows PowerShell-Cmdlets und Syntax.  

![Ändern der illustration](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> Wir empfehlen für die Illustration die Maße 1420x1080 Pixel bei 96 dpi mit einer Dateigröße von höchstens 200 KB.  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
  
  
