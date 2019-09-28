---
title: Festlegen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: a8903c300d12a019f8fb4aef6d367131a195d034
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371457"
---
# <a name="reset"></a>Festlegen



Setzt "DiskShadow. exe" auf den Standardzustand zurück. **Reset** ist besonders nützlich, wenn Sie zusammengesetzte DiskShadow-Vorgänge wie **Create**, **Import**, **Backup**oder **Restore**voneinander trennen.

## <a name="syntax"></a>Syntax

```
reset
```

## <a name="remarks"></a>Hinweise

-   Wenn Sie den **Reset** -Befehl verwenden, verlieren Sie den Status von Befehlen wie " **Add**", " **set**", " **Load**" oder " **Writer**". **Reset** gibt auch ivssbackupcomponent-Schnittstellen frei und verliert nicht persistente Schatten Kopien.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)