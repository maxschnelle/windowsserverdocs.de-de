---
title: bitsadmin getminretrydelay
description: Windows-Befehle Thema **Bitsadmin Getminretrydelay** -Ruft die Zeitdauer in Sekunden, die der Dienst wartet, nachdem ein vorübergehender Fehler auftritt, bevor Sie versuchen, die Datei zu übertragen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a6df9faab8340994ad9219a863ad8e50186ccd1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832201"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay



Ruft die Zeitdauer in Sekunden, die der Dienst wartet, nachdem ein vorübergehender Fehler auftritt, bevor Sie versuchen, die Datei zu übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetMinRetryDelay <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die minimale wiederholungsverzögerung für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetMinRetryDelay myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)