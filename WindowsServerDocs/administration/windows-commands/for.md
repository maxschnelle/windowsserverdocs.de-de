---
title: als Typ für
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e275726c-035f-4a74-8062-013c37f5ded1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8764887794857ae56b7c1a3bda656ece18c117f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439214"
---
# <a name="for"></a>als Typ für



Führt einen Befehl für jede Datei in einen Satz von Dateien an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
for {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|{%%\|%}\<Variable>|Erforderlich. Stellt einen ersetzbaren Parameter dar. Verwenden Sie ein einzelnen Prozentzeichen ( **%** ) für die Durchführung der **für** Befehl an der Eingabeaufforderung. Verwenden Sie doppelte Prozentzeichen ( **%%** ) für die Durchführung der **für** Befehl innerhalb einer Batchdatei. Variablen sind Groß-/Kleinschreibung beachtet, und sie müssen dargestellt werden mit einem alphabetischen Wert wie z. B. **%A**, **%B**, oder **%C**.|
|(\<Festgelegt >)|Erforderlich. Gibt an, eine oder mehrere Dateien, Verzeichnisse oder Zeichenfolgen oder einen Bereich von Werten auf dem Sie den Befehl ausführen. Die Klammern sind erforderlich.|
|\<Befehl >|Erforderlich. Gibt an, der Befehl, der Sie sich auf jede Datei, Verzeichnis oder Textzeichenfolge oder den Bereich der Werte, die in enthaltenen ausführen möchten *festgelegt*.|
|\<CommandLineOptions>|Gibt alle Befehlszeilenoptionen, die Sie mit dem angegebenen Befehl verwenden möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Mithilfe von **für**

  Sie können die **für** Befehl innerhalb einer Batchdatei oder direkt über die Eingabeaufforderung.
- Verwenden von Batchparametern

  Die folgenden Attribute gelten für die **für** Befehl:  
  - Die **für** -Befehl ersetzt **%** <em>Variable</em> oder **%%** <em>Variable</em>mit jeder Zeichenfolge in der angegebenen Menge aus, bis der angegebene Befehl alle Dateien verarbeitet.
  - Variablennamen wird die Groß-/Kleinschreibung beachtet, global und nicht mehr als 52 gleichzeitig aktiv sein können.
  - Um Verwechslungen mit den Batchparametern zu vermeiden **%0** über **%9**, können Sie jedes beliebige Zeichen *Variable* außer die Ziffern 0 bis 9. Für einfache Batchdateien, ein einzelnes Zeichen wie z. B. **%sql_product_prefix%** funktioniert.
  - Sie können mehrere Werte für *Variable* in komplexen Batchdateien, verschiedene ersetzbare Variablen zu unterscheiden.
- Angeben einer Gruppenstatus von Dateien

  Die *festgelegt* Parameter kann eine einzelne Gruppe von Dateien oder mehrere Gruppen von Dateien darstellen. Sie können Platzhalterzeichen verwenden ( **&#42;** und **?** ) legen Sie eine Datei angeben. Im folgenden finden gültige Dateigruppen:  
  ```
  (*.doc) 
  (*.doc *.txt *.me)
  (jan*.doc jan*.rpt feb*.doc feb*.rpt)
  (ar??1991.* ap??1991.*)
  ```  
  Bei Verwendung der **für** Befehl, den ersten Wert im *festgelegt* ersetzt **%** <em>Variable</em> oder **%%** <em>Variable</em>, und klicken Sie dann der angegebene Befehl verarbeitet diesen Wert. Dieser Vorgang wird fortgesetzt, bis alle Dateien (oder Gruppen von Dateien), die entsprechen, den *festgelegt* Wert verarbeitet werden.
- Mithilfe der **in** und **führen** Schlüsselwörter

  **In** und **führen** sind keine Parameter, aber Sie müssen diese mit verwenden **für**. Wenn Sie eines dieser Schlüsselwörter weglassen, wird eine Fehlermeldung angezeigt.
- Verwenden weitere Formen der **für**

  Wenn befehlserweiterungen aktiviert sind (die der Standardwert ist), die folgenden zusätzlichen Formen **für** werden unterstützt:  
  - Nur Verzeichnisse

    Wenn *festgelegt* Platzhalterzeichen enthält ( **&#42;** oder **?** ), dem angegebenen *Befehl* führt für jedes Verzeichnis (statt eines Satzes die Dateien im angegebenen Verzeichnis), entspricht *festgelegt*.

    Die Syntax lautet:  
    ```
    for /d {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>] 
    ```  
  - Rekursiv

    Führt die Verzeichnisstruktur, die als Stamm ist *Laufwerk*:*Pfad* und führt die **für** Anweisung in jedem Verzeichnis der Struktur. Wenn kein Verzeichnis, nach dem angegeben ist **/r**, das aktuelle Verzeichnis als Stammverzeichnis verwendet wird. Wenn *festgelegt* nur ein einzigen Punkt (.), wird nur die Verzeichnisstruktur aufgelistet.

    Die Syntax lautet:  
    ```
    for /r [[<Drive>:]<Path>] {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>]
    ```  
  - Durchlaufen einen Bereich von Werten

    Verwenden Sie eine iterative Variable zum Festlegen des Werts ab (*starten*#) und anschließend durchlaufen Sie einen Set-Bereich von Werten, bis der Wert Endwert überschreitet (*End*#). **/ l** führt durch Vergleichen der iterative *starten*# mit *End*#. Wenn *starten*# ist kleiner als *End*# der Befehl ausgeführt wird. Wenn die iterative Variable überschreitet *End*#, die Befehlsshell beendet die Schleife. Sie können auch eine Negative *Schritt*#, um einen Bereich in absteigender Werte zu durchlaufen. Beispielsweise (1,1,5) generiert die Folge 1 2 3 4 5 und (5,-1,1) die Sequenz 5 4 3 2 1 generiert.

    Die Syntax lautet:  
    ```
    for /l {%%|%}<Variable> in (<Start#>,<Step#>,<End#>) do <Command> [<CommandLineOptions>]
    ```  
  - Durchlaufen und die Datei zu analysieren

    Verwenden Sie die Ausgabe des Befehls verarbeiten, Zeichenfolgen und Inhalt der Datei bei der Analyse.  Verwenden Sie iterative Variablen definieren Sie den Inhalt oder die Zeichenfolgen, die Sie untersuchen möchten, und verwenden Sie die verschiedenen *Analyseschlüsselwörter* Optionen für die Analyse weiter zu ändern.  Verwenden der *Analyseschlüsselwörter* token verwenden, um anzugeben, welche Token als iterative Variablen übergeben werden sollen. Beachten Sie, dass bei der Verwendung ohne die Option token **/f** wird nur das erste Token untersuchen.

    Analysieren von Datei besteht aus beim Lesen der Ausgabe, die Zeichenfolge oder den Inhalt der Datei, und klicken Sie dann in einzelne Textzeilen unterteilt wird und Analysieren der einzelnen Zeilen in NULL oder mehr Token. Die **für** Schleife wird anschließend aufgerufen, mit dem iterativen Variablenwert, der auf das Token festlegen. In der Standardeinstellung **/f** erste Leerzeichen getrennte token übergibt, aus jeder Zeile jeder Datei. Leere Zeilen werden übersprungen.

    Die Syntax ist:  
    ```
    for /f ["<ParsingKeywords>"] {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>]
    for /f ["<ParsingKeywords>"] {%%|%}<Variable> in ("<LiteralString>") do <Command> [<CommandLineOptions>]
    for /f ["<ParsingKeywords>"] {%%|%}<Variable> in ('<Command>') do <Command> [<CommandLineOptions>]
    ```  
    Die *festgelegt* Argument gibt einen oder mehrere Dateinamen an. Jede Datei ist geöffnet, gelesen und verarbeitet, bevor die Umstellung auf die nächste Datei im *festgelegt*. Um das standardanalyseverhalten zu überschreiben, geben *Analyseschlüsselwörter*. Dies ist eine Zeichenfolge in Anführungszeichen, die ein oder mehrere Schlüsselwörter zum Angeben von Möglichkeiten für die Analyse enthält.

    Bei Verwendung der **Usebackq** option, eine der folgenden Syntaxangaben verwenden:  
    ```
    for /f ["usebackq <ParsingKeywords>"] {%%|%}<Variable> in ("<Set>") do <Command> [<CommandLineOptions>]
    for /f ["usebackq <ParsingKeywords>"] {%%|%}<Variable> in ('<LiteralString>') do <Command> [<CommandLineOptions>]
    for /f ["usebackq <ParsingKeywords>"] {%%|%}<Variable> in (`<Command>`) do <Command> [<CommandLineOptions>]
    ```  
    Die folgende Tabelle enthält die Analyse Schlüsselwörter, mit denen Sie für *Analyseschlüsselwörter*.  

    |      Schlüsselwort      |                                                                                                                                                                                                          Beschreibung                                                                                                                                                                                                          |
    |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    |     eol=\<c>      |                                                                                                                                                                                   Gibt ein Ende der Zeile-Zeichen (nur ein einzelnes Zeichen).                                                                                                                                                                                    |
    |     skip=\<N>     |                                                                                                                                                                              Gibt die Anzahl der Zeilen, die am Anfang der Datei ausgelassen werden sollen.                                                                                                                                                                              |
    |   delims=\<xxx>   |                                                                                                                                                                     Gibt einen Trennzeichensatz. Dies ersetzt den Standardsatz der Trennzeichen aus Leerzeichen und Tabulator.                                                                                                                                                                      |
    | tokens=\<X,Y,M–N> | Gibt an, welche Token aus jeder Zeile sind, übergeben werden soll die **für** Schleife für jede Iteration. Daher werden die Namen von zusätzliche Variable zugeordnet. *M*–*N* gibt einen Bereich von der *M*th über die *N*th-Token. Wenn das letzte Zeichen in der **Token =** Zeichenfolge ist ein Sternchen ( **&#42;** ), wird eine zusätzliche Variable zugewiesen und erhält den restlichen Text in der Zeile nach dem letzten Token, die analysiert wird. |
    |     usebackq      |                                                                                             Gibt an, dass: Ausführen einer Zeichenfolge in Anführungszeichen zurück, wie ein Befehl, verwenden Sie eine Zeichenfolge in einfachen Anführungszeichen als Zeichenfolgenliteral oder, Dateinamen in lange Dateinamen, die Leerzeichen enthalten, ermöglichen  *\<festgelegt\>* , jeweils in eingeschlossen werden doppelte Anführungszeichen.                                                                                              |


  - VariablenErsetzung

    Die folgende Tabelle enthält optionale Syntax (für jede Variable **ich**).  

    |Die Variable mit dem Modifizierer|Beschreibung|
    |----------------------|-----------|
    |%~I|Wird erweitert, **%I** entfernt keine umgebenden Anführungszeichen ("").|
    |%~fI|Wird erweitert, **%I** auf einen vollqualifizierten Pfadnamen.|
    |%~dI|Wird erweitert, **%I** nur einen Laufwerkbuchstaben.|
    |%~pI|Wird erweitert, **%I** nur zu einem Pfad.|
    |%~nI|Wird erweitert, **%I** nur zu einer Datei.|
    |%~xI|Wird erweitert, **%I** mit nur einer Dateierweiterung.|
    |%~sI|Wird erweitert, Path, um nur einen kurzen Namen enthalten.|
    |%~aI|Wird erweitert, **%I** an den Dateiattributen der Datei.|
    |%~tI|Wird erweitert, **%I** auf das Datum und Uhrzeit der Datei.|
    |%~zI|Wird erweitert, **%I** auf die Größe der Datei.|
    |%~$PATH:I|Die in der PATH-Umgebungsvariable aufgeführten Verzeichnisse durchsucht und erweitert **%I** auf den vollqualifizierten Namen der das erste Verzeichnis gefunden. Wenn der Name der Umgebungsvariablen nicht definiert ist oder die Datei wird von der Suche nicht gefunden, wird dieser Modifizierer auf eine leere Zeichenfolge erweitert.|

    Die folgende Tabelle enthält die Modifizierer-Kombinationen, die Sie verwenden können, um zusammengesetzte Ergebnisse zu erhalten.  

    |Variable mit kombinierte Modifizierer|Beschreibung|
    |--------------------------------|-----------|
    |%~dpI|Wird erweitert, **%I** auf einem Laufwerkbuchstaben und Pfad nur.|
    |%~nxI|Wird erweitert, **%I** , einen Dateinamen und die Erweiterung nur.|
    |%~fsI|Wird erweitert, **%I** zu einem vollständigen Pfadnamen mit kurzen Namen.|
    |%~dp$PATH:I|Sucht die Verzeichnisse, die aufgeführt sind, in der PATH-Umgebungsvariablen für **%I** und erweitert, um den Laufwerkbuchstaben und Pfad der ersten gefunden.|
    |%~ftzaI|Wird erweitert, **%I** auf eine Ausgabezeile, die wie **Dir**.|

    Sie können in den obigen Beispielen ersetzen **%I** und Pfad mit einem anderen gültigen Werte. Ein gültiger **für** Variablenname beendet die **%~** Syntax.

    Mithilfe von Großbuchstaben Variablennamen wie z. B. **%I**, können Sie Ihren Code besser lesbar und Vermeidung von Verwechslungen mit den Parametern, die nicht Groß-/Kleinschreibung beachtet werden.
- Analysieren einer Zeichenfolge

  Können Sie die **für/f** Analyselogik auf direkt für eine Zeichenfolge durch das wrapping *\<LiteralString\>* entweder: doppelte Anführungszeichen (*ohne* " Usebackq") oder in einfache Anführungszeichen (*mit* "Usebackq") – Beispiel ("MyString") oder ("MyString"). *\<LiteralString\>*  wird als einzelne Zeile der Eingabe aus einer Datei behandelt. Bei der Analyse *\<LiteralString\>* in doppelten Anführungszeichen, Befehl Symbole (z. B. **\\ \& \| \> \< \^** ) werden als normales Zeichen behandelt.
- Analysieren der Ausgabe

  Sie können die **für/f** Befehl aus, um die Ausgabe eines Befehls zu analysieren, durch das Platzieren einer zurück in Anführungszeichen *\<Befehl\>* zwischen den Klammern. Es wird als eine Befehlszeile behandelt, die an ein untergeordnetes Element Cmd.exe übergeben wird. Die Ausgabe wird in den Speicher erfasst und analysiert, als ob es sich um eine Datei ist.

## <a name="BKMK_examples"></a>Beispiele für

Verwendung von **für** in einer Batchdatei, verwenden Sie die folgende Syntax:
```
for {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>]
```
Zeigen Sie den Inhalt aller Dateien im aktuellen Verzeichnis, die der Erweiterung DOC oder TXT zu haben, mittels des ersetzbaren Variable **%f**, Typ:
```
for %f in (*.doc *.txt) do type %f 
```
Im vorherigen Beispiel alle Dateien mit der Erweiterung DOC oder TXT im aktuellen Verzeichnis ersetzt wird, für die **%f** Variable, bis der Inhalt jeder Datei angezeigt werden. Um diesen Befehl in einer Batchdatei verwenden, ersetzt alle Vorkommen von **%f** mit **%sql_product_prefix%** . Anderenfalls die Variable wird ignoriert, und eine Fehlermeldung wird angezeigt.

Um eine Datei zu analysieren, kommentiert wird ignoriert, Linien, Typ:
```
for /f "eol=; tokens=2,3* delims=," %i in (myfile.txt) do @echo %i %j %k
```
Dieser Befehl analysiert jede Zeile in Myfile.txt. Sie ignoriert Zeilen, die mit einem Semikolon zu beginnen, und übergibt Sie das zweite und dritte Token aus jeder Zeile auf die **für** Text (Token werden durch Kommas oder Leerzeichen getrennt). Der Hauptteil der **für** -Anweisung verweist auf **%i** zum Abrufen von Zugriffstoken, des zweites **%j** beim Abrufen des dritten Tokens, und **%k** zum Abrufen aller die verbleibenden Token. Wenn die Dateinamen, die Sie angeben, die Leerzeichen enthalten, verwenden Sie Anführungszeichen um den Text (z. B. "Dateiname"). Sie müssen zum Verwenden von Anführungszeichen verwenden **Usebackq**. Andernfalls werden die Anführungszeichen interpretiert, als definieren ein Zeichenfolgenliteral beim Analysieren.

**%i** wird explizit deklariert, der **für** Anweisung. **%j** und **%k** implizit deklariert werden, indem **Token =** . Sie können **Token =** bis zu 26-Token angeben, vorausgesetzt, dass es keinen Versuch, eine Variable, die höher als die Buchstaben "Z" oder "Z" verursacht

Das folgende Beispiel listet die Namen der Umgebungsvariablen in der aktuellen Umgebung. Beim Analysieren der Ausgabe eines Befehls durch Platzieren von *festgelegt* Geben Sie zwischen den Klammern:
```
for /f "usebackq delims==" %i in ('set') do @echo %i 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
