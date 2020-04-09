---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: Ändern der Abbildung auf der AD FS Anmeldeseite
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: de0fc7af4c4eecad59b7af6b08426ef207da5db1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859953"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>Ändern der Abbildung auf der AD FS Anmeldeseite

## <a name="change-the-illustration"></a>Ändern der Abbildung  


Zum Ändern der Abbildung wird in der Grafik auf der linken Seite, die auf der Seite Sign\-in angezeigt wird, das folgende Windows PowerShell-Cmdlet und die folgende Syntax verwendet.  

![Abbildung ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> Wir empfehlen für die Illustration die Maße 1420x1080 Pixel bei 96 dpi mit einer Dateigröße von höchstens 200 KB.  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
  
  
