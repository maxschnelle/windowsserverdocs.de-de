---
title: bitsadmin cache and setexpirationtime
description: Referenz Artikel für den bitadmin-Cache und den setexpirationtime-Befehl, mit dem die Ablaufzeit für den Cache festgelegt wird.
ms.topic: reference
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0d9bc67292796afdbcec695ea2e65966b5b5e46d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632531"
---
# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin cache and setexpirationtime

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt die Ablaufzeit für den Cache fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /setexpirationtime secs
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Sekunden | Die Anzahl der Sekunden bis zum Ablauf des Caches. |

## <a name="examples"></a>Beispiele

So legen Sie fest, dass der Cache in 60 Sekunden abläuft:

```
bitsadmin /cache / setexpirationtime 60
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Cache"](bitsadmin-cache.md)
