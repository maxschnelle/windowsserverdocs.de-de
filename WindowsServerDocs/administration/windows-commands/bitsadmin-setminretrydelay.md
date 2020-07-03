---
title: bitsadmin setminretrydelay
description: Referenz Artikel für den Befehl "BITSAdmin setminretrydelay", mit dem die minimale Zeitdauer (in Sekunden) festgelegt wird, nach der ein vorübergehender Fehler auftritt, bevor versucht wird, die Datei zu übertragen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a28bdcc90fdeee4d5173272c8670f9d0bff3c0a0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927688"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

Legt die minimale Zeitspanne (in Sekunden) fest, die Bits nach dem Auftreten eines vorübergehenden Fehlers wartet, bevor versucht wird, die Datei zu übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /setminretrydelay <job> <retrydelay>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| retrydelay | Mindestzeitdauer für Bits, die nach einem Fehler während der Übertragung gewartet werden (in Sekunden). |

## <a name="examples"></a>Beispiele

So legen Sie die minimale Wiederholungs Verzögerung auf 35 Sekunden für den Auftrag *mydownloadjob*fest:

```
bitsadmin /setminretrydelay myDownloadJob 35
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
