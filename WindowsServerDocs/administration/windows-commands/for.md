---
title: for
description: Referenz Artikel für den for-Befehl, der einen angegebenen Befehl für jede Datei in einem Satz von Dateien ausführt.
ms.topic: reference
ms.assetid: e275726c-035f-4a74-8062-013c37f5ded1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7120ed613595b5b90334e49b0865c3e598f3cabb
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027638"
---
# <a name="for"></a>for

Führt einen angegebenen Befehl für jede Datei in einem Satz von Dateien aus.

## <a name="syntax"></a>Syntax

```
for {%% | %}<variable> in (<set>) do <command> [<commandlineoptions>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `{%% | %}<variable>` | Erforderlich. Stellt einen austauschbaren Parameter dar. Verwenden Sie ein einzelnes Prozentzeichen ( `%` ), um den **for** -Befehl an der Eingabeaufforderung auszuführen. Verwenden Sie doppelte Prozentzeichen ( `%%` ), um den **for** -Befehl in einer Batchdatei auszuführen. Bei Variablen wird die Groß-/Kleinschreibung beachtet, und Sie müssen mit einem alphabetischen Wert wie **% a**, **% b**oder **% c**dargestellt werden. |
| (`<set>`) | Erforderlich. Gibt eine oder mehrere Dateien, Verzeichnisse oder Text Zeichenfolgen oder einen Wertebereich an, für den der Befehl ausgeführt werden soll. Die Klammern sind erforderlich. |
| `<command>` | Erforderlich. Gibt den Befehl an, den Sie für jede Datei, jedes Verzeichnis oder jede Text *Zeichenfolge*ausführen möchten, oder für den Wertebereich, der in Set enthalten ist. |
| `<commandlineoptions>` | Gibt alle Befehlszeilenoptionen an, die Sie mit dem angegebenen Befehl verwenden möchten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Sie können diesen Befehl in einer Batchdatei oder direkt über die Eingabeaufforderung verwenden.

- Die folgenden Attribute gelten für den **for** -Befehl:

  - Mit diesem Befehl wird `% variable` oder `%% variable` durch jede Text Zeichenfolge in der angegebenen Menge ersetzt, bis der angegebene Befehl alle Dateien verarbeitet.

  - Bei Variablennamen wird die Groß-/Kleinschreibung beachtet, Global und höchstens 52 kann gleichzeitig aktiv sein.

  - Um Verwechslungen mit den Batch Parametern zu vermeiden, `%0` `%9` können Sie mithilfe von ein beliebiges Zeichen für die *Variable* verwenden, mit Ausnahme der Ziffern **0** bis **9**. Bei einfachen Batch Dateien funktioniert ein einzelnes Zeichen wie z `%%f` . b..

  - Sie können mehrere Werte für *Variable* in komplexen Batch Dateien verwenden, um unterschiedliche ersetzbare Variablen zu unterscheiden.

- Der *Set* -Parameter kann eine einzelne Gruppe von Dateien oder mehrere Gruppen von Dateien darstellen. Sie können Platzhalter Zeichen (**&#42;** und **?**) verwenden, um einen Datei Satz anzugeben. Im folgenden sind gültige Datei Sätze aufgeführt:

  ```
  (*.doc)
  (*.doc *.txt *.me)
  (jan*.doc jan*.rpt feb*.doc feb*.rpt)
  (ar??1991.* ap??1991.*)
  ```

- Wenn Sie diesen Befehl verwenden *, ersetzt der* erste Wert von `% variable` oder `%% variable` , und der angegebene Befehl verarbeitet diesen Wert. Dies wird so lange fortgesetzt, bis alle Dateien (oder Dateigruppen), die dem *Satz* Wert entsprechen, verarbeitet werden.

- **In** und **sind keine Parameter** , aber Sie müssen diese mit diesem Befehl verwenden. Wenn Sie keines dieser Schlüsselwörter weglassen, wird eine Fehlermeldung angezeigt.

- Wenn Befehls Erweiterungen aktiviert sind (Standardeinstellung), werden die folgenden zusätzlichen Formen von **für** unterstützt:

  - **Nur Verzeichnisse:** Wenn *Set* Platzhalter Zeichen (**&#42;** oder **?**) enthält, wird der angegebene *Befehl* für jedes Verzeichnis (anstelle eines Satzes von Dateien in einem angegebenen Verzeichnis) ausgeführt, der mit *Set*übereinstimmt. Die Syntax ist:

    ```
    for /d {%%|%}<Variable> in (<Set>) do <Command> [<CommandLineOptions>]
    ```

  - **Rekursiv:** Durchläuft die Verzeichnisstruktur, die sich auf *Laufwerk*:*path* befindet, und führt die for-Anweisung in jedem Verzeichnis der Struktur **aus** . Wenn nach **/r**kein Verzeichnis angegeben ist, wird das aktuelle Verzeichnis als Stammverzeichnis verwendet. Wenn *Set* nur ein einzelner Zeitraum (.) ist, wird nur die Verzeichnisstruktur aufgelistet. Die Syntax ist:

    ```
    for /r [[<drive>:]<path>] {%%|%}<variable> in (<set>) do <command> [<commandlinepptions>]
    ```

  - **Iteration eines Wertebereichs:** Verwenden Sie eine iterative Variable, um den Startwert (*Start*Nr.) festzulegen, und durchlaufen Sie dann einen festgelegten Wertebereich, bis der Wert den festgelegten Endwert (*End*#) überschreitet. **/l** führt das iterative durch Vergleichen von *Start*# mit *End*# aus. Wenn " *Start*#" kleiner als " *End*" ist, wird der Befehl ausgeführt. Wenn die iterative Variable den Wert für *End*# überschreitet, beendet die Befehlsshell die Schleife. Sie können auch einen negativen *Schritt*# verwenden, um einen Bereich in abnehmenden Werten schrittweise zu durchlaufen. Beispielsweise generiert (1, 1, 5) die Sequenz 1 2 3 4 5, und (5,-1, 1) generiert die Sequenz 5 4 3 2 1. Die Syntax ist:

    ```
    for /l {%%|%}<variable> in (<start#>,<step#>,<end#>) do <command> [<commandlinepptions>]
    ```

  - **Iteration und Dateiverarbeitung:** Verwenden Sie die Datei--Verarbeitung, um Befehlsausgabe, Zeichen folgen und Dateiinhalte zu verarbeiten. Verwenden Sie iterative Variablen, um die Inhalte oder Zeichen folgen zu definieren, die Sie untersuchen möchten, und verwenden Sie die verschiedenen Optionen für "paramesing *Keywords* ", um die Verarbeitung weiter zu ändern.  Verwenden Sie die Option *parsingkeywords* Token, um anzugeben, welche Token als iterative Variablen übermittelt werden sollen. Beachten Sie, dass **/f** bei Verwendung ohne die Token-Option nur das erste Token untersucht.

    Die Datei-Analyse besteht darin, die Ausgabe-, Zeichen folgen-oder Dateiinhalte zu lesen und Sie dann in einzelne Textzeilen zu unterteilen und jede Zeile in NULL oder mehr Token zu parsen. Die **for** -Schleife wird dann aufgerufen, wobei der Wert der iterativen Variablen auf das Token festgelegt ist. Standardmäßig übergibt **/f** das erste leere getrennte Token von jeder Zeile jeder Datei. Leere Zeilen werden übersprungen.

    Die Syntaxen lauten:

    ```
    for /f [<parsingkeywords>] {%%|%}<variable> in (<set>) do <command> [<commandlinepptions>]
    for /f [<parsingkeywords>] {%%|%}<variable> in (<literalstring>) do <command> [<commandlinepptions>]
    for /f [<parsingkeywords>] {%%|%}<variable> in ('<command>') do <command> [<commandlinepptions>]
    ```

    Das *Set* -Argument gibt mindestens einen Dateinamen an. Alle Dateien werden vor dem Wechsel zur nächsten Datei in *festgelegt*, gelesen und verarbeitet. Um das standardmäßige Parametrisierungsverhalten zu überschreiben, geben Sie " *Parser Keywords*" Dies ist eine Zeichenfolge in Anführungszeichen, die ein oder mehrere Schlüsselwörter enthält, um verschiedene Optionen für die Verarbeitung anzugeben.

    Wenn Sie die Option **usebackq** verwenden, verwenden Sie eine der folgenden Syntaxen:

    ```
    for /f [usebackq <parsingkeywords>] {%%|%}<variable> in (<Set>) do <command> [<commandlinepptions>]
    for /f [usebackq <parsingkeywords>] {%%|%}<variable> in ('<LiteralString>') do <command> [<commandlinepptions>]
    for /f [usebackq <parsingkeywords>] {%%|%}<variable> in (`<command>`) do <command> [<commandlinepptions>]
    ```

    In der folgenden Tabelle sind die Schlüsselwörter aufgeführt, die Sie für die Verwendung von *para*Metern verwenden können.

    | Schlüsselwort | Beschreibung |
    | ------- | ----------- |
    | EOL =`<c>` | Gibt ein Zeilenendezeichen an (nur ein Zeichen). |
    | Skip =`<n>` | Gibt die Anzahl der Zeilen an, die am Anfang der Datei übersprungen werden sollen. |
    | Delta =`<xxx>` | Gibt einen Trenn Zeichensatz an. Dadurch wird das Standard Trennzeichen Set von Space und Tab ersetzt. |
    | Tokens =`<x,y,m–n>` | Gibt an, welche Token aus den einzelnen Zeilen an die **for** -Schleife für jede Iterationen übermittelt werden sollen. Folglich werden zusätzliche Variablennamen zugeordnet. *m-n* gibt einen Bereich an, vom *m*-bis zum *n*-ten Token. Wenn das letzte Zeichen in **Token =** String ein Sternchen (**&#42;**) ist, wird eine zusätzliche Variable zugeordnet und empfängt den verbleibenden Text in der Zeile nach dem letzten analysierten Token. |
    | usebackq | Gibt an, dass eine Zeichenfolge mit einer Zeichenfolge in einer Zeichenfolge als eine Literalzeichenfolge verwendet werden soll, eine Zeichenfolge in einfachen Anführungszeichen als Literalzeichenfolge verwendet werden soll, oder für lange Dateinamen, die Leerzeichen enthalten, `<set>` in doppelte Anführungszeichen eingeschlossen werden. |

  - **Variablen Ersetzung:** In der folgenden Tabelle ist die optionale Syntax (für jede Variable **I**) aufgelistet:

    | Variable mit Modifizierer | Beschreibung |
    | ---------------------- | ----------- |
    |` %~I` | Erweitert `%I` , wodurch alle umgebenden Anführungszeichen entfernt werden. |
    | `%~fI `| Wird `%I` zu einem voll qualifizierten Pfadnamen erweitert. |
    | `%~dI `| Wird `%I` nur auf einen Laufwerk Buchstaben erweitert. |
    | `%~pI` | Wird `%I` nur zu einem Pfad erweitert. |
    | `%~nI `| Wird `%I` nur auf einen Dateinamen erweitert. |
    | `%~xI` | Wird `%I` nur zu einer Dateinamenerweiterung erweitert. |
    | `%~sI` | Erweitert den Pfad, sodass nur Kurznamen enthalten sind. |
    | `%~aI` | Wird `%I` zu den Dateiattributen der Datei erweitert. |
    | `%~tI` | Wird `%I` auf das Datum und die Uhrzeit der Datei erweitert. |
    | `%~zI` | Wird `%I` auf die Größe der Datei erweitert. |
    | `%~$PATH:I` | Durchsucht die Verzeichnisse, die in der PATH-Umgebungsvariablen aufgelistet sind, und erweitert den `%I` voll qualifizierten Namen des ersten gefundenen Verzeichnisses. Wenn der Name der Umgebungsvariablen nicht definiert ist oder die Datei von der Suche nicht gefunden wird, wird dieser Modifizierer auf die leere Zeichenfolge erweitert. |

    In der folgenden Tabelle sind Modifiziererkombinationen aufgelistet, die Sie verwenden können, um zusammengesetzte Ergebnisse zu erhalten.

    | Variable mit kombinierten modifizierervariablen | Beschreibung |
    | -------------------------------- | ----------- |
    | `%~dpI `| Wird `%I` nur zu einem Laufwerk Buchstaben und-Pfad erweitert. |
    | `%~nxI` | Wird `%I` nur auf einen Dateinamen und eine Erweiterung erweitert. |
    | `%~fsI` | Wird `%I` zu einem vollständigen Pfadnamen mit nur Kurznamen erweitert. |
    | `%~dp$PATH:I` | Durchsucht die Verzeichnisse, die in der PATH-Umgebungsvariablen für aufgelistet sind, `%I` und erweitert den Laufwerk Buchstaben und den Pfad des ersten gefundenen Verzeichnisses. |
    | `%~ftzaI` | `%I`Wird zu einer Ausgabezeile erweitert, die wie **dir**aussieht. |

    In den obigen Beispielen können Sie `%I` und path durch andere gültige Werte ersetzen. Ein gültiger **für** Variablenname beendet die **%~** Syntax.

    Mithilfe von Großbuchstaben, wie z `%I` . b., können Sie den Code besser lesbar machen und Verwirrung mit den Modifizierer vermeiden, bei denen die Groß-/Kleinschreibung nicht beachtet wird.

- **Eine Zeichenfolge** wird verarbeitet: Sie können die- `for /f` parameterlogik für eine sofortige Zeichenfolge verwenden `<literalstring>` , indem Sie entweder doppelte Anführungszeichen (*ohne* usebackq) oder in einfache Anführungszeichen (*mit* usebackq) einschließen, z. b. (myString) oder (' myString '). `<literalstring>` wird als eine einzelne Zeile der Eingabe aus einer Datei behandelt. Beim Auswerten `<literalstring>` in doppelten Anführungszeichen werden Befehls Symbole (z. b. `\ & | > < ^` ) als normale Zeichen behandelt.

- **Ausgabe der Ausgabe:** Sie können den `for /f` Befehl verwenden, um die Ausgabe eines Befehls zu analysieren, indem Sie eine backanführungs Zeichen `<command>` zwischen den Klammern platzieren. Sie wird als Befehlszeile behandelt, die an eine untergeordnete Cmd.exe geleitet wird. Die Ausgabe wird im Arbeitsspeicher aufgezeichnet und so analysiert, als ob es sich um eine Datei handelt.

## <a name="examples"></a>Beispiele

Verwenden Sie die folgende Syntax, um **für** in einer Batchdatei zu verwenden:

```
for {%%|%}<variable> in (<set>) do <command> [<commandlineoptions>]
```

Geben Sie Folgendes ein, um den Inhalt aller Dateien im aktuellen Verzeichnis mit der Erweiterung ". doc" oder ". txt" mithilfe der ersetzbaren Variable **% f**anzuzeigen:

```
for %f in (*.doc *.txt) do type %f
```

Im vorherigen Beispiel wird jede Datei mit der Erweiterung ". doc" oder ". txt" im aktuellen Verzeichnis durch die **% f** -Variable ersetzt, bis der Inhalt jeder Datei angezeigt wird. Um diesen Befehl in einer Batchdatei zu verwenden, ersetzen Sie jedes Vorkommen von **% f** durch **%% f**. Andernfalls wird die Variable ignoriert, und es wird eine Fehlermeldung angezeigt.

Geben Sie Folgendes ein, um eine Datei zu analysieren und kommentierte Zeilen zu ignorieren:

```
for /f eol=; tokens=2,3* delims=, %i in (myfile.txt) do @echo %i %j %k
```

Dieser Befehl analysiert jede Zeile in *myfile.txt*. Sie ignoriert Zeilen, die mit einem Semikolon beginnen, und übergibt das zweite und dritte Token von jeder Zeile an den **für** Text (Token werden durch Kommas oder Leerzeichen getrennt). Der Text der **for** -Anweisung verweist auf " **% i** ", um das zweite Token zu erhalten, **% j** , um das dritte Token zu erhalten, und " **% k** ", um alle verbleibenden Token zu erhalten. Wenn die von Ihnen bereitgestellten Dateinamen Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. Dateiname). Zum Verwenden von Anführungszeichen müssen Sie **usebackq**verwenden. Andernfalls werden die Anführungszeichen als Definieren einer Literalzeichenfolge interpretiert, die analysiert werden soll.

**% i** ist explizit in der **for** -Anweisung deklariert. **% j** und **% k** werden implizit mithilfe von **Tokens =** deklariert. Sie können **Tokens =** zum Angeben von bis zu 26 Token verwenden, vorausgesetzt, es wird nicht versucht, eine Variable zu deklarieren, die höher als der Buchstabe z oder z ist.

Um die Ausgabe eines Befehls zu analysieren, indem Sie eine *Menge* zwischen den Klammern platzieren, geben Sie Folgendes ein:

```
for /f usebackq delims== %i in ('set') do @echo %i
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
