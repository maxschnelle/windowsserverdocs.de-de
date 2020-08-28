---
title: bitsadmin cache and setexpirationtime
description: Referenz Artikel für den bitadmin-Cache und den setexpirationtime-Befehl, mit dem die Ablaufzeit für den Cache festgelegt wird.
ms.topic: reference
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e07e862d8577c33daec24bbc93fe5859f13944db
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028808"
---
# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin cache and setexpirationtime

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt die Ablaufzeit für den Cache fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /setexpirationtime secs
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
