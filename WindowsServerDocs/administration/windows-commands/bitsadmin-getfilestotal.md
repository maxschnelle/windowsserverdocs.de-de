---
title: bitsadmin getfilestotal
description: Referenz Artikel für den bizadmin getfilestotal-Befehl, mit dem die Anzahl der Dateien im angegebenen Auftrag abgerufen wird.
ms.topic: reference
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 74e5dad863b12b7f90ed74bca0e6b0b352fb1360
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033608"
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
