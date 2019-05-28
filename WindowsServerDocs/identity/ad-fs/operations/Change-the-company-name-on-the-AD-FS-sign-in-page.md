---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: Ändern Sie den Namen "Unternehmen" auf der AD FS-Anmeldeseite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e2b5c7228094305759344d5094cffa7f24a0da7a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190022"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>Ändern Sie den Namen "Unternehmen" auf der AD FS-Anmeldeseite
 
So ändern Sie den Namen des Unternehmens, die auf die Anmeldeseite angezeigt wird\-auf der Seite verwenden Sie die folgenden Windows PowerShell-Cmdlets und Syntax. Dieser Wert wird standardmäßig festgelegt, indem der Wert des Verbunddienst-Anzeigenamens verwendet wird, den Sie während des Setups eingegeben haben.  

![Ändern des Namens](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> Sie können auch die Windows PowerShell integrierte Skriptumgebung \(ISE\) so ändern Sie den Firmennamen. Mithilfe der Windows PowerShell ISE können Sie Inhalte in einem Unicodeprogramm anzeigen\-kompatiblen Umgebung. Weitere Informationen finden Sie unter [Introducing the Windows PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx).  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
  
