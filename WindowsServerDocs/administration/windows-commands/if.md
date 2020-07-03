---
title: if
description: Referenz Artikel zum if-Befehl, der die bedingte Verarbeitung in Batch Programmen ausführt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 698b3fb9-532b-4c2b-af7f-179f8dc57131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd55ebb6ae3562906efdc710f7a067a7e7514e59
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924471"
---
# <a name="if"></a>if

Führt die bedingte Verarbeitung in Batch Programmen aus.

## <a name="syntax"></a>Syntax

```
if [not] ERRORLEVEL <number> <command> [else <expression>]
if [not] <string1>==<string2> <command> [else <expression>]
if [not] exist <filename> <command> [else <expression>]
```

Wenn Befehls Erweiterungen aktiviert sind, verwenden Sie die folgende Syntax:

```
if [/i] <string1> <compareop> <string2> <command> [else <expression>]
if cmdextversion <number> <command> [else <expression>]
if defined <variable> <command> [else <expression>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- |------------ |
| not | Gibt an, dass der Befehl nur ausgeführt werden soll, wenn die Bedingung false ist. |
| ERRORLEVEL`<number>` | Gibt eine echte Bedingung nur dann an, wenn das vorherige Programm, das von Cmd.exe ausgeführt wird, einen Exitcode zurückgegeben hat, der gleich oder *größer als* |
| `<command>` | Gibt den Befehl an, der ausgeführt werden soll, wenn die vorangehende Bedingung erfüllt ist. |
| `<string1>==<string2>` | Gibt eine echte Bedingung nur an, wenn *Zeichenfolge1* und *Zeichenfolge2* identisch sind. Diese Werte können Literalzeichenfolgen oder Batch Variablen (z `%1` . b.) sein. Sie müssen keine Literalzeichenfolgen in Anführungszeichen einschließen. |
| existierten`<filename>` | Gibt eine echte Bedingung an, wenn der angegebene Dateiname vorhanden ist. |
| `<compareop>` | Gibt einen Vergleichs Operator mit drei Buchstaben an, einschließlich:<ul><li>**EQU** -gleich</li><li>**NEQ** Nicht gleich</li><li>**LSS** -kleiner als</li><li>**Leq** -kleiner als oder gleich</li><li>**GTR** (größer als)</li><li>**GEQ** -größer als oder gleich</li></ul> |
| /i | Erzwingt die Groß-/Kleinschreibung von Zeichen folgen vergleichen Sie können **/i** im Format verwenden, `string1==string2` **Wenn**. Diese Vergleiche sind generisch, d. h., wenn sowohl *Zeichenfolge1* als auch *Zeichenfolge2* nur aus numerischen Ziffern bestehen, werden die Zeichen folgen in Zahlen konvertiert, und es wird ein numerischer Vergleich ausgeführt. |
| cmdextversion`<number>` | Gibt eine echte Bedingung nur an, wenn die interne Versionsnummer, die dem Befehls Erweiterungs Feature von Cmd.exe zugeordnet ist, größer oder gleich der angegebenen Zahl ist. Die erste Version ist 1. Sie vergrößert sich um einen Schritt von 1, wenn den Befehls Erweiterungen bedeutende Erweiterungen hinzugefügt werden. Die bedingte **cmdextversion** ist nie true, wenn Befehls Erweiterungen deaktiviert sind (Standardmäßig sind die Befehls Erweiterungen aktiviert). |
| defined `<variable>` | Gibt eine echte Bedingung an, wenn *Variable* definiert ist. |
| `<expression>` | Gibt einen Befehlszeilen Befehl und alle Parameter an, die an den Befehl in einer **else** -Klausel weitergegeben werden sollen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn die in einer **if** -Klausel angegebene Bedingung true ist, wird der Befehl ausgeführt, der der Bedingung folgt. Wenn die Bedingung false ist, wird der Befehl in der **if** -Klausel ignoriert, und der Befehl führt jeden Befehl aus, der in der **else** -Klausel angegeben ist.

- Wenn ein Programm beendet wird, wird ein Exitcode zurückgegeben. Um Exitcodes als Bedingungen zu verwenden, verwenden Sie den **ERRORLEVEL** -Parameter.

- Wenn Sie **defined**verwenden, werden die folgenden drei Variablen der Umgebung hinzugefügt: **% ERRORLEVEL%**, **% cmdcmdline%** und **% cmdextversion%**.

  - **% ERRORLEVEL%**: wird in eine Zeichen folgen Darstellung des aktuellen Werts der Umgebungsvariablen ERRORLEVEL erweitert. Diese Variable geht davon aus, dass noch keine Umgebungsvariable mit dem Namen ERRORLEVEL vorhanden ist. Wenn dies der Fall ist, erhalten Sie stattdessen den Wert ERRORLEVEL.

  - **% cmdcmdline%**: wird in die ursprüngliche Befehlszeile erweitert, die vor der Verarbeitung durch Cmd.exe an Cmd.exe übergeben wurde. Dabei wird davon ausgegangen, dass noch keine Umgebungsvariable mit dem Namen "cmdcmdline" vorhanden ist. Wenn dies der Fall ist, erhalten Sie stattdessen diesen cmdcmdline-Wert.

  - **% cmdextversion%**: wird in die Zeichen folgen Darstellung des aktuellen Werts von **cmdextversion**erweitert. Dabei wird davon ausgegangen, dass noch keine Umgebungsvariable mit dem Namen "cmdextversion" vorhanden ist. Wenn dies der Fall ist, erhalten Sie stattdessen den Wert cmdextversion.

- Sie müssen die **else** -Klausel in derselben Zeile wie der Befehl nach dem **if**-Befehl verwenden.

### <a name="examples"></a>Beispiele

Wenn die Meldung **nicht gefunden werden kann, wenn die Datei Product. dat nicht gefunden werden kann**, geben Sie Folgendes ein:

```
if not exist product.dat echo Cannot find data file
```

Um einen Datenträger in Laufwerk a zu formatieren und eine Fehlermeldung anzuzeigen, wenn während des Formatierungs Vorgangs ein Fehler auftritt, geben Sie in einer Batchdatei die folgenden Zeilen ein:

```
:begin
@echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program.
```

Wenn Sie die Datei Product. dat aus dem aktuellen Verzeichnis löschen oder eine Meldung anzeigen möchten, wenn Product. dat nicht gefunden wird, geben Sie die folgenden Zeilen in eine Batchdatei ein:

```
IF EXIST Product.dat (
del Product.dat
) ELSE (
echo The Product.dat file is missing.
)
```

> [!NOTE]
> Diese Zeilen können wie folgt in eine einzelne Zeile kombiniert werden:
> ```
> IF EXIST Product.dat (del Product.dat) ELSE (echo The Product.dat file is missing.)
> ```

Geben Sie die folgenden Zeilen in der Batchdatei ein, um den Wert der Umgebungsvariablen ERRORLEVEL nach dem Ausführen einer Batchdatei widerzuspiegeln:

```
goto answer%errorlevel%
:answer1
echo The program returned error level 1
goto end
:answer0
echo The program returned error level 0
goto end
:end
echo Done!
```

Wenn der Wert der Umgebungsvariablen ERRORLEVEL kleiner oder gleich 1 sein soll, geben Sie Folgendes ein, um zur okay-Bezeichnung zu wechseln:

```
if %errorlevel% LEQ 1 goto okay
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [GOTO-Befehl](goto.md)
