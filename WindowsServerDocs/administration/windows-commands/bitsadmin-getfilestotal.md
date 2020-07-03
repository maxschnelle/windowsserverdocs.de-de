---
title: bitsadmin getfilestotal
description: Referenz Artikel für den bizadmin getfilestotal-Befehl, mit dem die Anzahl der Dateien im angegebenen Auftrag abgerufen wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7592f783d17e31fe8a1e7fbf82cb41e20171c9fd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928281"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal

Ruft die Anzahl der Dateien im angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getfilestotal <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
