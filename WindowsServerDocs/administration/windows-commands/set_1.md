---
title: set
description: Referenz Artikel für Set, mit dem cmd.exe-Umgebungsvariablen angezeigt, festgelegt oder entfernt werden.
ms.topic: reference
ms.assetid: 5fdd60d6-addf-4574-8c92-8aa53fa73d76
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2f53655aa344e1770c9483e5302885734c389837
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389028"
---
# <a name="set-environment-variable"></a>Set (Umgebungsvariable)

Zeigt cmd.exe Umgebungsvariablen an, legt Sie fest oder entfernt Sie. Bei Verwendung ohne Parameter zeigt **Set** die aktuellen Umgebungsvariablen Einstellungen an.

> [!NOTE]
> Dieser Befehl erfordert Befehls Erweiterungen, die standardmäßig aktiviert sind.

Der **Set** -Befehl kann auch in der Windows-Wiederherstellungskonsole mit unterschiedlichen Parametern ausgeführt werden. Weitere Informationen finden Sie in der [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

## <a name="syntax"></a>Syntax

```
set [<variable>=[<string>]]
set [/p] <variable>=[<promptString>]
set /a <variable>=<expression>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<variable>` | Gibt die Umgebungsvariable an, die festgelegt oder geändert werden soll. |
| `<string>` | Gibt die Zeichenfolge an, die der angegebenen Umgebungsvariablen zugeordnet werden soll. |
| /p | Legt den Wert von `<variable>` auf eine Zeile der Eingabe fest, die vom Benutzer eingegeben wurde. |
| `<promptstring>` | Gibt eine Meldung an, mit der der Benutzer zur Eingabe aufgefordert wird. Dieser Parameter muss mit dem **/p** -Parameter verwendet werden. |
| /a | Legt `<string>` auf einen numerischen Ausdruck fest, der ausgewertet wird. |
| `<expression>` | Gibt einen numerischen Ausdruck an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn Befehls Erweiterungen aktiviert sind (Standardeinstellung) und Sie **Set** mit einem Wert ausführen, werden alle Variablen angezeigt, die mit diesem Wert beginnen.

- Die Zeichen,, `<` `>` `|` , `&` und `^` sind spezielle befehlsshellzeichen, und Ihnen muss das Escapezeichen () vorangestellt werden, oder Sie müssen `^` in Anführungszeichen eingeschlossen werden, wenn Sie in verwendet werden `<string>` (z. b. "stringenthaltende&Symbol"). Wenn Sie eine Zeichenfolge, die eines der Sonderzeichen enthält, in Anführungszeichen einschließen, werden diese als Teil des Werts der Umgebungsvariable festgelegt.

- Verwenden Sie Umgebungsvariablen, um das Verhalten einiger Batch Dateien und-Programme zu steuern und die Art und Weise zu steuern, wie Windows und das MS-DOS-Subsystem angezeigt werden und funktionieren. Der **Set** -Befehl wird häufig in der Datei **Autoexec. NT** verwendet, um Umgebungsvariablen festzulegen.

- Wenn Sie den **Set** -Befehl ohne Parameter verwenden, werden die aktuellen Umgebungseinstellungen angezeigt. Diese Einstellungen umfassen in der Regel die Umgebungsvariablen **COMSPEC** und **path** , die zur Suche nach Programmen auf dem Datenträger verwendet werden. Zwei andere Umgebungsvariablen, die von Windows verwendet werden, sind **prompt** und **DIRCMD**.

- Wenn Sie Werte für `<variable>` und angeben `<string>` , wird der angegebene `<variable>` Wert der Umgebung hinzugefügt und `<string>` dieser Variablen zugeordnet. Wenn die Variable bereits in der Umgebung vorhanden ist, ersetzt der neue Zeichen folgen Wert den alten Zeichen folgen Wert.

- Wenn Sie nur eine Variable und ein Gleichheitszeichen (ohne `<string>` ) für den **set** -Befehl angeben, wird der Wert, der `<string>` der Variablen zugeordnet ist, gelöscht (als ob die Variable nicht vorhanden ist).

- Wenn Sie den **/a** -Parameter verwenden, werden die folgenden Operatoren in absteigender Rangfolge unterstützt:

  | Betreiber | Ausgeführte Operation |
  |--|--|
  | `( )` | Gruppierung |
  | `! ~ -` | Unär |
  | `* / %` | Arithmetik |
  | `+ -` | Arithmetik |
  | `<< >>` | Logische Verschiebung |
  | `&` | Bitweises AND |
  | `^` | Bitweises exklusives OR |
  | `= *= /= %= += -= &= ^=` | `= <<= >>=` |
  | `,` | Ausdrucks Trennzeichen |

- Wenn Sie logische `&&` `||` Operatoren (oder) oder Modulo ( **%** )-Operatoren verwenden, schließen Sie die Ausdrucks Zeichenfolge in Anführungszeichen ein. Alle nicht numerischen Zeichen folgen im Ausdruck werden als Umgebungsvariablen Namen betrachtet, und ihre Werte werden in Zahlen konvertiert, bevor Sie verarbeitet werden. Wenn Sie einen Umgebungsvariablen Namen angeben, der nicht in der aktuellen Umgebung definiert ist, wird der Wert NULL zugewiesen, sodass Sie arithmetische Werte mit Umgebungsvariablen Werten ausführen können, ohne das% zum Abrufen eines Werts zu verwenden.

- Wenn Sie **Set/a** über die Befehlszeile außerhalb eines Befehls Skripts ausführen, wird der endgültige Wert des Ausdrucks angezeigt.

- Numerische Werte sind Dezimalzahlen, es sei denn, Sie werden für hexadezimal Zahlen mit 0 × vorangestellt. Daher ist 0 × 12 identisch mit 18, was mit 022 identisch ist.

- Die Unterstützung für die verzögerte Erweiterung von Umgebungsvariablen ist standardmäßig deaktiviert. Sie können Sie jedoch mithilfe von **cmd/v**aktivieren oder deaktivieren.

- Beim Erstellen von Batch Dateien können Sie **Set** verwenden, um Variablen zu erstellen, und Sie dann auf die gleiche Weise wie die nummerierten Variablen **%0** bis **%9**verwenden. Sie können auch die Variablen **%0** bis **%9** als Eingabe für **set**verwenden.

- Wenn Sie einen variablen Wert aus einer Batchdatei aufzurufen, müssen Sie den Wert in Prozentzeichen ( **%** ) einschließen. Wenn Ihr Batch-Programm z. b. eine Umgebungsvariable mit dem Namen *Baud*erstellt, können Sie die Zeichenfolge, die der *Baudrate* zugeordnet ist, als ersetzbaren Parameter verwenden, indem Sie **% Baud%** an der Eingabeaufforderung eingeben

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Umgebungsvariable mit dem Namen *Test ^ 1*festzulegen:

```
set testVar=test^^1
```

Mit dem **Set** -Befehl werden alle Elemente, die dem Gleichheitszeichen (=) folgen, dem Wert der Variablen zugewiesen. Wenn Sie eingeben `set testVar=test^1` , erhalten Sie daher folgendes Ergebnis: `testVar=test^1` .

Geben Sie Folgendes ein, um eine Umgebungsvariable mit dem Namen *Test&1*festzulegen:

```
set testVar=test^&1
```

Um eine Umgebungsvariable mit dem Namen include festzulegen, damit die Zeichenfolge *c:\directory* zugeordnet ist, geben Sie *Folgendes* ein:

```
set include=c:\directory
```

Anschließend können Sie die Zeichenfolge *c:\directory* in Batch Dateien verwenden, indem Sie den Namen include mit Prozentzeichen ( **%** ) einschließen. Beispielsweise können Sie `dir %include%` in einer Batchdatei verwenden, um den Inhalt des Verzeichnisses anzuzeigen, das der INCLUDE-Umgebungsvariablen zugeordnet ist. Nachdem dieser Befehl verarbeitet wurde, ersetzt die Zeichenfolge c:\directory **% include%**.

Wenn Sie den Befehl **Set** in einem Batch-Programm verwenden möchten, um der *path* -Umgebungsvariablen ein neues Verzeichnis hinzuzufügen, geben Sie Folgendes ein:

```
@echo off
rem ADDPATH.BAT adds a new directory
rem to the path environment variable.
set path=%1;%path%
set
```

Zum Anzeigen einer Liste aller Umgebungsvariablen, die mit dem Buchstaben " *P*" beginnen, geben Sie Folgendes ein:

```
set p
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)