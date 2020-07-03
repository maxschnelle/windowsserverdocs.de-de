---
title: bitsadmin cache and setexpirationtime
description: Referenz Artikel für den bitadmin-Cache und den setexpirationtime-Befehl, mit dem die Ablaufzeit für den Cache festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60372a74acc6ea5312afb5dafcb3ab7b3299f4d2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923256"
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
