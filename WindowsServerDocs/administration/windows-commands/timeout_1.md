---
title: timeout
description: Referenz Artikel für Timeout, bei dem der Befehlsprozessor für die angegebene Anzahl von Sekunden angehalten wird.
ms.topic: reference
ms.assetid: e26b4a84-0e30-46e1-aa10-0667b7d3cb4c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4905eaadc745fc5499cb393b1808794e2f803361
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038258"
---
# <a name="timeout"></a>timeout

Hält den Befehlsprozessor für die angegebene Anzahl von Sekunden an.



## <a name="syntax"></a>Syntax

```
timeout /t <TimeoutInSeconds> [/nobreak]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/t \<TimeoutInSeconds>|Gibt die Dezimalzahl von Sekunden (zwischen-1 und 99999) an, die gewartet wird, bevor der Befehlsprozessor die Verarbeitung fortsetzt. Der Wert-1 bewirkt, dass der Computer unbegrenzt auf eine Tastenkombination wartet.|
|/nobreak|Gibt an, dass Benutzer Tastatur Striche ignoriert werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Der **Timeout** -Befehl wird in der Regel in Batch Dateien verwendet.
-   Eine Benutzer Tastatur wird die Ausführung des Befehls Prozessors sofort fortsetzen, auch wenn der Timeout Zeitraum nicht abgelaufen ist.
-   Bei Verwendung in Verbindung **mit dem Standby** -Befehl ähnelt das **Timeout** dem Befehl **Pause** .

## <a name="examples"></a>Beispiele

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
