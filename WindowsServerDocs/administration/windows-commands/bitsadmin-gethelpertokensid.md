---
title: bitsadmin gethelpertokensid
description: Referenz Artikel für den Befehl "BITSAdmin gethelpertokensid", der die sid für das Hilfsobjekt eines Bits-Übertragungs Auftrags zurückgibt, sofern ein solcher festgelegt ist.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 742c009d1625fe5ba755367a2a93310627d10550
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894234"
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
