---
title: bitsadmin cache and setlimit
description: Referenz Artikel für den bizadmin-Cache und den setLimit-Befehl, mit dem die Cache Größenbeschränkung festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de218990d9176336e779b551bfacc0897df5d114
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923210"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin cache and setlimit

Legt die Cache Größenbeschränkung fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
