---
title: timeout
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e26b4a84-0e30-46e1-aa10-0667b7d3cb4c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3997399b732c494050797c83a0a52938574986bd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830171"
---
# <a name="timeout"></a>timeout



Hält den Befehlsprozessor für die angegebene Anzahl von Sekunden an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
timeout /t <TimeoutInSeconds> [/nobreak] 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/t \<TimeoutInSeconds>|Gibt die Dezimalzahl in Sekunden (zwischen 1 und 99999) zum Warten, bevor der Befehlsprozessor Verarbeitung wird fortgesetzt. Der Wert-1 wird den Computer, um unbegrenzt zu warten, bis eine Tastatureingabe.|
|/nobreak|Gibt an, um Benutzer Tastenanschläge zu ignorieren.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die **Timeout** Befehl wird in der Regel in Batchdateien verwendet.
-   Tastenanschlag durch einen Benutzer wird die Ausführung des Befehls Prozessor sofort fortgesetzt, selbst wenn das Timeout nicht abgelaufen ist.
-   Bei Verwendung in Verbindung mit der **Standbymodus** Befehl **Timeout** ist vergleichbar mit der **anhalten** Befehl.

## <a name="BKMK_examples"></a>Beispiele für

Um den Befehlsprozessor zehn Sekunden lang angehalten, geben Sie Folgendes ein:
```
timeout /t 10
```
Um den Befehlsprozessor für 100 Sekunden angehalten und tastatureingabeprotokollierung ignorieren, geben Sie Folgendes ein:
```
timeout /t 100 /nobreak
```
Um den Befehlsprozessor anzuhalten, bis eine Taste gedrückt wird, geben Sie Folgendes ein:
```
timeout /t -1
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
