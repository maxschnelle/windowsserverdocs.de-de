---
title: EXEC
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ecdfd05b8abefb35946b783daaa3220a6713a38d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882921"
---
# <a name="exec"></a>EXEC



führt eine Datei auf dem lokalen Computer. Die Datei kann werden eine **Cmd** Skript.

## <a name="syntax"></a>Syntax

```
exec <ScriptFile.cmd>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<ScriptFile.cmd>|Gibt den auszuführenden Skriptdatei an.|

## <a name="remarks"></a>Hinweise

-   Mit diesem Befehl wird verwendet, um doppelte Daten als Teil einer Sicherung wiederherstellen oder restore-Sequenz.
-   Wenn das Skript fehlschlägt, wird ein Fehler zurückgegeben, und DiskShadow beendet.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)