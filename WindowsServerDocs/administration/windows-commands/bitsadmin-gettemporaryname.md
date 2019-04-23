---
title: Bitsadmin gettemporaryname
description: Windows-Befehle Thema **Bitsadmin Gettemporaryname** -gibt den temporären Dateinamen, der die angegebene Datei innerhalb des Auftrags.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 762a2a5943202b38e94a245b74745e6631e0792d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876711"
---
# <a name="bitsadmin-gettemporaryname"></a>Bitsadmin gettemporaryname



Gibt den temporären Dateinamen, der die angegebene Datei innerhalb des Auftrags an.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetTemporaryName <Job> <file index> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Datei-index|Beginnt bei 0|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel gibt den temporären Dateinamen der Datei "2" für den Auftrag mit dem Namen *MyJob*.
```
C:\>bitsadmin /GetTemporaryName myJob 1 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)