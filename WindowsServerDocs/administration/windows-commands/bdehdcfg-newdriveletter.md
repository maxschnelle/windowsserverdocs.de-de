---
title: bdehdcfg newdriveletter
description: Referenz Artikel für den bdehdcfg newdriveletter-Befehl, der dem Teil eines Laufwerks, das als Systemlaufwerk verwendet wird, einen neuen Laufwerk Buchstaben zuweist.
ms.topic: reference
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf3cf52bfd23db5aadd82170de2bf20c8e602573
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031548"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter

Weist dem Teil eines Laufwerks, das als Systemlaufwerk verwendet wird, einen neuen Laufwerk Buchstaben zu. Als bewährte Vorgehensweise wird empfohlen, dem Systemlaufwerk keinen Laufwerk Buchstaben zuzuweisen.

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -newdriveletter <drive_letter>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------| ----------- |
| `<drive_letter>` | Definiert den Laufwerk Buchstaben, der dem angegebenen Ziellaufwerk zugewiesen wird. |

## <a name="examples"></a>Beispiele

Zum Zuweisen des Standard Laufwerks wird der Laufwerk Buchstabe `P` :

```
bdehdcfg -target default -newdriveletter P:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
