---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: "Ändern Sie in der Abbildung auf die AD FS-Anmeldeseite"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ac5e60aaad864248b58a3908e7aa9622165fbc14
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>Ändern Sie in der Abbildung auf die AD FS-Anmeldeseite

>Gilt für: Windows Server 2016, Windows Server2012 R2

## <a name="change-the-illustration"></a>Die Abbildung ändern  


Zum Ändern der Illustration die Grafik auf der linken Seite, die auf der Anmeldeseite angezeigt wird, verwenden Sie die folgenden Windows PowerShell-PowerShell-Cmdlet und die folgende Syntax.  

![Abbildung ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> Es wird empfohlen, die Größe der Abbildung 1420 x 1080 Pixel bei 96 DPI mit einer Dateigröße von höchstens 200 KB sein.  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
  
  
