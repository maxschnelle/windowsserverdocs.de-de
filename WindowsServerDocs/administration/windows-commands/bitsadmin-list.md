---
title: bitsadmin list
description: Referenz Artikel für den Befehl bizadmin List, der die Übertragungs Aufträge auflistet, die sich im Besitz des aktuellen Benutzers befinden.
ms.topic: reference
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 81fecf15f16cfa28933b63f9de693ba4e07679e8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631500"
---
# <a name="bitsadmin-list"></a>bitsadmin list

Listet die Übertragungs Aufträge auf, die sich im Besitz des aktuellen Benutzers befinden.

## <a name="syntax"></a>Syntax

```
bitsadmin /list [/allusers][/verbose]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| /ALLUSERS | (Optional) Listet die Aufträge für alle Benutzer auf. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |
| /verbose | (Optional) Stellt ausführliche Informationen zu jedem Auftrag bereit. |

## <a name="examples"></a>Beispiele

Zum Abrufen von Informationen zu Aufträgen, die sich im Besitz des aktuellen Benutzers befinden.

```
bitsadmin /list
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
