---
title: bitsadmin getpriority
description: Referenz Artikel für den Befehl bizadmin GetPriority, der die Priorität des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 39ce769e2eb1dcf7a05d416dc2a66c6c082c9ae4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926855"
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

#### <a name="output"></a>Ausgabe

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
