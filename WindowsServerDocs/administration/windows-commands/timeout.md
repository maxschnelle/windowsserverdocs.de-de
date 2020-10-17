---
title: timeout
description: Referenz Artikel für den Timeout-Befehl, der den Befehlsprozessor für die angegebene Anzahl von Sekunden anhält.
ms.topic: reference
ms.assetid: e26b4a84-0e30-46e1-aa10-0667b7d3cb4c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: edb4d14614099b0e501df175e619285928344c78
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156719"
---
# <a name="timeout"></a>timeout

Hält den Befehlsprozessor für die angegebene Anzahl von Sekunden an. Dieser Befehl wird in der Regel in Batch Dateien verwendet.

## <a name="syntax"></a>Syntax

```
timeout /t <timeoutinseconds> [/nobreak]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /t `<timeoutinseconds>` | Gibt die Dezimalzahl von Sekunden (zwischen-1 und 99999) an, die gewartet wird, bevor der Befehlsprozessor die Verarbeitung fortsetzt. Der Wert **-1** bewirkt, dass der Computer unbegrenzt auf eine Tastenkombination wartet. |
| /nobreak | Gibt an, dass Benutzer Tastatur Striche ignoriert werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Eine Benutzer Tastatur wird die Ausführung des Befehls Prozessors sofort fortsetzen, auch wenn der Timeout Zeitraum nicht abgelaufen ist.

- Bei Verwendung in Verbindung mit **dem standbytool des** ressourcenkits ähnelt das **Timeout** dem Befehl **Pause** .

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
