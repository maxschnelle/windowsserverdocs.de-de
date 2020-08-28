---
title: bitsadmin getpriority
description: Referenz Artikel für den Befehl bizadmin GetPriority, der die Priorität des angegebenen Auftrags abruft.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 2aeff973b0ca285cc8c9852f284e314879f8de02
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028698"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

Ruft die Priorität des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
