---
title: more
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ded14f6a-d82f-4aeb-a2d8-7ec1c94dfb8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 93ba6c696c509ea20ffe8f680d4416d24d202b89
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437315"
---
# <a name="more"></a>more



Es wird ein Bildschirm mit der Ausgabe zu einem Zeitpunkt.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
<Command> | more [/c] [/p] [/s] [/t<N>] [+<N>]
more [[/c] [/p] [/s] [/t<N>] [+<N>]] < [<Drive>:][<Path>]<FileName>
more [/c] [/p] [/s] [/t<N>] [+<N>] [<Files>]
```

## <a name="parameters"></a>Parameter

|           Parameter            |                               Beschreibung                               |
|--------------------------------|-------------------------------------------------------------------------|
|           \<Befehl >           |      Gibt einen Befehl für den in der Ausgabe angezeigt werden sollen.      |
|               /c               |               Löscht den Bildschirm vor der Anzeige einer Seite an.               |
|               /p               |                      Wird erweitert, Zeichen.                      |
|               /s               |          Zeigt mehrere leere Zeilen als einzelne Zeile leer.          |
|             /t\<N>             |         Werden Registerkarten angezeigt wird, als die angegebene Anzahl von Leerzeichen durch *N*.         |
|             +\<N>              |     Zeigt den Anfang der ersten Datei in der Zeile, die anhand des *N*.     |
| [\<Drive>:] [<Path>]<FileName> |          Gibt den Speicherort und Namen einer Datei angezeigt.          |
|            \<Dateien >            | Gibt eine Liste der Dateien angezeigt. Trennen Sie Namen durch ein Leerzeichen ein. |
|               /?               |                  Zeigt die Hilfe an der Eingabeaufforderung an.                   |

## <a name="remarks"></a>Hinweise

-   Die folgenden Unterbefehle akzeptiert werden, auf die **weitere** Eingabeaufforderung (`-- More --`).  
    |Key|Aktion|
    |---|------|
    |SPACEBAR|Zeigt die nächste Seite.|
    |EINGABETASTE|Zeigt die nächste Zeile.|
    |f|Zeigt die nächste Datei.|
    |q|Beendet die **weitere** Befehl.|
    |=|Zeigt die Nummer der Zeile an.|
    |p \<N>|Zeigt die nächste *N* Zeilen.|
    |s \<N>|Überspringt die nächste *N* Zeilen.|
    |?|Zeigt die Befehle, die unter der **weitere** Eingabeaufforderung.|
– Wenn Sie das Umleitungszeichen verwenden ( **<** ), müssen Sie einen Dateinamen als Quelle angeben. Wenn Sie die Pipe zu verwenden (**|*), können Sie diese Befehle als **Dir**, **Sortierreihenfolge**, und **Typ**.
-   Die **weitere** -Befehl, mit verschiedenen Parametern finden Sie in der Wiederherstellungskonsole.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie zum Anzeigen der ersten Seite des Informationen einer Datei mit dem Namen Kunden.neu einen der folgenden Befehle aus:
```
more < clients.new
type clients.new | more
```
Die **weitere** Befehl zeigt den ersten Bildschirm von Informationen aus dem Kunden.neu und zeigt dann die folgende Aufforderung:
```
-- More --
```
Drücken Sie dann die LEERTASTE, um dem nächsten Bildschirm des Informationen finden Sie unter.

Deaktivieren Sie den Bildschirm, und entfernen Sie alle zusätzliche leere Zeilen vor der Anzeige der Datei Kunden.neu, geben Sie einen der folgenden Befehle aus:
```
more /c /s < clients.new
type clients.new | more /c /s
```
Die **weitere** Befehl zeigt den ersten Bildschirm von Informationen aus dem Kunden.neu und zeigt dann die folgende Aufforderung:
```
-- More --
```

### <a name="using-more-subcommands"></a>Verwenden mehrere Unterbefehle

In den folgenden Beispielen können verwendet werden, auf die **weitere** Eingabeaufforderung (`-- More --`).
- Um die Datei eine Zeile zu einem Zeitpunkt anzuzeigen, drücken Sie die EINGABETASTE auf der **weitere** Eingabeaufforderung.
- Drücken Sie die LEERTASTE an, um dem nächsten Bildschirm anzuzeigen, die **weitere** Eingabeaufforderung.
- Geben Sie zum Anzeigen der nächsten Datei aufgeführt, die in der Befehlszeile **f** an die **weitere** Eingabeaufforderung.
- Geben Sie zum Anzeigen der verfügbaren Befehle **?** auf der **weitere** Eingabeaufforderung.
- Um den Vorgang abzubrechen **weitere**, Typ **q** an die **weitere** Eingabeaufforderung.
- Um die aktuelle Zeilennummer anzuzeigen, geben **=** an die **weitere** Eingabeaufforderung. Die aktuelle Zeilennummer wird hinzugefügt, um die **weitere** Eingabeaufforderung wie folgt:  
  ```
  -- More [Line: 24] --
  ```  
- Geben Sie zum Anzeigen einer bestimmten Anzahl von Zeilen **p** an die **weitere** Eingabeaufforderung. **Weitere** aufgefordert, für die Anzahl der Zeilen, die wie folgt angezeigt:  
  ```
  -- More -- Lines:
  ```  
  Geben Sie die Anzahl der anzuzeigenden Zeilen an, und drücken Sie dann die EINGABETASTE. **Weitere** zeigt die angegebene Anzahl von Zeilen.
- Um eine bestimmte Anzahl von Zeilen zu überspringen, geben Sie **s** an die **weitere** Eingabeaufforderung. **Weitere** aufgefordert, für die Anzahl der Zeilen, die wie folgt überspringen:  
  ```
  -- More -- Lines:
  ```  
  Geben Sie die Anzahl der zu überspringenden Zeilen an, und drücken Sie dann die EINGABETASTE. **Weitere** überspringt die angegebene Anzahl von Zeilen und den nächsten Bildschirm des Informationen angezeigt.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)