---
title: findstr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 82ba51cdb49501492c1fa38c6c93933f4aee90d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890461"
---
# <a name="findstr"></a>findstr



Sucht nach Mustern von Text in Dateien.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
findstr [/b] [/e] [/l | /r] [/s] [/i] [/x] [/v] [/n] [/m] [/o] [/p] [/f:<File>] [/c:<String>] [/g:<File>] [/d:<DirList>] [/a:<ColorAttribute>] [/off[line]] <Strings> [<Drive>:][<Path>]<FileName>[ ...]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/b|Mit dem Textmuster übereinstimmt, wenn sie am Anfang einer Zeile befindet.|
|/ e|Mit dem Textmuster übereinstimmt, wenn es am Ende einer Zeile ist.|
|/l|Prozesse Suchen von Zeichenfolgen buchstäblich.|
|/r|Prozesse Suchen von Zeichenfolgen als reguläre Ausdrücke. Dies ist die Standardeinstellung.|
|/s|Das aktuelle Verzeichnis und alle Unterverzeichnisse durchsucht.|
|/i|Ignoriert die Groß-/Kleinschreibung der Zeichen, bei der Suche nach der Zeichenfolge.|
|/x|Gibt die Zeilen, die exakt übereinstimmen.|
|/v|Gibt nur die Zeilen, die eine Übereinstimmung nicht enthalten.|
|/n|Gibt die Zeilennummer der jede Zeile, der mit übereinstimmt.|
|/m|Gibt nur den Dateinamen an, wenn eine Datei eine Übereinstimmung enthält.|
|/o|Gibt den Zeichenoffset vor den übereinstimmenden Zeilen.|
|/p|Überspringt die Dateien mit nicht druckbare Zeichen.|
|/off[line]|Dateien, die das Attribut "offline" festgelegt ist, werden nicht übersprungen werden.|
|/f:\<File>|Ruft eine Liste von Dateien aus der angegebenen Datei ab.|
|/c:\<String>|Verwendet den angegebenen Text als literal Suchzeichenfolge an.|
|/ g:\<Datei >|Ruft Suchen von Zeichenfolgen aus der angegebenen Datei.|
|/d:\<DirList>|Durchsucht die angegebene Liste von Verzeichnissen an. Jedes Verzeichnis muss z. B. mit einem Semikolon (;) getrennt werden `dir1;dir2;dir3`.|
|/a:\<ColorAttribute>|Gibt Farbattribute mit zwei hexadezimalen Zeichen. Typ `color /?` für zusätzliche Informationen.|
|\<Strings>|Gibt den Text im zu suchende *FileName*. Erforderlich.|
|[\<Laufwerk >:] [<Path>]<FileName>[...]|Gibt den Speicherort und die Datei oder die zu durchsuchenden Dateien. Mindestens ein Dateiname ist erforderlich.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Alle **Findstr** Befehlszeilenoptionen müssen vorangehen *Zeichenfolgen* und *FileName* in der Befehlszeichenfolge.
-   Reguläre Ausdrücke werden sowohl Metazeichen als auch Literale Zeichen verwenden, um Textmuster, anstatt genaue Zeichenfolgen mit Zeichen suchen. Literalzeichen ist ein Zeichen, die keine besondere Bedeutung in der Syntax für reguläre Ausdrücke – es entspricht einem Vorkommen des Zeichens. Beispielsweise sind Buchstaben und Zahlen Literalzeichen. Ein Metazeichen ist ein Symbol mit besonderer Bedeutung (ein Operator oder Trennzeichen) in der Syntax von regulären Ausdrücken.

    Die folgende Tabelle enthält die Metazeichen, **Findstr** akzeptiert.  
    |Metazeichen|Wert|
    |-------------|-----|
    |.|: Platzhalterzeichen|
    |*|Wiederholung: NULL oder mehr Vorkommen des vorherigen Zeichens oder -Klasse|
    |^|Zeilenposition: der Zeile ab|
    |$|Zeilenposition: Ende der Zeile|
    |[class]|Zeichenklasse: ein einzelnes Zeichen in einer Gruppe|
    |[^class]|Inverse-Klasse: ein einzelnes Zeichen nicht in einem Satz|
    |[x-y]|Bereich: alle Zeichen innerhalb des angegebenen Bereichs|
    |\x|Escapezeichen: direkte Verwendung von einem Metazeichen x|
    |\\<string|Word-Position: des Worts ab|
    |string\>|Word-Position: Ende des Worts|

    Die Sonderzeichen in der Syntax für reguläre Ausdrücke haben das größte Leistungspotenzial auf, wenn Sie zusammen verwendet werden. Beispielsweise verwenden Sie die folgende Kombination von das Platzhalterzeichen (.), und wiederholen Sie die Zeichen (*) eine beliebige Zeichenfolge von Zeichen:  
    ```
    .*
    ```  
    Verwenden Sie den folgenden Ausdruck im Rahmen eines umfassenderen Ausdrucks eine beliebige Zeichenfolge mit "Ing" mit "b" beginnen und enden:  
    ```
    b.*ing
    ```

## <a name="BKMK_examples"></a>Beispiele für

Verwenden Sie Leerzeichen, mehrere Zeichenfolgen zu trennen, es sei denn, das Argument vorangestellt wird **/c**.

Zu suchende "Hello", oder geben Sie in der Datei x.y "there":
```
findstr "hello there" x.y 
```
Um "Hello es" aus, in dem Datei-x.y suchen, geben Sie Folgendes ein:
```
findstr /c:"hello there" x.y 
```
Um alle Vorkommen des Worts "Windows" (mit einem großen Anfangsbuchstaben W) in der Datei Proposal.txt suchen, geben Sie Folgendes ein:
```
findstr Windows proposal.txt 
```
Geben Sie Folgendes ein, um jede Datei im aktuellen Verzeichnis und allen Unterverzeichnissen, die mit dem Windows, unabhängig von der Groß-/Kleinschreibung, Wort zu suchen:
```
findstr /s /i Windows *.* 
```
Alle Vorkommen von Zeilen, die mit "FOR" beginnen, und beginnen mit NULL oder mehr Leerzeichen (wie in einer Programmschleife) und die Nummer der Zeile anzeigen, wobei jedes Vorkommen gefunden wird, geben Sie Folgendes:
```
findstr /b /n /r /c:"^ *FOR" *.bas 
```
Um mehrere Zeichenfolgen in einen Satz von Dateien zu suchen, erstellen Sie eine Textdatei, die jede Suchkriterium in einer separaten Zeile enthält. Sie können auch die genauen Dateien auflisten, die Sie in einer Textdatei suchen möchten. Z. B. um die Suchkriterien in der Datei Stringlist.txt verwenden zu können, suchen Sie die Dateien in %% amp;quot;FileList.txt%%amp;quot; und speichern Sie die Ergebnisse in der Datei Results.out, Typ:
```
findstr /g:stringlist.txt /f:filelist.txt > results.out 
```
Geben Sie Folgendes ein, um jede Datei, die das Wort "Computer" in das aktuelle Verzeichnis und alle Unterverzeichnisse, unabhängig von der Schreibweise, aufzulisten:
```
findstr /s /i /m "\<computer\>" *.*
```
So Listen Sie jede Datei, die mit dem Wort "Computer" und andere Wörter, die mit "Comp" (z. B. "Ergänzung" und "Wettbewerb") Typ beginnen:
```
findstr /s /i /m "\<comp.*" *.*
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)