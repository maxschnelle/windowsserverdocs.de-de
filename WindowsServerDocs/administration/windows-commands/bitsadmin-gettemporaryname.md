---
title: bitsadmin gettemporaryname
description: Referenz Artikel für den bizadmin gettemporaryname-Befehl, der den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags meldet.
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b5919d45f2b8497bb6e8fa6cf3650f49e27cd48
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893833"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin gettemporaryname

Meldet den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /gettemporaryname <job> <file_index>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
