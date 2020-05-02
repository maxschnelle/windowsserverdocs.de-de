---
title: bitsadmin gettemporaryname
description: Referenz Thema für den bizadmin gettemporaryname-Befehl, der den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags meldet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7780691f37fb78f1553fa993fd408d224be39ff
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717484"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
