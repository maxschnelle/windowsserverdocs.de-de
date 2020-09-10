---
title: bitsadmin cancel
description: Referenz Artikel für den Befehl bizadmin Cancel, der den Auftrag aus der Übertragungs Warteschlange entfernt und alle dem Auftrag zugeordneten temporären Dateien löscht.
ms.topic: reference
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4ef8810b04141b41851f029f6cde4586b89a90d4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632420"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

Entfernt den Auftrag aus der Übertragungs Warteschlange und löscht alle temporären Dateien, die dem Auftrag zugeordnet sind.

## <a name="syntax"></a>Syntax

```
bitsadmin /cancel <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So entfernen Sie den Auftrag " *mydownloadjob* " aus der Übertragungs Warteschlange:

```
bitsadmin /cancel myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
