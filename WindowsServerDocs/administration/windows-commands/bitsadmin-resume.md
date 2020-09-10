---
title: bitsadmin resume
description: Referenz Artikel für den Befehl bizadmin Resume, der einen neuen oder angehaltenen Auftrag in der Übertragungs Warteschlange aktiviert.
ms.topic: reference
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2ccab242034af3e0b5e01f0efec60d5309879516
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631107"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume

Aktiviert einen neuen oder angehaltenen Auftrag in der Übertragungs Warteschlange. Wenn Sie Ihren Auftrag versehentlich fortsetzen oder den Auftrag einfach aussetzen müssen, können Sie den Schalter [bigsadmin Suspend](bitsadmin-suspend.md) zum Aussetzen des Auftrags verwenden.

## <a name="syntax"></a>Syntax

```
bitsadmin /resume <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So setzen Sie den Auftrag mit dem Namen " *mydownloadjob*" fort

```
bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Suspend"](bitsadmin-suspend.md)

- [Bider admin-Befehl](bitsadmin.md)
