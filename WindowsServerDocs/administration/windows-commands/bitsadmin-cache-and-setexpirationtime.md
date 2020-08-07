---
title: bitsadmin cache and setexpirationtime
description: Referenz Artikel für den bitadmin-Cache und den setexpirationtime-Befehl, mit dem die Ablaufzeit für den Cache festgelegt wird.
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 367088525366707797296d844f134dcf8a02def7
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894735"
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
