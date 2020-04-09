---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: Ändern des Unternehmens namens auf der AD FS-Anmeldeseite
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 378979825c0e8e505c3996cf8cbcdb471a0c7d79
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859963"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>Ändern des Unternehmens namens auf der AD FS-Anmeldeseite
 
Verwenden Sie zum Ändern des Namens des Unternehmens, das auf der Seite Sign\-in angezeigt wird, das folgende Windows PowerShell-Cmdlet und die folgende Syntax. Dieser Wert wird standardmäßig festgelegt, indem der Wert des Verbunddienst-Anzeigenamens verwendet wird, den Sie während des Setups eingegeben haben.  

![Name ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> Sie können auch die Windows PowerShell Integrated Scripting Environment \(ISE-\) verwenden, um den Namen des Unternehmens zu ändern. Mithilfe der Windows PowerShell ISE können Sie Inhalte in einer Unicode-\-kompatiblen Umgebung anzeigen. Weitere Informationen finden Sie unter [Introducing the Windows PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
  
