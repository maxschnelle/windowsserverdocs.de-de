---
title: reset
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0701324ad1ee94cc645c7519d81fef7357b6a34a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722348"
---
# <a name="reset"></a>reset



Setzt "DiskShadow. exe" auf den Standardzustand zurück. **Reset** ist besonders nützlich, wenn Sie zusammengesetzte DiskShadow-Vorgänge wie **Create**, **Import**, **Backup**oder **Restore**voneinander trennen.

## <a name="syntax"></a>Syntax

```
reset
```

## <a name="remarks"></a>Bemerkungen

-   Wenn Sie den **Reset** -Befehl verwenden, verlieren Sie den Status von Befehlen wie " **Add**", " **set**", " **Load**" oder " **Writer**". **Reset** gibt auch ivssbackupcomponent-Schnittstellen frei und verliert nicht persistente Schatten Kopien.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)