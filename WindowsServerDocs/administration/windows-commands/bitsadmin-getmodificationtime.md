---
title: bitsadmin getmodificationtime
description: Referenz Thema für den bizadmin getmodificationtime-Befehl, der den Zeitpunkt der letzten Änderung des Auftrags oder die erfolgreiche Übertragung der Daten abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6bab8c317917894a351c03df1efefb17842ecb7d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717840"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
