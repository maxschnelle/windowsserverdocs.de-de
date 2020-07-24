---
title: bitsadmin gethelpertokensid
description: Referenz Artikel für den Befehl "BITSAdmin gethelpertokensid", der die sid für das Hilfsobjekt eines Bits-Übertragungs Auftrags zurückgibt, sofern ein solcher festgelegt ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 3c8ef7502c524994454c697e2fa7d5dee223da5d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955462"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
