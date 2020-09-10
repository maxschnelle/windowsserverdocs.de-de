---
title: bitsadmin cache and setlimit
description: Referenz Artikel für den bizadmin-Cache und den setLimit-Befehl, mit dem die Cache Größenbeschränkung festgelegt wird.
ms.topic: reference
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7547a2a51104285b10af6b02c1962c89f75d51fa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632482"
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
