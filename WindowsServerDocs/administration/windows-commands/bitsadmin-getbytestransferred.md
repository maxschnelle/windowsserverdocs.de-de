---
title: bitsadmin getbytestransferred
description: Referenz Artikel für den bizadmin getbytestransferred-Befehl, mit dem die Anzahl der für den angegebenen Auftrag übertragenen Bytes abgerufen wird.
ms.topic: reference
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c67185ff147611436dcb75803e2282542f376019
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632305"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

Ruft die Anzahl der Bytes ab, die für den angegebenen Auftrag übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
