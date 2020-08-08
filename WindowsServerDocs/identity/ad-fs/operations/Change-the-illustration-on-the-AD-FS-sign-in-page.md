---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: Ändern der Abbildung auf der AD FS Anmeldeseite
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 91ba9ca9068ccf2d619c8f98e1f678df7194e1a6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956517"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>Ändern der Abbildung auf der AD FS Anmeldeseite

## <a name="change-the-illustration"></a>Ändern der Abbildung

Zum Ändern der Abbildung können Sie in der Grafik auf der linken Seite, die auf der Anmeldeseite angezeigt wird \- , das folgende Windows PowerShell-Cmdlet und die folgende Syntax verwenden.

![Abbildung ändern](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

> [!IMPORTANT]
> Wir empfehlen für die Illustration die Maße 1420x1080 Pixel bei 96 dpi mit einer Dateigröße von höchstens 200 KB.

```powershell
Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}
```

## <a name="additional-references"></a>Weitere Verweise

[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
