---
title: bitsadmin getmodificationtime
description: Referenz Artikel für den bizadmin getmodificationtime-Befehl, der den Zeitpunkt der letzten Änderung des Auftrags oder die erfolgreiche Übertragung der Daten abruft.
ms.topic: reference
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 293b8ef47374c0df3f9b1cd3d76802d592c3c522
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631930"
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
