---
title: bitsadmin getcompletiontime
description: Windows-Befehle Thema **Bitsadmin Getcompletiontime** -Ruft die Uhrzeit an, dass der Auftrag beendet wurde, Übertragen von Daten ab.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3790a91c4b347b982c0f0a023d5977a8d6cd1f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857381"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime



Ruft die Zeit, dass der Auftrag beendet wurde, Übertragen von Daten ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetCompletionTime <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Zeit, die der Auftrag mit dem Namen *MyDownloadJob* übertragen von Daten beendet wurde.
```
C:\>bitsadmin /GetCompletionTime myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)