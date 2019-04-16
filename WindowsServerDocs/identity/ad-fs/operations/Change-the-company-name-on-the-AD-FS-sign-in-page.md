---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: "Ändern Sie der Name des Unternehmens auf dem AD FS-Anmeldeseite"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8e99f6fed8922ed15bf78a98b207b6f46767763a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>Ändern Sie der Name des Unternehmens auf dem AD FS-Anmeldeseite

>Gilt für: Windows Server 2016, Windows Server2012 R2
 
Zum Ändern des Namens des Unternehmens, die auf der Anmeldeseite angezeigt wird, verwenden Sie die folgenden Windows PowerShell-PowerShell-Cmdlet und die folgende Syntax. Dieser Wert wird standardmäßig festgelegt, mit dem Wert aus dem Verbunddienst Anzeigenamen, den Sie während des Setups eingegeben haben.  

![Ändern Sie den Namen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> Die Windows PowerShell Integrated Scripting Environment \(ISE\) können auch den Firmennamen ändern. Mithilfe der Windows PowerShell ISE können Sie Inhalte in einer Umgebung mit farblich gekennzeichneter Syntax kompatible anzeigen. Weitere Informationen finden Sie unter [Einführung in die Windows PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
  
