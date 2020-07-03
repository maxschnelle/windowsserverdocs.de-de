---
title: bitsadmin list
description: Referenz Artikel für den Befehl bizadmin List, der die Übertragungs Aufträge auflistet, die sich im Besitz des aktuellen Benutzers befinden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d9a2c86536ff0910b4e0a8bea15ec43d9371087
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926556"
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
| /ALLUSERS | Dies ist optional. Listet die Aufträge für alle Benutzer auf. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |
| /verbose | Dies ist optional. Stellt ausführliche Informationen zu jedem Auftrag bereit. |

## <a name="examples"></a>Beispiele

Zum Abrufen von Informationen zu Aufträgen, die sich im Besitz des aktuellen Benutzers befinden.

```
bitsadmin /list
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
