---
title: bitsadmin getcompletiontime
description: Referenz Artikel für den bizadmin getcompletiontime-Befehl, der den Zeitpunkt abruft, zu dem der Auftrag das Übertragen von Daten abgeschlossen hat.
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a242ec3689bef6e4ecd2bb961f532efbb874e98c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894476"
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
