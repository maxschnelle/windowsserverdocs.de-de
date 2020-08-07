---
title: bitsadmin cache and setlimit
description: Referenz Artikel für den bizadmin-Cache und den setLimit-Befehl, mit dem die Cache Größenbeschränkung festgelegt wird.
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41a1331a19f66e7d84dc3eb57b04d42596a40628
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894706"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin cache and setlimit

Legt die Cache Größenbeschränkung fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Prozent | Der als Prozentsatz des gesamten Festplatten Speichers definierte Cache Limit. |

## <a name="examples"></a>Beispiele

So legen Sie die Cache Größenbeschränkung auf 50% fest:

```
bitsadmin /cache /setlimit 50
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Cache"](bitsadmin-cache.md)
