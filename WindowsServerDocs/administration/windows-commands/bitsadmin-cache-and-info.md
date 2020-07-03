---
title: bitsadmin cache and info
description: Referenz Artikel für den bistiadmin-Cache und den Info-Befehl, der einen bestimmten Cache Eintrag absichert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dabf9b229138bf1d39863643574c5509ffcfcd91
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923264"
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
