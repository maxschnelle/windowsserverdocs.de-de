---
title: findstr
description: Referenz Artikel für den findstr-Befehl, der in Dateien nach Textmustern sucht.
ms.topic: reference
ms.assetid: c2d803fb-4cd2-46a1-a1b7-6f5e0249c418
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bdd268c3b2ddde1b42527968252770e6903bacc4
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035128"
---
# <a name="findstr"></a>findstr

Sucht Textmuster in Dateien.

## <a name="syntax"></a>Syntax

```
findstr [/b] [/e] [/l | /r] [/s] [/i] [/x] [/v] [/n] [/m] [/o] [/p] [/f:<file>] [/c:<string>] [/g:<file>] [/d:<dirlist>] [/a:<colorattribute>] [/off[line]] <strings> [<drive>:][<path>]<filename>[ ...]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /b | Entspricht dem Textmuster, wenn es sich am Anfang einer Zeile befindet. |
| /e | Entspricht dem Textmuster, wenn es sich am Ende einer Zeile befindet. |
| /l | Verarbeitet Such Zeichenfolgen buchstäblich. |
| /r | Verarbeitet Such Zeichenfolgen als reguläre Ausdrücke. Dies ist die Standardeinstellung. |
| /s | Durchsucht das aktuelle Verzeichnis und alle Unterverzeichnisse. |
| /i | Ignoriert bei der Suche nach der Zeichenfolge die Groß-/Kleinschreibung der Zeichen. |
| /x | Druckt Zeilen, die exakt übereinstimmen. |
| /v | Druckt nur Zeilen, die keine Entsprechung enthalten. |
| /n | Gibt die Zeilennummer der einzelnen Zeilen aus, die mit übereinstimmen. |
| /m | Druckt nur den Dateinamen, wenn eine Datei eine Entsprechung enthält. |
| /o | Druckt den Zeichen Offset vor jeder übereinstimmenden Zeile. |
| /p | Überspringt Dateien mit nicht druckbaren Zeichen. |
| /Off [Zeile] | Überspringt keine Dateien, für die das Offline-Attribut festgelegt ist. |
| /f`<file>` | Ruft eine Datei Liste aus der angegebenen Datei ab. |
| /c`<string>` | Verwendet den angegebenen Text als Literale Such Zeichenfolge. |
| /g`<file>` | Ruft Such Zeichenfolgen aus der angegebenen Datei ab. |
| /d`<dirlist>` | Durchsucht die angegebene Liste von Verzeichnissen. Jedes Verzeichnis muss durch ein Semikolon (z. b.;) getrennt werden `dir1;dir2;dir3` . |
| /a`<colorattribute>` | Gibt Farb Attribute mit zwei hexadezimal Ziffern an. Geben Sie `color /?` für zusätzliche Informationen ein. |
| `<strings>` | Gibt den Text an, nach dem in *filename*gesucht werden soll. Erforderlich. |
| `[\<drive>:][<path>]<filename>[ ...]` | Gibt den Speicherort und die Datei an, die durchsucht werden sollen. Mindestens ein Dateiname ist erforderlich. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Alle **findstr** -Befehlszeilenoptionen müssen den Zeichen *folgen* und *filename* in der Befehls Zeichenfolge vorangestellt sein.

- Reguläre Ausdrücke verwenden sowohl Literalzeichen als auch Meta-Zeichen, um Textmuster zu suchen, anstelle von exakten Zeichen folgen.

  - Ein Literalzeichen ist ein Zeichen, das in der Syntax für reguläre Ausdrücke keine besondere Bedeutung hat. Stattdessen entspricht er einem Vorkommen dieses Zeichens. Buchstaben und Ziffern sind z. b. Literalzeichen.

  - Ein Meta-Zeichen ist ein Symbol mit spezieller Bedeutung (Operator oder Trennzeichen) in der Syntax für reguläre Ausdrücke.

    Folgende Meta-Zeichen werden akzeptiert:

    | Meta-Zeichen | Wert |
    | -------------- | ----- |
    | `.` | Platz **Halter-** beliebiges Zeichen |
    | `*` | **Wiederholen** Sie 0 (null) oder mehr Vorkommen des vorherigen Zeichens oder der vorherigen Klasse. |
    | `^` | **Zeilen Position** -Anfang der Zeile. |
    | `$` | **Endzeilige Position** -Ende der Zeile. |
    | `[class]` | **Zeichenklasse** -beliebiges Zeichen in einer Menge. |
    | `[^class]` | **Inverse Klasse** -ein beliebiges Zeichen, das nicht in einer Menge vorhanden ist. |
    | `[x-y]` | **Range** -beliebige Zeichen innerhalb des angegebenen Bereichs. |
    | `\x` | Escapeliterale Verwendung eines **Meta-Zeichens** . |
    | `<string` | **Beginn der Wort Position** -Anfang des Worts. |
    | `string>` | Ende der **Wort Position** -Ende des Worts. |

    Die Sonderzeichen in der Syntax regulärer Ausdrücke haben die größte Potenz, wenn Sie Sie gleichzeitig verwenden. Verwenden Sie z. b. die Kombination aus dem Platzhalter Zeichen ( `.` ) und dem Wiederholungs Zeichen ( `*` ), um eine beliebige Zeichenfolge abzugleichen: `.*`

    Verwenden Sie den folgenden Ausdruck als Teil eines größeren Ausdrucks, um eine beliebige Zeichenfolge abzugleichen, die *mit "* *b* " beginnt und mit "" endet`b.*ing`

- Wenn Sie mehrere Zeichen folgen in einem Satz von Dateien suchen möchten, müssen Sie eine Textdatei erstellen, die jedes Suchkriterium in einer separaten Zeile enthält.

- Verwenden Sie Leerzeichen, um mehrere Such Zeichenfolgen zu trennen, **/c**es sei denn, das-Argument weist das

### <a name="examples"></a>Beispiele

Wenn Sie in der Datei *x. y*nach *Hello* oder *dort* suchen möchten, geben Sie Folgendes ein:

```
findstr hello there x.y
```

Geben Sie Folgendes ein, um in der Datei *x. y*nach " *Hello* " zu suchen:

```
findstr /c:hello there x.y
```

Wenn Sie alle Vorkommen der Word- *Fenster* (mit dem ersten Großbuchstaben "W") in der Datei *proposal.txt*suchen möchten, geben Sie Folgendes ein:

```
findstr Windows proposal.txt
```

Geben Sie Folgendes ein, um jede Datei im aktuellen Verzeichnis und alle Unterverzeichnisse zu durchsuchen, die das Word- *Fenster*enthalten, unabhängig vom Buchstaben Fall:

```
findstr /s /i Windows *.*
```

Geben Sie Folgendes ein, um alle Vorkommen von Zeilen zu suchen, die mit *für* und mit 0 (null) oder mehr Leerzeichen (wie in einer Computerprogramm Schleife) beginnen, und um die Zeilennummer anzuzeigen, in der die einzelnen Vorkommen gefunden werden:

```
findstr /b /n /r /c:^ *FOR *.bas
```

Zum Auflisten der Dateien, die Sie in einer Textdatei suchen möchten, verwenden Sie die Suchkriterien in der Datei *stringlist.txt*, um die in *filelist.txt*aufgeführten Dateien zu durchsuchen und die Ergebnisse dann in den Datei Ergebnissen zu speichern *. Geben Sie*Folgendes ein, und geben Sie Folgendes ein:

```
findstr /g:stringlist.txt /f:filelist.txt > results.out
```

Geben Sie Folgendes ein, um jede Datei mit dem Word- *Computer* im aktuellen Verzeichnis und allen Unterverzeichnissen aufzulisten, unabhängig von der Groß-/Kleinschreibung:

```
findstr /s /i /m <computer> *.*
```

Geben Sie Folgendes ein, um alle Dateien mit dem Wort Computer und alle anderen Wörter aufzulisten, die mit Comp beginnen (z. b. "Kompliment" und "konkurrieren"):

```
findstr /s /i /m <comp.* *.*
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)