---
title: bitsadmin setminretrydelay
description: Referenz Artikel für den Befehl "BITSAdmin setminretrydelay", mit dem die minimale Zeitdauer (in Sekunden) festgelegt wird, nach der ein vorübergehender Fehler auftritt, bevor versucht wird, die Datei zu übertragen.
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 448e03805f30af50abffa28365e456028598ae1a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893075"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

Legt die minimale Zeitspanne (in Sekunden) fest, die Bits nach dem Auftreten eines vorübergehenden Fehlers wartet, bevor versucht wird, die Datei zu übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /setminretrydelay <job> <retrydelay>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
