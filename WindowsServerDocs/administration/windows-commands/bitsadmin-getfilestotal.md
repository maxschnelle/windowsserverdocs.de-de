---
title: bitsadmin getfilestotal
description: Referenz Thema für den bizadmin getfilestotal-Befehl, mit dem die Anzahl der Dateien im angegebenen Auftrag abgerufen wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5cf3b33c15bb18c8a141408f82fdd72a6e710817
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717978"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal

Ruft die Anzahl der Dateien im angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getfilestotal <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Anzahl der Dateien ab, die im Auftrag mit dem Namen *mydownloadjob*enthalten sind:

```
bitsadmin /getfilestotal myDownloadJob
```

## <a name="see-also"></a>Weitere Informationen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
