---
title: bitsadmin getcompletiontime
description: Referenz Artikel für den bizadmin getcompletiontime-Befehl, der den Zeitpunkt abruft, zu dem der Auftrag das Übertragen von Daten abgeschlossen hat.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e07dd6a345cd1bd58277ef08e08802a62d6e6772
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923106"
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
