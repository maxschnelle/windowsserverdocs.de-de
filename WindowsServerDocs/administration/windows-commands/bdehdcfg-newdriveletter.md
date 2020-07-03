---
title: bdehdcfg newdriveletter
description: Referenz Artikel für den bdehdcfg newdriveletter-Befehl, der dem Teil eines Laufwerks, das als Systemlaufwerk verwendet wird, einen neuen Laufwerk Buchstaben zuweist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f210056f74e930ad39361c9fc0cbf05d6e1894f4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923497"
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
