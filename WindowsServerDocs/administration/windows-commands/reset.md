---
title: reset
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c27ddd93d06670a30f797bd58dd396a9e7ce70a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835783"
---
# <a name="reset"></a>reset



Setzt "DiskShadow. exe" auf den Standardzustand zurück. **Reset** ist besonders nützlich, wenn Sie zusammengesetzte DiskShadow-Vorgänge wie **Create**, **Import**, **Backup**oder **Restore**voneinander trennen.

## <a name="syntax"></a>Syntax

```
reset
```

## <a name="remarks"></a>Hinweise

-   Wenn Sie den **Reset** -Befehl verwenden, verlieren Sie den Status von Befehlen wie " **Add**", " **set**", " **Load**" oder " **Writer**". **Reset** gibt auch ivssbackupcomponent-Schnittstellen frei und verliert nicht persistente Schatten Kopien.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)