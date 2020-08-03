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
ms.openlocfilehash: 3b6489ae115fb236e19214bceb291cd8f6dfacba
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519809"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>Ändern des Unternehmens namens auf der AD FS-Anmeldeseite

Verwenden Sie zum Ändern des Namens des Unternehmens, das auf der Anmeldeseite angezeigt wird \- , das folgende Windows PowerShell-Cmdlet und die folgende Syntax. Dieser Wert wird standardmäßig festgelegt, indem der Wert des Verbunddienst-Anzeigenamens verwendet wird, den Sie während des Setups eingegeben haben.

![Name ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)

```powershell
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"
```

> [!NOTE]
> Sie können auch die Windows PowerShell Integrated Scripting Environment \( ISE verwenden \) , um den Firmennamen zu ändern. Mithilfe der Windows PowerShell ISE können Sie Inhalte in einer Unicode- \- kompatiblen Umgebung anzeigen. Weitere Informationen finden Sie unter [Introducing the Windows PowerShell ISE](/previous-versions/mt707506(v=msdn.10)).

## <a name="additional-references"></a>Zusätzliche Verweise

- [AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
