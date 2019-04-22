---
title: bitsadmin setminretrydelay
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 640492cf690a934e3e3b8d0ecf8ca7a0d6a7dc2f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813081"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

Legt der minimalen Länge der Zeit in Sekunden fest, dass BITS wartet, nachdem ein vorübergehender Fehler auftritt, bevor Sie versuchen, die Datei zu übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetMinRetryDelay <Job> <RetryDelay>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|RetryDelay|Eine Zahl, ausgedrückt in Sekunden.|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die minimale wiederholungsverzögerung für den Auftrag mit dem Namen *MyDownloadJob* , 35 Sekunden.
```
C:\>bitsadmin /SetMinRetryDelay myDownloadJob 35
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)