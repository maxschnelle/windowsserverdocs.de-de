---
title: wenn
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 698b3fb9-532b-4c2b-af7f-179f8dc57131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 706ac1569ac3ca7ae504410935f334be360eda3a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842233"
---
# <a name="if"></a>wenn



Führt die bedingte Verarbeitung in Batch Programmen aus.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
if [not] ERRORLEVEL <Number> <Command> [else <Expression>]
if [not] <String1>==<String2> <Command> [else <Expression>]
if [not] exist <FileName> <Command> [else <Expression>]
```
Wenn Befehls Erweiterungen aktiviert sind, verwenden Sie die folgende Syntax:
```
if [/i] <String1> <CompareOp> <String2> <Command> [else <Expression>]
if cmdextversion <Number> <Command> [else <Expression>]
if defined <Variable> <Command> [else <Expression>]
```

### <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                                                Beschreibung                                                                                                                                                                                                                 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           not           |                                                                                                                                                                              Gibt an, dass der Befehl nur ausgeführt werden soll, wenn die Bedingung false ist.                                                                                                                                                                              |
|  ERRORLEVEL-\<Anzahl >   |                                                                                                                                                      Gibt eine echte Bedingung nur an, wenn das vorherige Programm, das von "cmd. exe" ausgeführt wird, einen *Number*Exitcode zurückgegeben hat, der größer oder gleich                                                                                                                                                       |
|       \<Befehl >        |                                                                                                                                                                            Gibt den Befehl an, der ausgeführt werden soll, wenn die vorangehende Bedingung erfüllt ist.                                                                                                                                                                             |
|  \<Zeichenfolge1 > = =<String2>  |                                                                                                             Gibt eine echte Bedingung nur an, wenn *Zeichenfolge1* und *Zeichenfolge2* identisch sind. Diese Werte können Literalzeichenfolgen oder Batch Variablen (z. b. %1) sein. Sie müssen keine Literalzeichenfolgen in Anführungszeichen einschließen.                                                                                                              |
|    \<Dateiname vorhanden >    |                                                                                                                                                                                       Gibt eine echte Bedingung an, wenn der angegebene Dateiname vorhanden ist.                                                                                                                                                                                        |
|      \<compareop->       |                                                                               Gibt einen Vergleichs Operator mit drei Buchstaben an. Die folgende Liste stellt gültige Werte für *compareop*dar:</br>**EQU** Gleich</br>" **NQ** " Ungleich</br>**LSS** Kleiner als</br>**Leq** Kleiner als oder gleich</br>**GTR** Größer als</br>**GEQ** Größer als oder gleich                                                                                |
|           /i            |                                                            Erzwingt die Groß-/Kleinschreibung von Zeichen folgen vergleichen  Sie können **/i** im Zeichenfolge1- <em>String1</em> **==** <em>Zeichenfolge2</em> -Format von **if**verwenden. Diese Vergleiche sind generisch, d. h., wenn sowohl *Zeichenfolge1* als auch *Zeichenfolge2* nur aus numerischen Ziffern bestehen, werden die Zeichen folgen in Zahlen konvertiert, und es wird ein numerischer Vergleich ausgeführt.                                                            |
| cmdextversion \<Anzahl > | Gibt eine echte Bedingung nur an, wenn die der Befehls Erweiterungs Funktion von "cmd. exe" zugeordnete interne Versionsnummer größer oder gleich der angegebenen Zahl ist. Die erste Version ist 1. Sie vergrößert sich um einen Schritt von 1, wenn den Befehls Erweiterungen bedeutende Erweiterungen hinzugefügt werden. Die bedingte **cmdextversion** ist nie true, wenn Befehls Erweiterungen deaktiviert sind (Standardmäßig sind die Befehls Erweiterungen aktiviert). |
|   definiert \<Variable >   |                                                                                                                                                                                            Gibt eine echte Bedingung an, wenn *Variable* definiert ist.                                                                                                                                                                                            |
|      \<Ausdrucks >      |                                                                                                                                                                   Gibt einen Befehlszeilen Befehl und alle Parameter an, die an den Befehl in einer **else** -Klausel weitergegeben werden sollen.                                                                                                                                                                   |
|           /?            |                                                                                                                                                                                                    Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                    |

## <a name="remarks"></a>Hinweise

-   Wenn die in einer **if** -Klausel angegebene Bedingung true ist, wird der Befehl ausgeführt, der der Bedingung folgt. Wenn die Bedingung false ist, wird der Befehl in der **if** -Klausel ignoriert, und der Befehl führt jeden Befehl aus, der in der **else** -Klausel angegeben ist.
-   Wenn ein Programm beendet wird, wird ein Exitcode zurückgegeben. Verwenden Sie **ERRORLEVEL**, um Exitcodes als Bedingungen zu verwenden.
-   Wenn Sie **defined**verwenden, werden die folgenden drei Variablen der Umgebung hinzugefügt: **% ERRORLEVEL%** , **% cmdcmdline%** und **% cmdextversion%** .  
    -   **% ERRORLEVEL%** wird in eine Zeichen folgen Darstellung des aktuellen Werts der Umgebungsvariablen ERRORLEVEL erweitert. Dabei wird davon ausgegangen, dass es keine vorhandene Umgebungsvariable mit dem Namen ERRORLEVEL gibt – wenn dies der Fall ist, erhalten Sie stattdessen den ERRORLEVEL-Wert.
    -   **% cmdcmdline%** wird in die ursprüngliche Befehlszeile erweitert, die vor der Verarbeitung durch "cmd. exe" an "cmd. exe" übergeben wurde. Dabei wird davon ausgegangen, dass es keine vorhandene Umgebungsvariable mit dem Namen "cmdcmdline" gibt – wenn dies der Fall ist, wird stattdessen der cmdcmdline-Wert angezeigt.
    -   **% cmdextversion%** wird in die Zeichen folgen Darstellung des aktuellen Werts von **cmdextversion**erweitert. Dabei wird davon ausgegangen, dass es keine vorhandene Umgebungsvariable mit dem Namen "cmdextversion –" gibt. wenn dies der Fall ist, wird stattdessen der cmdextversion-Wert angezeigt.
-   Sie müssen die **else** -Klausel in derselben Zeile wie der Befehl nach dem **if**-Befehl verwenden.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Wenn die Meldung nicht gefunden werden kann, wenn die Datei Product. dat nicht gefunden werden kann, geben Sie Folgendes ein:
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
> Geben Sie die folgenden Zeilen in der Batchdatei ein, um den Wert der Umgebungsvariablen ERRORLEVEL nach dem Ausführen einer Batchdatei widerzuspiegeln:
> ```
> goto answer%errorlevel%
> :answer1
> echo The program returned error level 1
> goto end
> :answer0
> echo The program returned error level 0
> goto end
> :end
> echo Done! 
> ```
> Wenn der Wert der Umgebungsvariablen ERRORLEVEL kleiner oder gleich 1 sein soll, geben Sie Folgendes ein, um zur okay-Bezeichnung zu wechseln:
> ```
> if %errorlevel% LEQ 1 goto okay
> ```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Sei](if.md)

[GOTO](goto.md)
