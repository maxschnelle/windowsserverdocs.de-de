---
title: bitsadmin list
description: Referenz Artikel für den Befehl bizadmin List, der die Übertragungs Aufträge auflistet, die sich im Besitz des aktuellen Benutzers befinden.
ms.topic: reference
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e1d36a9236c834cea76e653b9a2e639c3b8f964e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024374"
---
# <a name="bitsadmin-list"></a>bitsadmin list

Listet die Übertragungs Aufträge auf, die sich im Besitz des aktuellen Benutzers befinden.

## <a name="syntax"></a>Syntax

```
bitsadmin /list [/allusers][/verbose]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
