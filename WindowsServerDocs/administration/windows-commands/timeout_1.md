---
title: timeout
description: Windows-Befehls Thema für Timeout, bei dem der Befehlsprozessor für die angegebene Anzahl von Sekunden angehalten wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e26b4a84-0e30-46e1-aa10-0667b7d3cb4c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd0a43e49e8a7567ac975333b04a9e6f549a0fd8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832813"
---
# <a name="timeout"></a>timeout

Hält den Befehlsprozessor für die angegebene Anzahl von Sekunden an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
timeout /t <TimeoutInSeconds> [/nobreak] 
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/t \<timeoutinseconds >|Gibt die Dezimalzahl von Sekunden (zwischen-1 und 99999) an, die gewartet wird, bevor der Befehlsprozessor die Verarbeitung fortsetzt. Der Wert-1 bewirkt, dass der Computer unbegrenzt auf eine Tastenkombination wartet.|
|/nobreak|Gibt an, dass Benutzer Tastatur Striche ignoriert werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Der **Timeout** -Befehl wird in der Regel in Batch Dateien verwendet.
-   Eine Benutzer Tastatur wird die Ausführung des Befehls Prozessors sofort fortsetzen, auch wenn der Timeout Zeitraum nicht abgelaufen ist.
-   Bei Verwendung in Verbindung **mit dem Standby** -Befehl ähnelt das **Timeout** dem Befehl **Pause** .

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um den Befehlsprozessor 10 Sekunden lang anzuhalten, geben Sie Folgendes ein:
```
timeout /t 10
```
Um den Befehlsprozessor für 100 Sekunden anzuhalten und Tastatureingaben zu ignorieren, geben Sie Folgendes ein:
```
timeout /t 100 /nobreak
```
Um den Befehlsprozessor unbegrenzt anzuhalten, bis eine Taste gedrückt wird, geben Sie Folgendes ein:
```
timeout /t -1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
