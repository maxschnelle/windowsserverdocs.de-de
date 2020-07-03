---
title: bitsadmin cache and delete
description: Referenz Artikel für den bistiadmin-Cache und den DELETE-Befehl, der einen bestimmten Cache Eintrag löscht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 739215722eac761aed45d6b4dba32b2b001450b3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927040"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin cache and delete

Löscht einen bestimmten Cache Eintrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /delete recordID
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Datensatz | Die GUID, die dem Cache Eintrag zugeordnet ist. |

## <a name="examples"></a>Beispiele

So löschen Sie den Cache Eintrag mit der RecordID von {6511fb02-E195-40A2-B595-e8e2f8f47702}:

```
bitsadmin /cache /delete {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Cache"](bitsadmin-cache.md)
