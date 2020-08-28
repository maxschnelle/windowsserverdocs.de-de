---
title: retain
description: Referenz Artikel für den Befehl "beibehalten", bei dem ein vorhandenes dynamisches Volume für die Verwendung als Start-oder System Volume vorbereitet wird.
ms.topic: reference
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 98c27c62ab7e0ac3320986dde6049be40d10db57
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89036989"
---
# <a name="retain"></a>retain

Bereitet ein vorhandenes einfaches dynamisches Volume für die Verwendung als Start-oder System Volume vor. Wenn Sie einen dynamischen Datenträger mit Master Boot Record (MBR) verwenden, erstellt dieser Befehl einen Partitionseintrag im Master Boot Record. Wenn Sie einen dynamischen GPT-Datenträger (GUID-Partitionstabelle) verwenden, erstellt dieser Befehl einen Partitionseintrag in der GUID-Partitionstabelle.

## <a name="syntax"></a>Syntax

```
retain
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
