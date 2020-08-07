---
title: bitsadmin getpriority
description: Referenz Artikel für den Befehl bizadmin GetPriority, der die Priorität des angegebenen Auftrags abruft.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 57d51e4a2a34fb5ae1361e864ee932ac314662b2
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894033"
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

- **Hochrangiger**

- **Normaler**

- **Preis**

- **UNKNOWN**

## <a name="examples"></a>Beispiele

So rufen Sie die Priorität für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
