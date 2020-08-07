---
title: bitsadmin getmodificationtime
description: Referenz Artikel für den bizadmin getmodificationtime-Befehl, der den Zeitpunkt der letzten Änderung des Auftrags oder die erfolgreiche Übertragung der Daten abruft.
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d89d3382c738ffc473135579eb58590f06774d5c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894169"
---
# <a name="bitsadmin-getmodificationtime"></a>bitsadmin getmodificationtime

Ruft den Zeitpunkt der letzten Änderung des Auftrags oder die erfolgreiche Übertragung der Daten ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getmodificationtime <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie den Zeitpunkt der letzten Änderung des Auftrags mit dem Namen *mydownloadjob*ab:

```
bitsadmin /getmodificationtime myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
