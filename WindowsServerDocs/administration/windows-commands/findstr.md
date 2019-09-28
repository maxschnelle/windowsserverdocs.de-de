---
title: findstr
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c2d803fb-4cd2-46a1-a1b7-6f5e0249c418
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 547a0abf658ef826cca8c87d451144181f8dac7d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377191"
---
# <a name="findstr"></a>findstr

Sucht Textmuster in Dateien.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
findstr [/b] [/e] [/l | /r] [/s] [/i] [/x] [/v] [/n] [/m] [/o] [/p] [/f:<File>] [/c:<String>] [/g:<File>] [/d:<DirList>] [/a:<ColorAttribute>] [/off[line]] <Strings> [<Drive>:][<Path>]<FileName>[ ...]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/b|Entspricht dem Textmuster, wenn es sich am Anfang einer Zeile befindet.|
|/e|Entspricht dem Textmuster, wenn es sich am Ende einer Zeile befindet.|
|/l|Verarbeitet Such Zeichenfolgen buchstäblich.|
|/r|Verarbeitet Such Zeichenfolgen als reguläre Ausdrücke. Dies ist die Standardeinstellung.|
|/s|Durchsucht das aktuelle Verzeichnis und alle Unterverzeichnisse.|
|/i|Ignoriert bei der Suche nach der Zeichenfolge die Groß-/Kleinschreibung der Zeichen.|
|/x|Druckt Zeilen, die exakt übereinstimmen.|
|/v|Druckt nur Zeilen, die keine Entsprechung enthalten.|
|/n|Gibt die Zeilennummer der einzelnen Zeilen aus, die mit übereinstimmen.|
|/m|Druckt nur den Dateinamen, wenn eine Datei eine Entsprechung enthält.|
|/o|Druckt den Zeichen Offset vor jeder übereinstimmenden Zeile.|
|/p|Überspringt Dateien mit nicht druckbaren Zeichen.|
|/Off [Zeile]|Überspringt keine Dateien, für die das Offline-Attribut festgelegt ist.|
|/f: @no__t 0datei >|Ruft eine Datei Liste aus der angegebenen Datei ab.|
|/c: \<string >|Verwendet den angegebenen Text als Literale Such Zeichenfolge.|
|/g: @no__t 0datei >|Ruft Such Zeichenfolgen aus der angegebenen Datei ab.|
|/d: \<dirlist >|Durchsucht die angegebene Liste von Verzeichnissen. Jedes Verzeichnis muss durch ein Semikolon (z. b.;) `dir1;dir2;dir3`) getrennt werden.|
|/a: \<colorattribute >|Gibt Farb Attribute mit zwei hexadezimal Ziffern an. Geben Sie für weitere Informationen `color /?` ein.|
|\<strings >|Gibt den Text an, nach dem in *filename*gesucht werden soll. Erforderlich.|
|[\<laufwerk >:] [<Path>] <FileName> [...]|Gibt den Speicherort und die Datei an, die durchsucht werden sollen. Mindestens ein Dateiname ist erforderlich.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Alle **findstr** -Befehlszeilenoptionen müssen den Zeichen *folgen* und *filename* in der Befehls Zeichenfolge vorangestellt sein.
- Reguläre Ausdrücke verwenden sowohl Literalzeichen als auch Metazeichen, um Textmuster zu suchen, anstelle von exakten Zeichen folgen. Ein Literalzeichen ist ein Zeichen, das in der Syntax für reguläre Ausdrücke keine besondere Bedeutung hat – es entspricht einem Vorkommen dieses Zeichens. Buchstaben und Ziffern sind z. b. Literalzeichen. Ein Metazeichen ist ein Symbol mit spezieller Bedeutung (Operator oder Trennzeichen) in der Syntax für reguläre Ausdrücke.

  In der folgenden Tabelle werden die Metazeichen aufgelistet, die von **findstr** akzeptiert werden.  

  |Metazeichen|Wert|
  |-------------|-----|
  |.|Platzhalter Zeichen: beliebiges Zeichen|
  |*|Wiederholung: NULL oder mehr Vorkommen des vorherigen Zeichens oder der vorherigen Klasse|
  |^|Zeilen Position: Zeilen Anfang|
  |$|Zeilen Position: Ende der Zeile|
  |klassi|Zeichenklasse: beliebiges Zeichen in einer Menge|
  |[^-Klasse]|Inverse Klasse: ein beliebiges Zeichen, das nicht in einer Menge vorhanden ist|
  |[x-y]|Range: beliebige Zeichen innerhalb des angegebenen Bereichs|
  |\x|Escape: Literale Verwendung eines Metazeichens x|
  |\\ < Zeichenfolge|Word-Position: Anfang des Worts|
  |Zeichenfolge @ no__t-0|Word-Position: Ende des Worts|

  Die Sonderzeichen in der Syntax regulärer Ausdrücke haben die größte Potenz, wenn Sie Sie gleichzeitig verwenden. Verwenden Sie beispielsweise die folgende Kombination aus dem Platzhalter Zeichen (.) und dem Wiederholungs Zeichen (*), um eine beliebige Zeichenfolge abzugleichen:

  ```
  .*
  ``` 

  Verwenden Sie den folgenden Ausdruck als Teil eines größeren Ausdrucks, um eine beliebige Zeichenfolge abzugleichen, die mit "b" beginnt und mit "ung" endet: 

  ```
  b.*ing
  ```

## <a name="examples"></a>Beispiele

Verwenden Sie Leerzeichen, um mehrere Such Zeichenfolgen zu trennen,es sei denn, das-Argument weist das

Wenn Sie in der Datei x. y nach "Hello" oder "There" suchen möchten, geben Sie Folgendes ein:

```
findstr "hello there" x.y 
```

Geben Sie Folgendes ein, um in der Datei x. y nach "Hello There" zu suchen:

```
findstr /c:"hello there" x.y 
```

Geben Sie Folgendes ein, um alle Vorkommen des Worts "Windows" (mit dem ersten Großbuchstaben "W") in der Datei "Proposal. txt" zu finden:

```
findstr Windows proposal.txt 
```

Geben Sie Folgendes ein, um jede Datei im aktuellen Verzeichnis und alle Unterverzeichnisse zu durchsuchen, die das Word-Fenster enthalten, unabhängig vom Buchstaben Fall:

```
findstr /s /i Windows *.* 
```

Wenn Sie alle Vorkommen von Zeilen suchen möchten, die mit "for" beginnen und von NULL oder mehr Leerzeichen (wie in einer Computerprogramm Schleife) vorangestellt werden, und um die Zeilennummer anzuzeigen, in der die einzelnen Vorkommen gefunden werden, geben Sie Folgendes ein:

```
findstr /b /n /r /c:"^ *FOR" *.bas 
```

Wenn Sie mehrere Zeichen folgen in einem Satz von Dateien suchen möchten, erstellen Sie eine Textdatei, die jedes Suchkriterium in einer separaten Zeile enthält. Sie können auch die genauen Dateien auflisten, die Sie in einer Textdatei durchsuchen möchten. Wenn Sie z. b. die Suchkriterien in der Datei "stringlist. txt" verwenden möchten, suchen Sie die in FileList. txt aufgeführten Dateien, und speichern Sie dann die Ergebnisse in den Datei Ergebnissen. out, geben Sie Folgendes ein:

```
findstr /g:stringlist.txt /f:filelist.txt > results.out 
```

Geben Sie Folgendes ein, um jede Datei mit dem Wort "Computer" im aktuellen Verzeichnis und allen Unterverzeichnissen aufzulisten, unabhängig von der Groß-/Kleinschreibung:

```
findstr /s /i /m "\<computer\>" *.*
```

Geben Sie Folgendes ein, um alle Dateien aufzulisten, die das Wort "Computer" und alle anderen Wörter enthalten, die mit "Comp" beginnen (z. b. "Kompliment" und "konkurrieren"):

```
findstr /s /i /m "\<comp.*" *.*
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)