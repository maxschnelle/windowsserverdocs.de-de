---
title: bitsadmin getmodificationtime
description: Referenz Artikel für den bizadmin getmodificationtime-Befehl, der den Zeitpunkt der letzten Änderung des Auftrags oder die erfolgreiche Übertragung der Daten abruft.
ms.topic: reference
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 763ca0f60fa834ad14b92eb7963107fa407a8964
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028728"
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
