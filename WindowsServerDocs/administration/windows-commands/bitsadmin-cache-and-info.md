---
title: bitsadmin cache and info
description: Referenz Artikel für den bistiadmin-Cache und den Info-Befehl, der einen bestimmten Cache Eintrag absichert.
ms.topic: reference
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 16eda9ddd04a270fbfd754186fd5c9f4a6152cd5
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632549"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin cache and info

Sichert einen bestimmten Cache Eintrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /info recordID [/verbose]
```

### <a name="parameters"></a>Parameter

| Paramreter | BESCHREIBUNG |
| -------------- | -------------- |
| Datensatz | Die GUID, die dem Cache Eintrag zugeordnet ist. |

## <a name="examples"></a>Beispiele

So sichern Sie den Cache Eintrag mit dem Datensatz-Wert {6511fb02-E195-40A2-B595-e8e2f8f47702}:

```
bitsadmin /cache /info {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Cache"](bitsadmin-cache.md)
