---
title: bitsadmin setmaxdownloadtime
description: Referenz Artikel für den Befehl "bizadmin setmaxdownloadtime", der das Download Timeout in Sekunden festlegt.
ms.topic: reference
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9937a4f2945e45d351cfa3506a9aefbd4723f37c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630809"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>bitsadmin setmaxdownloadtime

Legt das Download Timeout in Sekunden fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setmaxdownloadtime <job> <timeout>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
