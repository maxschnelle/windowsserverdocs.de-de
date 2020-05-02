---
title: bitsadmin getpriority
description: Referenz Thema für den bizadmin GetPriority-Befehl, der die Priorität des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 38f92e83ccf5b048d168ce6a21c6026f490b18bf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717679"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

Ruft die Priorität des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

#### <a name="output"></a>Output

Die zurückgegebene Priorität für diesen Befehl kann wie folgt lauten:

- **Grundes**

- **HIGH**

- **Normaler**

- **LOW**

- **UNKNOWN**

## <a name="examples"></a>Beispiele

So rufen Sie die Priorität für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
