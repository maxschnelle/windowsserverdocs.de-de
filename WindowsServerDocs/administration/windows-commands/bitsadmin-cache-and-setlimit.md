---
title: bitsadmin cache and setlimit
description: Referenz Thema für den bizadmin-Cache und den setLimit-Befehl, mit dem die Cache Größenbeschränkung festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4c41102bfb87ff6d48113c4e85a821b821b5b01
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718287"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Cache"](bitsadmin-cache.md)
