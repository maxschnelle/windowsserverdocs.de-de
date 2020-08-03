---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: Ändern der Abbildung auf der AD FS Anmeldeseite
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 47a71fffc864f6ae5ecb46d562f92d2d9cece092
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519789"
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

## <a name="additional-references"></a>Zusätzliche Verweise

[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
