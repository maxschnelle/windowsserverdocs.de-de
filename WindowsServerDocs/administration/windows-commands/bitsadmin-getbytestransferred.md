---
title: bitsadmin getbytestransferred
description: Referenz Thema für den bizadmin getbytestransferred-Befehl, mit dem die Anzahl der für den angegebenen Auftrag übertragenen Bytes abgerufen wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c333926ed46dd2e66e0e2507f838f721a73c192
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718146"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

Ruft die Anzahl der Bytes ab, die für den angegebenen Auftrag übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Anzahl von Bytes ab, die für den Auftrag mit dem Namen *mydownloadjob*übertragen werden

```
bitsadmin /getbytestransferred myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
