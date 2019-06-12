---
title: wenn
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 698b3fb9-532b-4c2b-af7f-179f8dc57131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9751dfe3e0cb0965cc2c5169ea19e0f08110b0ff
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438102"
---
# <a name="if"></a>wenn



Führt die bedingte Verarbeitung in Batchprogrammen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
if [not] ERRORLEVEL <Number> <Command> [else <Expression>]
if [not] <String1>==<String2> <Command> [else <Expression>]
if [not] exist <FileName> <Command> [else <Expression>]
```
Wenn der befehlserweiterungen aktiviert sind, verwenden Sie die folgende Syntax:
```
if [/i] <String1> <CompareOp> <String2> <Command> [else <Expression>]
if cmdextversion <Number> <Command> [else <Expression>]
if defined <Variable> <Command> [else <Expression>]
```

## <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                                                Beschreibung                                                                                                                                                                                                                 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           not           |                                                                                                                                                                              Gibt an, dass der Befehl durchgeführt werden sollte, nur dann, wenn die Bedingung false ergibt.                                                                                                                                                                              |
|  ERRORLEVEL \<Anzahl >   |                                                                                                                                                      Gibt eine Bedingung "true" nur, wenn das vorherige Programm ausführen, indem Cmd.exe einen Exitcode, gleich oder größer als zurückgegeben *Anzahl*.                                                                                                                                                       |
|       \<Befehl >        |                                                                                                                                                                            Gibt den Befehl aus, der ausgeführt werden soll, wenn die vorherige Bedingung erfüllt ist.                                                                                                                                                                             |
|  \<String1>==<String2>  |                                                                                                             Gibt an, nur ein true-Bedingung, wenn *String1* und *Zeichenfolge2* sind identisch. Diese Werte können Literalzeichenfolgen oder Batchvariablen (z. B. "%1") sein. Sie müssen kein literale-Zeichenfolgen in Anführungszeichen einschließen.                                                                                                              |
|    vorhanden \<Dateiname >    |                                                                                                                                                                                       Gibt eine Bedingung "true" an, wenn der angegebene Dateiname vorhanden ist.                                                                                                                                                                                        |
|      \<CompareOp>       |                                                                               Gibt einen drei Buchstaben bestehenden Vergleichsoperator. Die folgende Liste stellt die gültigen Werte für *Vergleichsop*:</br>**EQU** gleich</br>**NEQ** nicht gleich</br>**LSS** kleiner als</br>**LEQ** kleiner als oder gleich</br>**GTR** größer als</br>**GEQ** größer als oder gleich                                                                                |
|           /i            |                                                            Erzwingt, dass bei Zeichenfolgenvergleichen um Groß-und Kleinschreibung ignoriert.  Können Sie **/i** auf die <em>String1</em> **==** <em>Zeichenfolge2</em> Form **Wenn**. Diese Vergleiche sind generisch, wenn beide *String1* und *Zeichenfolge2* bestehen aus numerischen Zeichen nur die Zeichenfolgen in Zahlen konvertiert werden und ein numerischer Vergleich wird ausgeführt.                                                            |
| Cmdextversion \<Anzahl > | Gibt nur einer true-Bedingung, wenn die interne Versionsnummer zugeordnet, mit den befehlserweiterungen, die Funktion von Cmd.exe entspricht oder größer als die angegebene Anzahl an. Die erste Version ist 1. Sie erhöht die Schritten von je 1 mit, wenn bedeutende Verbesserungen an den Befehl Erweiterungen hinzugefügt werden. Die **Cmdextversion** bedingte wird niemals "true" Wenn Befehl Extensions sind deaktiviert (standardmäßig aktiviert sind). |
|   definiert \<Variable >   |                                                                                                                                                                                            Eine Bedingung "true" gibt an, ob *Variable* definiert ist.                                                                                                                                                                                            |
|      \<Ausdruck >      |                                                                                                                                                                   Gibt die Befehlszeile und alle Parameter, in dem Befehl übergeben werden an ein **else** Klausel.                                                                                                                                                                   |
|           /?            |                                                                                                                                                                                                    Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                    |

## <a name="remarks"></a>Hinweise

-   Wenn die Bedingung in angegeben ein **Wenn** -Klausel ist "true", die die Bedingung der nachfolgende Befehl durchgeführt wird. Wenn die Bedingung "false" ist der Befehl in der **Wenn** -Klausel wird ignoriert, und der Befehl führt den Befehl aus, die im angegebenen die **else** Klausel.
-   Wenn ein Programm beendet wird, gibt es einen Exitcode zurück. Für die Verwendung der Exitcodes als Bedingungen verwenden **Errorlevel**.
-   Bei Verwendung von **definiert**, werden die folgenden drei Variablen in der Umgebung hinzugefügt: **%ERRORLEVEL%** , **so %** , und **Cmdextversion %** .  
    -   **%ERRORLEVEL%** in eine Zeichenfolgendarstellung des aktuellen Werts der Umgebungsvariablen ERRORLEVEL erweitert. Dabei wird davon ausgegangen, dass keine vorhandene Umgebungsvariable mit dem Namen ERRORLEVEL – liegt vor, Sie erhalten diesen Wert von ERRORLEVEL stattdessen.
    -   **So %** wird in der ursprünglichen Befehlszeile, die vor der Verarbeitung von Cmd.exe zu Cmd.exe übergeben wurde. Dabei wird davon ausgegangen, dass keine vorhandene Umgebungsvariable mit dem Namen so – liegt, werden Sie stattdessen den so-Wert abrufen.
    -   **Cmdextversion %** wird in eine Zeichenfolgendarstellung des aktuellen Werts der **Cmdextversion**. Dabei wird davon ausgegangen, dass keine vorhandene Umgebungsvariable mit dem Namen CMDEXTVERSION – liegt, werden Sie stattdessen den CMDEXTVERSION-Wert abrufen.
-   Verwenden Sie die **else** Klausel in der gleichen Zeile wie der Befehl nach der **Wenn**.

## <a name="BKMK_examples"></a>Beispiele für

Zum Anzeigen der Nachricht "Datendatei wurde nicht gefunden" Wenn die Datei Product.dat nicht gefunden werden kann, geben:
```
if not exist product.dat echo Cannot find data file 
```
Um eine Diskette in Laufwerk A zu formatieren und eine Fehlermeldung angezeigt, wenn ein Fehler während des Formatierungsvorgangs auftritt, geben Sie die folgenden Zeilen in einer Batchdatei aus:
```
:begin
@echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program.
```
Löschen Sie die Datei Product.dat aus dem aktuellen Verzeichnis oder eine Meldung angezeigt, wenn Product.dat nicht gefunden wird, geben Sie die folgenden Zeilen in einer Batchdatei aus:
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
> Um den Wert der Umgebungsvariablen ERRORLEVEL echo nach einer Batchdatei ausführen, geben Sie die folgenden Zeilen in der Batchdatei:
> ```
> goto answer%errorlevel%
> :answer1
> echo Program had return code 1
> :answer0
> echo Program had return code 0
> goto end
> :end
> echo Done! 
> ```
> So gehen auf die Bezeichnung "OK", wenn der Wert der Umgebungsvariablen ERRORLEVEL kleiner als oder gleich 1, Typ ist ein:
> ```
> if %errorlevel% LEQ 1 goto okay
> ```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[If](if.md)

[Goto](goto.md)