---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: Ändern des Unternehmens namens auf der AD FS-Anmeldeseite
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e47d0ee6b1969bca847dd88bfc6cca69bd72b6ba
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956577"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>Ändern des Unternehmens namens auf der AD FS-Anmeldeseite

Verwenden Sie zum Ändern des Namens des Unternehmens, das auf der Anmeldeseite angezeigt wird \- , das folgende Windows PowerShell-Cmdlet und die folgende Syntax. Dieser Wert wird standardmäßig festgelegt, indem der Wert des Verbunddienst-Anzeigenamens verwendet wird, den Sie während des Setups eingegeben haben.

![Name ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)

```powershell
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"
```

> [!NOTE]
> Sie können auch die Windows PowerShell Integrated Scripting Environment \( ISE verwenden \) , um den Firmennamen zu ändern. Mithilfe der Windows PowerShell ISE können Sie Inhalte in einer Unicode- \- kompatiblen Umgebung anzeigen. Weitere Informationen finden Sie unter [Introducing the Windows PowerShell ISE](/previous-versions/mt707506(v=msdn.10)).

## <a name="additional-references"></a>Weitere Verweise

- [AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
