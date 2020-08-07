---
title: reset
description: Referenz Artikel für * * * *-
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f491a3d8c805ac6b3558f3778f6eba91a7551b82
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883651"
---
# <a name="reset"></a>reset



Setzt DiskShadow.exe auf den Standardzustand zurück. **Reset** ist besonders nützlich, wenn Sie zusammengesetzte DiskShadow-Vorgänge wie **Create**, **Import**, **Backup**oder **Restore**voneinander trennen.

## <a name="syntax"></a>Syntax

```
reset
```

## <a name="remarks"></a>Bemerkungen

-   Wenn Sie den **Reset** -Befehl verwenden, verlieren Sie den Status von Befehlen wie " **Add**", " **set**", " **Load**" oder " **Writer**". **Reset** gibt auch ivssbackupcomponent-Schnittstellen frei und verliert nicht persistente Schatten Kopien.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)