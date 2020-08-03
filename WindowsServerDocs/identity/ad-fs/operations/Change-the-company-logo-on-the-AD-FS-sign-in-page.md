---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: Ändern des Unternehmens Logos auf der AD FS-Anmeldeseite
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b61f7321dc75613a3450998284536673bd790f2b
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519819"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>Ändern des Unternehmens Logos auf der AD FS-Anmeldeseite

## <a name="change-company-logo"></a>Ändern des Unternehmenslogos

Um das Logo des Unternehmens zu ändern, das auf der Anmelde \- Seite angezeigt wird, verwenden Sie das folgende PowerShell-Windows PowerShell-Cmdlet und die folgende Syntax.

![Logo ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

> [!IMPORTANT]
> Wir empfehlen für das Logo die Maße 260x35 bei 96 dpi mit einer Dateigröße von höchstens 10 KB.

```powershell
Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}
```

> [!NOTE]
> Der `TargetName`-Parameter ist erforderlich. Das Standarddesign, das mit AD FS freigegeben wird, hat den Namen *default*.

## <a name="additional-references"></a>Zusätzliche Verweise

[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
