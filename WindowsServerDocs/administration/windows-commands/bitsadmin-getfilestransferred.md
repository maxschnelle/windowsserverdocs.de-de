---
title: bitsadmin getfilestransferred
description: Referenz Thema für den bizadmin getfilestransferred-Befehl, der die Anzahl der für den angegebenen Auftrag übertragenen Dateien abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed11739029338ecce5fc4efbe1918873a7f37f62
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717915"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred

Ruft die Anzahl der Dateien ab, die für den angegebenen Auftrag übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getfilestransferred <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Anzahl der Dateien ab, die im Auftrag mit dem Namen *mydownloadjob*übertragen wurden:

```
bitsadmin /getfilestransferred myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
