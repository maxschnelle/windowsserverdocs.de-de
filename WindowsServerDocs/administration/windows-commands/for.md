---
title: als Typ für
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: db0bf54e35e4226cb020b040d5fc36ddd88dc02b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377123"
---
# <a name="for"></a>als Typ für



Führt einen angegebenen Befehl für jede Datei in einem Satz von Dateien aus.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
for {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|{%% \|%} \<Variable >|Erforderlich. Stellt einen austauschbaren Parameter dar. Verwenden Sie ein einzelnes Prozentzeichen ( **%** ), um den **for** -Befehl an der Eingabeaufforderung auszuführen. Verwenden Sie doppelte Prozentzeichen ( **%%** ), um den **for** -Befehl in einer Batchdatei auszuführen. Bei Variablen wird die Groß-/Kleinschreibung beachtet, und Sie müssen mit einem alphabetischen Wert wie **% A**, **% B**oder **% C**dargestellt werden.|
|(\<set >)|Erforderlich. Gibt eine oder mehrere Dateien, Verzeichnisse oder Text Zeichenfolgen oder einen Wertebereich an, für den der Befehl ausgeführt werden soll. Die Klammern sind erforderlich.|
|\<-Befehl >|Erforderlich. Gibt den Befehl an, den Sie für jede Datei, jedes Verzeichnis oder jede Text *Zeichenfolge*ausführen möchten, oder für den Wertebereich, der in Set enthalten ist.|
|\<commandlineoptions >|Gibt alle Befehlszeilenoptionen an, die Sie mit dem angegebenen Befehl verwenden möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Verwenden **von für**

  Sie können den **for** -Befehl in einer Batchdatei oder direkt über die Eingabeaufforderung verwenden.
- Verwenden von Batch Parametern

  Die folgenden Attribute gelten für den **for** -Befehl:  
  - Der **for** -Befehl ersetzt **%-** <em>Variable</em> oder **%%-** <em>Variable</em> durch jede Text Zeichenfolge in der angegebenen Menge, bis der angegebene Befehl alle Dateien verarbeitet.
  - Bei Variablennamen wird die Groß-/Kleinschreibung beachtet, Global und höchstens 52 kann gleichzeitig aktiv sein.
  - Um Verwechslungen mit den Batch Parametern **% 0** bis **% 9**zu vermeiden, können Sie ein beliebiges Zeichen für die *Variable* verwenden, mit Ausnahme der Ziffern 0 bis 9. Bei einfachen Batch Dateien funktioniert ein einzelnes Zeichen, z. **b.%% f** .
  - Sie können mehrere Werte für *Variable* in komplexen Batch Dateien verwenden, um unterschiedliche ersetzbare Variablen zu unterscheiden.
- Angeben einer Gruppe von Dateien

  Der *Set* -Parameter kann eine einzelne Gruppe von Dateien oder mehrere Gruppen von Dateien darstellen. Sie können Platzhalter Zeichen ( **&#42;** und **?** ) verwenden, um einen Datei Satz anzugeben. Im folgenden sind gültige Datei Sätze aufgeführt:  
  ```
  (*.doc) 
  (*.doc *.txt *.me)
  (jan*.doc jan*.rpt feb*.doc feb*.rpt)
  (ar??1991.* ap??1991.*)
  ```  
  Wenn Sie den **for** -Befehl verwenden, ersetzt der erste Wert in *set* **%-** <em>Variable</em> oder **%%** -<em>Variablen</em>, und der angegebene Befehl verarbeitet diesen Wert. Dies wird so lange fortgesetzt, bis alle Dateien (oder Dateigruppen), die dem *Satz* Wert entsprechen, verarbeitet werden.
- Verwenden der **in** -und **do** -Schlüsselwörter

  **In** und **sind keine Parameter** , aber Sie müssen Sie mit **for**verwenden. Wenn Sie keines dieser Schlüsselwörter weglassen, wird eine Fehlermeldung angezeigt.
- Verwenden zusätzlicher Formen von **für**

  Wenn Befehls Erweiterungen aktiviert sind (Standardeinstellung), werden die folgenden zusätzlichen Formen von **für** unterstützt:  
  - Nur Verzeichnisse

    Wenn *Set* Platzhalter Zeichen ( **&#42;** oder **?** ) enthält, wird der angegebene *Befehl* für jedes Verzeichnis (anstelle eines Satzes von Dateien in einem angegebenen Verzeichnis) ausgeführt, der mit *Set*übereinstimmt.

    Die Syntax lautet:  
    ```
    for /d {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>] 
    ```  
  - Rekursiv

    Durchläuft die Verzeichnisstruktur, die sich auf *Laufwerk*:*path* befindet, und führt die for-Anweisung in jedem Verzeichnis der Struktur **aus** . Wenn nach **/r**kein Verzeichnis angegeben ist, wird das aktuelle Verzeichnis als Stammverzeichnis verwendet. Wenn *Set* nur ein einzelner Zeitraum (.) ist, wird nur die Verzeichnisstruktur aufgelistet.

    Die Syntax lautet:  
    ```
    for /r [[<Drive>:]<Path>] {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>]
    ```  
  - Iterieren eines Wertebereichs

    Verwenden Sie eine iterative Variable, um den Startwert (*Start*Nr.) festzulegen, und durchlaufen Sie dann einen festgelegten Wertebereich, bis der Wert den festgelegten Endwert (*End*#) überschreitet. **/l** führt das iterative durch Vergleichen von *Start*# mit *End*# aus. Wenn " *Start*#" kleiner als " *End*" ist, wird der Befehl ausgeführt. Wenn die iterative Variable den Wert für *End*# überschreitet, beendet die Befehlsshell die Schleife. Sie können auch einen negativen *Schritt*# verwenden, um einen Bereich in abnehmenden Werten schrittweise zu durchlaufen. Beispielsweise generiert (1, 1, 5) die Sequenz 1 2 3 4 5, und (5,-1, 1) generiert die Sequenz 5 4 3 2 1.

    Die Syntax lautet:  
    ```
    for /l {%%|%}<Variable> in (<Start#>,<Step#>,<End#>) do <Command> [<CommandLineOptions>]
    ```  
  - Iteration und Dateiverarbeitung

    Verwenden Sie die Datei--Verarbeitung, um Befehlsausgabe, Zeichen folgen und Dateiinhalte zu verarbeiten.  Verwenden Sie iterative Variablen, um die Inhalte oder Zeichen folgen zu definieren, die Sie untersuchen möchten, und verwenden Sie die verschiedenen Optionen für "paramesing *Keywords* ", um die Verarbeitung weiter zu ändern.  Verwenden Sie die Option *parsingkeywords* Token, um anzugeben, welche Token als iterative Variablen übermittelt werden sollen. Beachten Sie, dass **/f** bei Verwendung ohne die Token-Option nur das erste Token untersucht.

    Die Datei-Analyse besteht darin, die Ausgabe-, Zeichen folgen-oder Dateiinhalte zu lesen und Sie dann in einzelne Textzeilen zu unterteilen und jede Zeile in NULL oder mehr Token zu parsen. Die **for** -Schleife wird dann aufgerufen, wobei der Wert der iterativen Variablen auf das Token festgelegt ist. Standardmäßig übergibt **/f** das erste leere getrennte Token von jeder Zeile jeder Datei. Leere Zeilen werden übersprungen.

    Die Syntaxen lauten:  
    ```
    for /f ["<ParsingKeywords>"] {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>]
    for /f ["<ParsingKeywords>"] {%%|%}<Variable> in ("<LiteralString>") do <Command> [<CommandLineOptions>]
    for /f ["<ParsingKeywords>"] {%%|%}<Variable> in ('<Command>') do <Command> [<CommandLineOptions>]
    ```  
    Das *Set* -Argument gibt mindestens einen Dateinamen an. Alle Dateien werden vor dem Wechsel zur nächsten Datei in *festgelegt*, gelesen und verarbeitet. Um das standardmäßige Parametrisierungsverhalten zu überschreiben, geben Sie " *Parser Keywords*" Dies ist eine Zeichenfolge in Anführungszeichen, die ein oder mehrere Schlüsselwörter enthält, um verschiedene Optionen für die Verarbeitung anzugeben.

    Wenn Sie die Option **usebackq** verwenden, verwenden Sie eine der folgenden Syntaxen:  
    ```
    for /f ["usebackq <ParsingKeywords>"] {%%|%}<Variable> in ("<Set>") do <Command> [<CommandLineOptions>]
    for /f ["usebackq <ParsingKeywords>"] {%%|%}<Variable> in ('<LiteralString>') do <Command> [<CommandLineOptions>]
    for /f ["usebackq <ParsingKeywords>"] {%%|%}<Variable> in (`<Command>`) do <Command> [<CommandLineOptions>]
    ```  
    In der folgenden Tabelle sind die Schlüsselwörter aufgeführt, die Sie für die Verwendung von *para*Metern verwenden können.  

    |      Schlüsselwort      |                                                                                                                                                                                                          Beschreibung                                                                                                                                                                                                          |
    |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    |     EOL = \<C >      |                                                                                                                                                                                   Gibt ein Zeilenendezeichen an (nur ein Zeichen).                                                                                                                                                                                    |
    |     Skip = \<n >     |                                                                                                                                                                              Gibt die Anzahl der Zeilen an, die am Anfang der Datei übersprungen werden sollen.                                                                                                                                                                              |
    |   Delta = \<xxx >   |                                                                                                                                                                     Gibt einen Trenn Zeichensatz an. Dadurch wird das Standard Trennzeichen Set von Space und Tab ersetzt.                                                                                                                                                                      |
    | Tokens = \<x, Y, M – N > | Gibt an, welche Token aus den einzelnen Zeilen an die **for** -Schleife für jede Iterationen übermittelt werden sollen. Folglich werden zusätzliche Variablennamen zugeordnet. *M*–*N* gibt einen Bereich an, vom *m*-bis zum *n*-ten Token. Wenn das letzte Zeichen in **Token =** String ein Sternchen ( **&#42;** ) ist, wird eine zusätzliche Variable zugeordnet, und Sie empfängt den verbleibenden Text in der Zeile nach dem letzten analysierten Token. |
    |     usebackq      |                                                                                             Gibt an: führen Sie eine Zeichenfolge in einer Zeichenfolge mit einer Zeichenfolge in Anführungszeichen als Literalzeichenfolge aus, oder verwenden Sie für lange Dateinamen, die Leerzeichen enthalten, die Angabe von Dateinamen in *\<Set @ no__t-2*in doppelte Anführungszeichen.                                                                                              |


  - Variablen Ersetzung

    In der folgenden Tabelle ist die optionale Syntax (für alle Variablen **I**) aufgeführt.  

    |Variable mit Modifizierer|Beschreibung|
    |----------------------|-----------|
    |% ~ I|Erweitert **% I** und entfernt alle umgebenden Anführungszeichen ("").|
    |% ~ fI|Erweitert **% I** in einen voll qualifizierten Pfadnamen.|
    |% ~ dI|" **% I** " wird nur in einen Laufwerk Buchstaben erweitert.|
    |% ~ pI|" **% I** " wird nur in einen Pfad erweitert.|
    |% ~ NI|Erweitert **% I** nur auf einen Dateinamen.|
    |% ~ XI|Erweitert **% I** nur in eine Dateinamenerweiterung.|
    |% ~ Si|Erweitert den Pfad, sodass nur Kurznamen enthalten sind.|
    |% ~ Ai|Erweitert **% I** zu den Dateiattributen der Datei.|
    |% ~ TI|Erweitert **% I** in das Datum und die Uhrzeit der Datei.|
    |% ~ Zi|Erweitert **% I** in die Größe der Datei.|
    |% ~ $PATH: I|Durchsucht die Verzeichnisse, die in der PATH-Umgebungsvariablen aufgelistet sind, und erweitert **% I** auf den voll qualifizierten Namen des ersten gefundenen Verzeichnisses. Wenn der Name der Umgebungsvariablen nicht definiert ist oder die Datei von der Suche nicht gefunden wird, wird dieser Modifizierer auf die leere Zeichenfolge erweitert.|

    In der folgenden Tabelle sind Modifiziererkombinationen aufgelistet, die Sie verwenden können, um zusammengesetzte Ergebnisse zu erhalten.  

    |Variable mit kombinierten modifizierervariablen|Beschreibung|
    |--------------------------------|-----------|
    |% ~ dpI|**% I** wird nur auf einen Laufwerk Buchstaben und einen Pfad erweitert.|
    |% ~ NXI|Erweitert **% I** auf einen Dateinamen und eine Erweiterung.|
    |% ~ FSI|Erweitert " **% I** " auf einen vollständigen Pfadnamen mit nur Kurznamen.|
    |% ~ DP $ Pfad: I|Durchsucht die Verzeichnisse, die in der PATH-Umgebungsvariablen für **% I** aufgelistet sind, und erweitert den Laufwerk Buchstaben und den Pfad des ersten gefundenen Verzeichnisses.|
    |% ~ "f"|Erweitert **% I** in eine Ausgabezeile, die wie **dir**aussieht.|

    In den obigen Beispielen können Sie " **% I** " und "Path" durch andere gültige Werte ersetzen. Ein gültiger **für** Variablenname beendet die **%~-** Syntax.

    Durch die Verwendung von Großbuchstaben (z. b. **% I**) können Sie den Code besser lesbar machen und Verwirrung mit den Modifizierer vermeiden, bei denen die Groß-/Kleinschreibung nicht beachtet wird.
- Eine Zeichenfolge wird verarbeitet.

  Sie können die **for/f** -parameterlogik in einer unmittelbaren Zeichenfolge verwenden, indem Sie *\<literalstring @ no__t-3* in doppelte Anführungszeichen (*ohne* "usebackq") oder in einfache Anführungszeichen (*mit* "usebackq") einschließen, z. b. ("myString") oder (" MyString '). *\<literalstring @ no__t-2* wird als einzelne Zeile der Eingabe aus einer Datei behandelt. Beim *\<literalstring @ no__t-2* in doppelten Anführungszeichen werden Befehls Symbole (z. b. **\\ \& \| \> \< \^** ) als normale Zeichen behandelt.
- Ausgabe wird verarbeitet

  Sie können den **for/f** -Befehl verwenden, um die Ausgabe eines Befehls zu analysieren, indem Sie die *\<command @ no__t-3* der Klammern zwischen den Klammern platzieren. Sie wird als Befehlszeile behandelt, die an eine untergeordnete Datei "cmd. exe" übergeben wird. Die Ausgabe wird im Arbeitsspeicher aufgezeichnet und so analysiert, als ob es sich um eine Datei handelt.

## <a name="BKMK_examples"></a>Beispiele

Verwenden Sie die folgende Syntax, um **für** in einer Batchdatei zu verwenden:
```
for {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>]
```
Geben Sie Folgendes ein, um den Inhalt aller Dateien im aktuellen Verzeichnis mit der Erweiterung ". doc" oder ". txt" mithilfe der ersetzbaren Variable **% f**anzuzeigen:
```
for %f in (*.doc *.txt) do type %f 
```
Im vorherigen Beispiel wird jede Datei mit der Erweiterung ". doc" oder ". txt" im aktuellen Verzeichnis durch die **% f** -Variable ersetzt, bis der Inhalt jeder Datei angezeigt wird. Um diesen Befehl in einer Batchdatei zu verwenden, ersetzen Sie jedes Vorkommen von **% f** durch **%% f**. Andernfalls wird die Variable ignoriert, und es wird eine Fehlermeldung angezeigt.

Geben Sie Folgendes ein, um eine Datei zu analysieren und kommentierte Zeilen zu ignorieren:
```
for /f "eol=; tokens=2,3* delims=," %i in (myfile.txt) do @echo %i %j %k
```
Dieser Befehl analysiert jede Zeile in MyFile. txt. Sie ignoriert Zeilen, die mit einem Semikolon beginnen, und übergibt das zweite und dritte Token von jeder Zeile an den **für** Text (Token werden durch Kommas oder Leerzeichen getrennt). Der Text der **for** -Anweisung verweist auf " **% i** ", um das zweite Token zu erhalten, **% j** , um das dritte Token zu erhalten, und " **% k** ", um alle verbleibenden Token zu erhalten. Wenn die von Ihnen angegebenen Dateinamen Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "Dateiname"). Zum Verwenden von Anführungszeichen müssen Sie **usebackq**verwenden. Andernfalls werden die Anführungszeichen als Definieren einer Literalzeichenfolge interpretiert, die analysiert werden soll.

**% i** ist explizit in der **for** -Anweisung deklariert. **% j** und **% k** werden implizit mithilfe von **Tokens =** deklariert. Sie können **Tokens =** zum Angeben von bis zu 26 Token verwenden, vorausgesetzt, es wird nicht versucht, eine Variable zu deklarieren, die höher ist als der Buchstabe "z" oder "z".

Im folgenden Beispiel werden die Namen der Umgebungsvariablen in der aktuellen Umgebung aufgelistet. Um die Ausgabe eines Befehls zu analysieren, indem Sie eine *Menge* zwischen den Klammern platzieren, geben Sie Folgendes ein:
```
for /f "usebackq delims==" %i in ('set') do @echo %i 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
