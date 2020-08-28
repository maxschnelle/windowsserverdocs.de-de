---
title: bitsadmin gethelpertokensid
description: Referenz Artikel für den Befehl "BITSAdmin gethelpertokensid", der die sid für das Hilfsobjekt eines Bits-Übertragungs Auftrags zurückgibt, sofern ein solcher festgelegt ist.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 9cfa2c2a10d1f3947374262bbeb9ab21e559cfee
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033548"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gethelpertokensid

Gibt die sid für das [Hilfsobjekt](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)eines Bits-Übertragungs Auftrags zurück, sofern ein solches festgelegt ist.

> [!NOTE]
> Dieser Befehl wird von Bits 3,0 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /gethelpertokensid <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die SID eines Bits-Übertragungs Auftrags mit dem Namen *mydownloadjob*ab

```
bitsadmin /gethelpertokensid myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
