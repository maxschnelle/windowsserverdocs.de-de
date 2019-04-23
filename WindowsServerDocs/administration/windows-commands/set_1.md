---
title: set
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fdd60d6-addf-4574-8c92-8aa53fa73d76
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ece1581bad3d78add93a5bac2c4331ebc5240eef
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882131"
---
# <a name="set"></a>set



Zeigt an, legt fest oder entfernt cmd ein. EXE-Umgebungsvariablen. Wenn Sie ohne Angabe von Parametern **festgelegt** zeigt die aktuellen variableneinstellungen der Umgebung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
set [<Variable>=[<String>]]
set [/p] <Variable>=[<PromptString>]
set /a <Variable>=<Expression>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Variable>|Gibt an, die Umgebungsvariable festlegen oder ändern.|
|\<String>|Gibt die Zeichenfolge, die angegebene Umgebungsvariable zugeordnet werden soll.|
|/p|Legt den Wert der *Variable* zu einer Zeile der Eingabe, die vom Benutzer eingegeben werden.|
|\<PromptString>|Optional. Gibt an, eine Nachricht an den Benutzer zur Eingabe aufzufordern. Dieser Parameter wird verwendet, mit der **/p** Befehlszeilenoption.|
|/a|Legt *Zeichenfolge* auf einen numerischen Ausdruck, der ausgewertet wird.|
|\<Ausdruck >|Gibt einen numerischen Ausdruck. Siehe Hinweise für gültige Operatoren, die verwendet werden können *Ausdruck*.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Mithilfe von **festgelegt** mit befehlserweiterungen aktiviert

    Wenn befehlserweiterungen sind aktiviert (Standard), und führen Sie **festgelegt** mit einem Wert, es zeigt alle Variablen, die mit diesem Wert beginnen.
-   Verwenden von Sonderzeichen

    Die Zeichen **<**, **>**, **|**, **&**, **^** sind spezielle Befehl-Shell-Zeichen, und sie müssen das Escape-Zeichen stehen (**^**) oder eingeschlossen in Anführungszeichen, bei der Verwendung in *Zeichenfolge* (z. B. **"Befehlszeilenzeichen & Symbol"**). Wenn Sie Anführungszeichen verwenden, um eine Zeichenfolge einzuschließen, die einen der Sonderzeichen enthält, werden die Anführungszeichen als Teil des Werts der Umgebungsvariable festgelegt.
-   Verwenden von Umgebungsvariablen

    Verwenden von Umgebungsvariablen zum Steuern des Verhaltens einiger Batchdateien und-Programme und Steuerung von der Möglichkeit Windows und MS-DOS-Subsystem wird angezeigt und funktioniert. Die **festgelegt** Befehl wird oft in die Datei verwendet, um Umgebungsvariablen festzulegen.
-   Zeigt die aktuelle umgebungseinstellungen

    Bei der Eingabe der **festgelegt** Befehl, die aktuellen umgebungseinstellungen werden angezeigt. Diese Einstellungen umfassen in der Regel die Umgebungsvariablen COMSPEC und den Pfad, die verwendet werden, um Programme auf dem Datenträger zu finden. Zwei andere Umgebungsvariablen, die von Windows verwendet werden, PROMPT und DIRCMD.
-   Verwenden von Parametern

    Wenn Sie geben Werte für *Variable* und *Zeichenfolge*, den angegebenen *Variable* Wert wird in der Umgebung hinzugefügt und *Zeichenfolge* ist die Variable zugeordnet ist. Wenn die Variable in der Umgebung bereits vorhanden ist, ersetzt der neue Zeichenfolgenwert den alte Zeichenfolgenwert.

    Bei Angabe von nur einer Variablen, einem Gleichheitszeichen (ohne *Zeichenfolge*) für die **festgelegt** Befehl aus, die *Zeichenfolge* Wert der Variablen zugeordnet ist (als ob die Variable ist deaktiviert. nicht vorhanden).
-   Mithilfe von   **/a**

    Die folgende Tabelle enthält die Operatoren für unterstützt **/a** in absteigender Reihenfolge.  
    |Operator|Vorgang|
    |--------|-------------------|
    |( )|Gruppieren|
    |! ~ -|Unär|
    |* / %|arithmetische Operationen|
    |+ -|arithmetische Operationen|
    |<< >>|Logische Verschiebung|
    |&|Bitweises AND|
    |^|Bitweises exklusives OR|
    |||Bitweise OR-Operation|
    |= *= /= %= += -= &= ^= |= <<= >>=|Assignment|
    |,|Expression-Trennzeichen|

    Bei Verwendung von logischen (**&&** oder **||**) Modulo (**%**) Operatoren müssen die Ausdruckszeichenfolge in Anführungszeichen einschließen. Numerische Zeichenfolgen im Ausdruck werden als Umgebungsvariablen betrachtet, und ihre Werte werden in Zahlen konvertiert, bevor sie verarbeitet werden. Wenn Sie ein Name der Umgebungsvariablen, die nicht in der aktuellen Umgebung definiert ist angeben, wird der Wert 0 (null) zugewiesen, können Sie Arithmetik mit Umgebungsvariablenwerte ausführen, ohne die % zum Abrufen eines Werts.

    Wenn das Ausführen **set/a** über die Befehlszeile außerhalb ein Befehlsskript, wird den endgültigen Wert des Ausdrucks.

    Numerische Werte sind Dezimalzahlen, es sei denn, 0 × für Hexadezimalzahlen oder 0 für oktale Zahlen vorangestellt. Aus diesem Grund entspricht 0 x 12-18, d.h. 022 identisch.
-   Unterstützung des verzögerten Erweiterung von Umgebungsvariablen

    Verzögerte Umgebung variablenerweiterung Unterstützung ist standardmäßig deaktiviert, jedoch können Sie aktivieren oder deaktivieren Sie es mit **Cmd/v**.
-   Arbeiten mit befehlserweiterungen

    Befehlserweiterungen sind aktiviert, wenn (Standard), und führen Sie Sie **festgelegt** , alle aktuellen Umgebungsvariablen angezeigt. Wenn das Ausführen **festgelegt** mit einem Wert für die Variablen, die diesem Wert entsprechen wird.
-   Mithilfe von **festgelegt** in Batchdateien

    Wenn Sie Batch-Dateien zu erstellen, können Sie **festgelegt** Variablen erstellen und verwenden Sie diese dann auf die gleiche Weise, dass Sie die nummerierten Variablen verwenden würden **%0** über **%9**. Sie können auch die Variablen **%0** über **%9** als Eingabe für **festgelegt**.
-   Aufrufen einer **festgelegt** Variablen aus einer Batchdatei

    Wenn Sie einen Wert der Variablen von einer Batchdatei aus aufrufen, müssen Sie den Wert in Prozentzeichen (**%**). Z. B. Wenn Ihr Batchprogramm eine Umgebungsvariable namens BAUD erstellt, können die zugeordnete Zeichenfolge BAUD als ein ersetzbarer Parameter durch Eingabe **Baud %** an der Eingabeaufforderung.
-   Mithilfe von **festgelegt** in der Wiederherstellungskonsole

    Die **festgelegt** -Befehl, mit verschiedenen Parametern finden Sie in der Wiederherstellungskonsole.

## <a name="BKMK_examples"></a>Beispiele für

Eine Umgebungsvariable namens TEST festgelegt ^ 1, Typ:
```
set testVar=test^^1
```

> [!NOTE]
> Die **festgelegt** Befehl weist alles, was das Gleichheitszeichen (=) auf den Wert der Variablen folgt. Wenn Sie eingeben:
```
set testVar="test^1"
```
Sie erhalten Folgendes Ergebnis:
```
testVar="test^1"
```
Zum Festlegen einer Umgebungsvariablen mit dem Namen "TEST & 1, Typ":
```
set testVar=test^&1
```
Zum Festlegen einer Umgebungsvariable EINSCHLIEßEN, damit die Zeichenfolge C:\Inc (\Inc Verzeichnis auf Laufwerk C) zugeordnet ist, geben Sie Folgendes ein:
```
set include=c:\inc
```
Sie können dann die Zeichenfolge C:\Inc in Batchdateien verwenden, durch den Namen "INCLUDE" in Prozentzeichen einschließen (**%**). Sie können z. B. den folgenden Befehl in einer Batchdatei einschließen, damit Sie den Inhalt des Verzeichnisses anzeigen können, die die INCLUDE-Umgebungsvariable zugeordnet ist:
```
dir %include%
```
Wenn dieser Befehl verarbeitet wird, ersetzt die Zeichenfolge C:\Inc **% enthalten %**.

Sie können auch **festgelegt** in einem Batchprogramm, das der Umgebungsvariablen PATH enthalten ein neues Verzeichnis hinzufügt. Zum Beispiel:
```
@echo off
rem ADDPATH.BAT adds a new directory
rem to the path environment variable.
set path=%1;%path%
set
```
Um eine Liste aller von der Umgebungsvariablen anzuzeigen, die mit dem Buchstaben P beginnen, geben Sie Folgendes ein:
```
set p 
```

> [!NOTE]
> Dieser Befehl erfordert befehlserweiterungen, die standardmäßig aktiviert sind.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)