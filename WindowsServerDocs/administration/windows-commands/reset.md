---
title: reset
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a412eff7bdf432608a999edb4531074ed5e8f26
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933089"
---
# <a name="reset"></a>reset



Setzt DiskShadow.exe auf den Standardzustand zurück. **Reset** ist besonders nützlich, wenn Sie zusammengesetzte DiskShadow-Vorgänge wie **Create**, **Import**, **Backup**oder **Restore**voneinander trennen.

## <a name="syntax"></a>Syntax

```
reset
```

## <a name="remarks"></a>Hinweise

-   Wenn Sie den **Reset** -Befehl verwenden, verlieren Sie den Status von Befehlen wie " **Add**", " **set**", " **Load**" oder " **Writer**". **Reset** gibt auch ivssbackupcomponent-Schnittstellen frei und verliert nicht persistente Schatten Kopien.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)