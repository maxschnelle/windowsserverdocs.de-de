---
title: bitsadmin gethelpertokensid
description: Referenz Artikel für den Befehl "BITSAdmin gethelpertokensid", der die sid für das Hilfsobjekt eines Bits-Übertragungs Auftrags zurückgibt, sofern ein solcher festgelegt ist.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 645957ab5526c98e806a4e7875e1baece3d375b3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632043"
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

| Parameter | BESCHREIBUNG |
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
