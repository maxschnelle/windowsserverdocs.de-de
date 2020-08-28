---
title: bitsadmin setmaxdownloadtime
description: Referenz Artikel für den Befehl "bizadmin setmaxdownloadtime", der das Download Timeout in Sekunden festlegt.
ms.topic: reference
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4b0096aeb14c4c8cb69654ad4b3723977d759ef
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024250"
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
