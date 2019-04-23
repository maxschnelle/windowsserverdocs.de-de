---
title: Zurücksetzen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0bd9b6735697cbcefdcf68dc3d4a53a6870a7a76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850961"
---
# <a name="reset"></a>Zurücksetzen



DiskShadow.exe zurückgesetzt auf den Standardzustand. **Zurücksetzen** ist besonders nützlich, z. B. Trennen von DiskShadow Verbundoperationen **erstellen**, **importieren**, **backup**, oder **Wiederherstellen**.

## <a name="syntax"></a>Syntax

```
reset
```

## <a name="remarks"></a>Hinweise

-   Bei Verwendung der **zurücksetzen** Befehl, verlieren Sie Status von Befehlen wie z. B. **hinzufügen**, **festgelegt**, **laden**, oder **Writer**. **Zurücksetzen** auch IVssBackupComponent Schnittstellen frei, und nicht persistent Schattenkopien verliert.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)