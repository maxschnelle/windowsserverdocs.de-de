---
title: bitsadmin getcompletiontime
description: Referenz Artikel für den bizadmin getcompletiontime-Befehl, der den Zeitpunkt abruft, zu dem der Auftrag das Übertragen von Daten abgeschlossen hat.
ms.topic: reference
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 660a28dcfe99bd5801ba2fc3ad909cec78a671ce
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632240"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime

Ruft den Zeitpunkt ab, zu dem der Auftrag die Datenübertragung abgeschlossen hat.

## <a name="syntax"></a>Syntax

```
bitsadmin /getcompletiontime <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Zeit ab, zu der der Auftrag mit dem Namen *mydownloadjob* die Datenübertragung abgeschlossen hat

```
bitsadmin /getcompletiontime myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
