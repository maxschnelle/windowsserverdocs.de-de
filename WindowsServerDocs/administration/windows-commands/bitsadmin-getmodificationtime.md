---
title: bitsadmin getmodificationtime
description: Referenz Artikel für den bizadmin getmodificationtime-Befehl, der den Zeitpunkt der letzten Änderung des Auftrags oder die erfolgreiche Übertragung der Daten abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9055c0ac70bc2360601ecd1b1f91c8ad3908d704
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928161"
---
# <a name="bitsadmin-getmodificationtime"></a>bitsadmin getmodificationtime

Ruft den Zeitpunkt der letzten Änderung des Auftrags oder die erfolgreiche Übertragung der Daten ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getmodificationtime <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
