---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: Ändern des Unternehmens namens auf der AD FS-Anmeldeseite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c4991b27f104cb96f55f09fa9467f2b93868b910
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407731"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>Ändern des Unternehmens namens auf der AD FS-Anmeldeseite
 
Zum Ändern des Namens des Unternehmens, das auf der Seite Sign @ no__t-0in angezeigt wird, verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax. Dieser Wert wird standardmäßig festgelegt, indem der Wert des Verbunddienst-Anzeigenamens verwendet wird, den Sie während des Setups eingegeben haben.  

![Name ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> Sie können auch den Windows PowerShell Integrated Scripting Environment \(ise @ no__t-1 verwenden, um den Namen des Unternehmens zu ändern. Mithilfe der Windows PowerShell ISE können Sie Inhalte in einer Unicode-Umgebung mit dem Format "@ no__t-0" anzeigen. Weitere Informationen finden Sie unter [Introducing the Windows PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
  
