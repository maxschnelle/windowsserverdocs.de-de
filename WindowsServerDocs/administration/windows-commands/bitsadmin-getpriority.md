---
title: bitsadmin getpriority
description: Referenz Artikel für den Befehl bizadmin GetPriority, der die Priorität des angegebenen Auftrags abruft.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 397a762a210aeae7a02e49283330a2d4214876e6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631766"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

Ruft die Priorität des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

#### <a name="output"></a>Output

Die zurückgegebene Priorität für diesen Befehl kann wie folgt lauten:

- **Grundes**

- **Hochrangiger**

- **Normaler**

- **Preis**

- **UNKNOWN**

## <a name="examples"></a>Beispiele

So rufen Sie die Priorität für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
