---
title: exec
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f10e28a8da96bc7228af4561fb36824899f2d7a4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725740"
---
# <a name="exec"></a>exec



Führt eine Datei auf dem lokalen Computer aus. Bei der Datei kann es sich um ein **cmd** -Skript handeln.

## <a name="syntax"></a>Syntax

```
exec <ScriptFile.cmd>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<> "scriptfile. cmd"|Gibt die auszuführende Skriptdatei an.|

## <a name="remarks"></a>Bemerkungen

-   Dieser Befehl wird verwendet, um Daten im Rahmen einer Sicherungs-oder Wiederherstellungs Sequenz zu duplizieren oder wiederherzustellen.
-   Wenn das Skript fehlschlägt, wird ein Fehler zurückgegeben, und DiskShadow wird beendet.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)