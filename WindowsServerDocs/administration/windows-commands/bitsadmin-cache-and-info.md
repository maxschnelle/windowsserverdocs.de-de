---
title: bitsadmin cache and info
description: Referenz Artikel für den bistiadmin-Cache und den Info-Befehl, der einen bestimmten Cache Eintrag absichert.
ms.topic: reference
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cce96d25b3968c1f975b6426ce8c25e7420f7bd3
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028888"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin cache and info

Sichert einen bestimmten Cache Eintrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /info recordID [/verbose]
```

### <a name="parameters"></a>Parameter

| Paramreter | Beschreibung |
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
