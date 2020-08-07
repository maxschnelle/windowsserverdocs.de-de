---
title: bitsadmin list
description: Referenz Artikel für den Befehl bizadmin List, der die Übertragungs Aufträge auflistet, die sich im Besitz des aktuellen Benutzers befinden.
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b4bf346cd52e09d81bfbb934df86b94b9b544aa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893707"
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
| /ALLUSERS | Optional. Listet die Aufträge für alle Benutzer auf. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |
| /verbose | Optional. Stellt ausführliche Informationen zu jedem Auftrag bereit. |

## <a name="examples"></a>Beispiele

Zum Abrufen von Informationen zu Aufträgen, die sich im Besitz des aktuellen Benutzers befinden.

```
bitsadmin /list
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
