---
title: bitsadmin geterror
description: Referenz Artikel für den bizadmin getError-Befehl, mit dem ausführliche Fehlerinformationen für den angegebenen Auftrag abgerufen werden.
ms.topic: reference
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1cfa4c5a7d0899e2d5eb34fd089944f2b801993a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632124"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

Ruft ausführliche Fehlerinformationen für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen der Fehlerinformationen für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
