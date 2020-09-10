---
title: biout admin Cache und DeleteUrl
description: Referenz Artikel für den bizadmin-Cache und den DeleteUrl-Befehl, der alle Cache Einträge für die angegebene URL löscht.
ms.topic: reference
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6e1c3af4cfbb6c1ef21a86ead6d3975bf1f44cf6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632620"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>biout admin Cache und DeleteUrl

Löscht alle Cache Einträge für die angegebene URL.

## <a name="syntax"></a>Syntax

```
bitsadmin /deleteURL URL
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| URL | Der Uniform Resource Locator, der eine Remote Datei identifiziert. |

## <a name="examples"></a>Beispiele

So löschen Sie alle Cache Einträge für `https://www.contoso.com/en/us/default.aspx` :

```
bitsadmin /deleteURL https://www.contoso.com/en/us/default.aspx
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Cache"](bitsadmin-cache.md)
