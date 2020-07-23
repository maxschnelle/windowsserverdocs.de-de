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
ms.openlocfilehash: f32abbfbc74ad81dfeab5aed403178be4a9b0a57
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953742"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>Ändern des Unternehmens namens auf der AD FS-Anmeldeseite
 
Verwenden Sie zum Ändern des Namens des Unternehmens, das auf der Anmeldeseite angezeigt wird \- , das folgende Windows PowerShell-Cmdlet und die folgende Syntax. Dieser Wert wird standardmäßig festgelegt, indem der Wert des Verbunddienst-Anzeigenamens verwendet wird, den Sie während des Setups eingegeben haben.  

![Name ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> Sie können auch die Windows PowerShell Integrated Scripting Environment \( ISE verwenden \) , um den Firmennamen zu ändern. Mithilfe der Windows PowerShell ISE können Sie Inhalte in einer Unicode- \- kompatiblen Umgebung anzeigen. Weitere Informationen finden Sie unter [Introducing the Windows PowerShell ISE](/previous-versions/mt707506(v=msdn.10)).  

## <a name="additional-references"></a>Zusätzliche Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
  
