---
title: bitsadmin getfilestotal
description: Referenz Artikel für den bizadmin getfilestotal-Befehl, mit dem die Anzahl der Dateien im angegebenen Auftrag abgerufen wird.
ms.topic: reference
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 73a543914f31a7b9e5b028caf273d7945a954fdd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632108"
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
