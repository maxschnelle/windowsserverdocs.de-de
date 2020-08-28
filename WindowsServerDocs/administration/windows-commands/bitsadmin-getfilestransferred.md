---
title: bitsadmin getfilestransferred
description: Referenz Artikel für den bigsadmin getfilestransferred-Befehl, der die Anzahl der für den angegebenen Auftrag übertragenen Dateien abruft.
ms.topic: reference
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e86e35d80e8e6b00d973b60e314f22068f7d115b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033588"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred

Ruft die Anzahl der Dateien ab, die für den angegebenen Auftrag übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getfilestransferred <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Anzahl der Dateien ab, die im Auftrag mit dem Namen *mydownloadjob*übertragen wurden:

```
bitsadmin /getfilestransferred myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
