---
title: bitsadmin setmaxdownloadtime
description: Referenz Artikel für den Befehl "bizadmin setmaxdownloadtime", der das Download Timeout in Sekunden festlegt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65853180a22d49011e8edb10ed15ac98625cbc30
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927737"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>bitsadmin setmaxdownloadtime

Legt das Download Timeout in Sekunden fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setmaxdownloadtime <job> <timeout>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| timeout | Die Länge des Download Timeouts (in Sekunden). |

## <a name="examples"></a>Beispiele

Um das Timeout für den Auftrag mit dem Namen *mydownloadjob* auf 10 Sekunden festzulegen.

```
bitsadmin /setmaxdownloadtime myDownloadJob 10
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
