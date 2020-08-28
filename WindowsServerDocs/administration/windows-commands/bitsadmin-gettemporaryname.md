---
title: bitsadmin gettemporaryname
description: Referenz Artikel für den bizadmin gettemporaryname-Befehl, der den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags meldet.
ms.topic: reference
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d9e03b00fa1885b89f25dab2781ce988aa0c5df8
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034808"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin gettemporaryname

Meldet den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /gettemporaryname <job> <file_index>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| file_index | Beginnt bei 0. |

## <a name="examples"></a>Beispiele

So melden Sie den temporären Dateinamen von Datei 2 für den Auftrag *mydownloadjob*:

```
bitsadmin /gettemporaryname myDownloadJob 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
