---
title: set
description: Referenz Artikel für Set, mit dem cmd.exe-Umgebungsvariablen angezeigt, festgelegt oder entfernt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5fdd60d6-addf-4574-8c92-8aa53fa73d76
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 002ac4624d9ed501fab7816a83c2a0c5fc6a2bce
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922825"
---
# <a name="set"></a>set

Zeigt cmd.exe Umgebungsvariablen an, legt Sie fest oder entfernt Sie. Bei Verwendung ohne Parameter zeigt **Set** die aktuellen Umgebungsvariablen Einstellungen an.



## <a name="syntax"></a>Syntax

```
set [<Variable>=[<String>]]
set [/p] <Variable>=[<PromptString>]
set /a <Variable>=<Expression>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Variable>|Gibt die Umgebungsvariable an, die festgelegt oder geändert werden soll.|
|\<String>|Gibt die Zeichenfolge an, die der angegebenen Umgebungsvariablen zugeordnet werden soll.|
|/p|Legt den Wert der *Variablen* auf eine Zeile der Eingabe fest, die vom Benutzer eingegeben wurde.|
|\<PromptString>|Dies ist optional. Gibt eine Meldung an, mit der der Benutzer zur Eingabe aufgefordert wird. Dieser Parameter wird mit der Befehlszeilenoption **/p** verwendet.|
|/a|Legt die *Zeichenfolge* auf einen numerischen Ausdruck fest, der ausgewertet wird.|
|\<Expression>|Gibt einen numerischen Ausdruck an. Informationen zu gültigen Operatoren, die in *Ausdrücken*verwendet werden können, finden Sie unter Hinweise.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Verwenden von **Set** mit aktivierten Befehls Erweiterungen

  Wenn Befehls Erweiterungen aktiviert sind (Standardeinstellung) und Sie **Set** mit einem Wert ausführen, werden alle Variablen angezeigt, die mit diesem Wert beginnen.
- Verwenden von Sonderzeichen

  Die Zeichen **<** , **>** , **|** , **&** , **^** sind spezielle befehlsshellzeichen, und Ihnen muss das Escapezeichen () vorangestellt **^** oder in Anführungszeichen eingeschlossen werden, wenn Sie in einer *Zeichenfolge* verwendet werden (z. b. **stringenthaltende&Symbol**). Wenn Sie eine Zeichenfolge, die eines der Sonderzeichen enthält, in Anführungszeichen einschließen, werden diese als Teil des Werts der Umgebungsvariable festgelegt.
- Verwenden von Umgebungsvariablen

  Verwenden Sie Umgebungsvariablen, um das Verhalten einiger Batch Dateien und-Programme zu steuern und die Art und Weise zu steuern, wie Windows und das MS-DOS-Subsystem angezeigt werden und funktionieren. Der **Set** -Befehl wird häufig in der Datei Autoexec. NT verwendet, um Umgebungsvariablen festzulegen.
- Anzeigen der aktuellen Umgebungseinstellungen

  Wenn Sie den **Set** -Befehl allein eingeben, werden die aktuellen Umgebungseinstellungen angezeigt. Diese Einstellungen umfassen in der Regel die Umgebungsvariablen COMSPEC und Path, die zur Suche nach Programmen auf dem Datenträger verwendet werden. Zwei andere Umgebungsvariablen, die von Windows verwendet werden, sind prompt und DIRCMD.
- Verwenden von Parametern

  Wenn Sie Werte für *Variable* und *Zeichenfolge*angeben, wird der angegebene *Variablen* Wert der Umgebung hinzugefügt, und die *Zeichenfolge* ist dieser Variablen zugeordnet. Wenn die Variable bereits in der Umgebung vorhanden ist, ersetzt der neue Zeichen folgen Wert den alten Zeichen folgen Wert.

  Wenn Sie nur eine Variable und ein Gleichheitszeichen (ohne *Zeichenfolge*) für den **set** -Befehl angeben, wird der *Zeichen* folgen Wert, der der Variablen zugeordnet ist, gelöscht (als ob die Variable nicht vorhanden ist).
- Verwenden von **/a**

  In der folgenden Tabelle sind die Operatoren aufgeführt, die für **/a** in absteigender Rangfolge unterstützt werden.

  |        Betreiber         | Ausgeführte Operation  |
  |-------------------------|----------------------|
  |           ( )           |       Gruppierung       |
  |          ! ~ -          |        Unäroperatoren         |
  |         \* / %          |      Arithmetik      |
  |           + -           |      Arithmetik      |
  |          << >>          |    Logische Verschiebung     |
  |            &            |     Bitweises AND      |
  |            ^            | Bitweises exklusives OR |
  |                         |                      |
  | = \*=/=% = + =-= &= ^ = |      = <<= >>=       |
  |            ,            | Ausdrucks Trennzeichen |

  Wenn Sie logische **&&** **||** Operatoren (oder) oder Modulo ( **%** )-Operatoren verwenden, schließen Sie die Ausdrucks Zeichenfolge in Anführungszeichen ein. Alle nicht numerischen Zeichen folgen im Ausdruck werden als Umgebungsvariablen Namen betrachtet, und ihre Werte werden in Zahlen konvertiert, bevor Sie verarbeitet werden. Wenn Sie einen Umgebungsvariablen Namen angeben, der nicht in der aktuellen Umgebung definiert ist, wird der Wert NULL zugewiesen, sodass Sie arithmetische Werte mit Umgebungsvariablen Werten ausführen können, ohne das% zum Abrufen eines Werts zu verwenden.

  Wenn Sie **Set/a** über die Befehlszeile außerhalb eines Befehls Skripts ausführen, wird der endgültige Wert des Ausdrucks angezeigt.

  Numerische Werte sind Dezimalzahlen, es sei denn, Sie werden für hexadezimal Zahlen mit 0 × vorangestellt. Daher ist 0 × 12 identisch mit 18, was mit 022 identisch ist.
- Unterstützen der Erweiterung für verzögerte Umgebungsvariablen

  Die Unterstützung für die verzögerte Erweiterung von Umgebungsvariablen ist standardmäßig deaktiviert. Sie können Sie jedoch mithilfe von **cmd/v**aktivieren oder deaktivieren.
- Arbeiten mit Befehls Erweiterungen

  Wenn Befehls Erweiterungen aktiviert sind (Standardeinstellung) und Sie **Set** allein ausführen, werden alle aktuellen Umgebungsvariablen angezeigt. Wenn Sie **Set** mit einem Wert ausführen, werden die Variablen angezeigt, die mit diesem Wert zu vergleichen sind.
- Verwenden von **Set** in Batch Dateien

  Beim Erstellen von Batch Dateien können Sie **Set** verwenden, um Variablen zu erstellen, und Sie dann auf die gleiche Weise wie die nummerierten Variablen **%0** bis **%9**verwenden. Sie können auch die Variablen **%0** bis **%9** als Eingabe für **set**verwenden.
- Aufrufen einer **Set** -Variablen aus einer Batchdatei

  Wenn Sie einen variablen Wert aus einer Batchdatei aufzurufen, müssen Sie den Wert in Prozentzeichen ( **%** ) einschließen. Wenn Ihr Batch-Programm z. b. eine Umgebungsvariable mit dem Namen Baud erstellt, können Sie die Zeichenfolge, die der Baudrate zugeordnet ist, als ersetzbaren Parameter verwenden, indem Sie **% Baud%** an der Eingabeaufforderung eingeben
- Verwenden von **Set** in der Wiederherstellungskonsole

  Der **Set** -Befehl mit unterschiedlichen Parametern ist über die Wiederherstellungskonsole verfügbar.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Umgebungsvariable mit dem Namen Test ^ 1 festzulegen:
```
set testVar=test^^1
```

> [!NOTE]
> Mit dem **Set** -Befehl werden alle Elemente, die dem Gleichheitszeichen (=) folgen, dem Wert der Variablen zugewiesen. Wenn Sie Folgendes eingeben:
> ```
> set testVar=test^1
> ```
> Sie erhalten folgendes Ergebnis:
> ```
> testVar=test^1
> ```
> Geben Sie Folgendes ein, um eine Umgebungsvariable mit dem Namen Test&1 festzulegen:
> ```
> set testVar=test^&1
> ```
> Geben Sie Folgendes ein, um eine Umgebungsvariable mit dem Namen include so festzulegen, dass die Zeichenfolge c:\inc (das Verzeichnis \inc auf Laufwerk C) damit verknüpft ist:
> ```
> set include=c:\inc
> ```
> Anschließend können Sie die Zeichenfolge c:\inc in Batch Dateien verwenden, indem Sie den Namen include in Prozentzeichen ( **%** ) einschließen. Beispielsweise können Sie den folgenden Befehl in eine Batchdatei einschließen, damit Sie den Inhalt des Verzeichnisses anzeigen können, das der INCLUDE-Umgebungsvariablen zugeordnet ist:
> ```
> dir %include%
> ```
> Wenn dieser Befehl verarbeitet wird, ersetzt die Zeichenfolge c:\inc **% include%**.

Sie können auch **Set** in einem Batch-Programm verwenden, das der PATH-Umgebungsvariablen ein neues Verzeichnis hinzufügt. Beispiel:
```
@echo off
rem ADDPATH.BAT adds a new directory
rem to the path environment variable.
set path=%1;%path%
set
```
Zum Anzeigen einer Liste aller Umgebungsvariablen, die mit dem Buchstaben "P" beginnen, geben Sie Folgendes ein:
```
set p
```

> [!NOTE]
> Dieser Befehl erfordert Befehls Erweiterungen, die standardmäßig aktiviert sind.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)