---
title: bitsadmin getcompletiontime
description: Referenz Artikel für den bizadmin getcompletiontime-Befehl, der den Zeitpunkt abruft, zu dem der Auftrag das Übertragen von Daten abgeschlossen hat.
ms.topic: reference
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d79fbf49aa4ec9cea60829a3b0859887da0e5dd5
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033678"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime

Ruft den Zeitpunkt ab, zu dem der Auftrag die Datenübertragung abgeschlossen hat.

## <a name="syntax"></a>Syntax

```
bitsadmin /getcompletiontime <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
