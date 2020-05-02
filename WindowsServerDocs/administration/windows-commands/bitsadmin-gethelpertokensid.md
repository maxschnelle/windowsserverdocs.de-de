---
title: bitsadmin gethelpertokensid
description: Referenz Thema für den BITSAdmin gethelpertokensid-Befehl, der die sid für das Hilfsobjekt eines Bits-Übertragungs Auftrags zurückgibt, sofern ein solcher festgelegt ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: c45bf86d8a7364289db41fa390f319270a2a8386
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717894"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gethelpertokensid

Gibt die sid für das [Hilfsobjekt](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)eines Bits-Übertragungs Auftrags zurück, sofern ein solches festgelegt ist.

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
