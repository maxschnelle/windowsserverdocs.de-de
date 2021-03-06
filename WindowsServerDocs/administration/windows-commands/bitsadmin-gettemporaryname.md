---
title: bitsadmin gettemporaryname
description: Referenz Artikel für den bizadmin gettemporaryname-Befehl, der den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags meldet.
ms.topic: reference
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9eeaf3c1093cf147c945bb029e5652db1819003c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631590"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin gettemporaryname

Meldet den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /gettemporaryname <job> <file_index>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| file_index | Beginnt bei 0. |

## <a name="examples"></a>Beispiele

So melden Sie den temporären Dateinamen von Datei 2 für den Auftrag *mydownloadjob*:

```
bitsadmin /gettemporaryname myDownloadJob 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
