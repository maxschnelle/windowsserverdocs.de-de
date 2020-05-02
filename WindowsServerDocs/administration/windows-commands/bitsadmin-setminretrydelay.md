---
title: bitsadmin setminretrydelay
description: Referenz Thema für den BITSAdmin setminretrydelay-Befehl, mit dem die minimale Zeitspanne (in Sekunden), die Bits nach dem Auftreten eines vorübergehenden Fehlers wartet, vor dem Versuch, die Datei zu übertragen, festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7fc54b4466d8f0bac12bd42ebf6c5e2c66087a15
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720123"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
