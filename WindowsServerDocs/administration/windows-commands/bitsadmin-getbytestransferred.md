---
title: bitsadmin getbytestransferred
description: Referenz Artikel für den bizadmin getbytestransferred-Befehl, mit dem die Anzahl der für den angegebenen Auftrag übertragenen Bytes abgerufen wird.
ms.topic: reference
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67e1432f2fbef32ac47320d87993f5d62053bb71
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028738"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

Ruft die Anzahl der Bytes ab, die für den angegebenen Auftrag übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Anzahl von Bytes ab, die für den Auftrag mit dem Namen *mydownloadjob*übertragen werden

```
bitsadmin /getbytestransferred myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
