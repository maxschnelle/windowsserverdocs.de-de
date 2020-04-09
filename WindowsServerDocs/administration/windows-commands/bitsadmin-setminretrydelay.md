---
title: bitsadmin setminretrydelay
description: Windows-Befehls Thema für BITSAdmin setminretrydelay, das die minimale Zeitspanne in Sekunden angibt, nach der ein vorübergehender Fehler auftritt, bevor versucht wird, die Datei zu übertragen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb2fe4c6d0e4f90c6ec49fa1da63404393d4f634
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849363"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

Legt die minimale Zeitspanne (in Sekunden) fest, die Bits nach dem Auftreten eines vorübergehenden Fehlers wartet, bevor versucht wird, die Datei zu übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetMinRetryDelay <Job> <RetryDelay>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|RetryDelay|Eine Zahl, die in Sekunden dargestellt wird.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die minimale Wiederholungs Verzögerung für den Auftrag *mydownloadjob* auf 35 Sekunden festgelegt.
```
C:\>bitsadmin /SetMinRetryDelay myDownloadJob 35
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)