---
title: copy
description: Referenz Thema für den Kopier Befehl, bei dem eine oder mehrere Dateien von einem Speicherort in einen anderen kopiert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9624d4a1-349a-4693-ad00-1d1d4e59e9ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 909bcdf83c87440dafe2653711c4d7e215f8d66b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719297"
---
# <a name="copy"></a>copy

Kopiert eine oder mehrere Dateien von einem Speicherort in einen anderen.

> [!NOTE]
> Sie können den **Kopier** Befehl auch mit anderen Parametern in der Wiederherstellungskonsole verwenden. Weitere Informationen zur Wiederherstellungskonsole finden Sie in der [Windows-Wiederherstellungs Umgebung (Windows Recovery Environment, Windows RE)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

## <a name="syntax"></a>Syntax

```
copy [/d] [/v] [/n] [/y | /-y] [/z] [/a | /b] <source> [/a | /b] [+<source> [/a | /b] [+ ...]] [<destination> [/a | /b]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /d | Ermöglicht, dass verschlüsselte Dateien, die kopiert werden, als entschlüsselte Dateien am Ziel gespeichert werden. |
| /v | Überprüft, ob neue Dateien ordnungsgemäß geschrieben werden. |
| /n | Verwendet einen kurzen Dateinamen, falls verfügbar, beim Kopieren einer Datei mit einem Namen, der länger als acht Zeichen ist, oder mit einer Dateinamenerweiterung, die länger als drei Zeichen ist. |
| /y | Unterdrückt die Eingabeaufforderung, um zu bestätigen, dass Sie eine vorhandene Zieldatei überschreiben möchten. |
| /-y | Sie werden aufgefordert, zu bestätigen, dass Sie eine vorhandene Zieldatei überschreiben möchten. |
| /z | Kopiert vernetzte Dateien im neu startbaren Modus. |
| /a | Gibt eine ASCII-Textdatei an. |
| /b | Gibt eine Binärdatei an. |
| `<source>` | Erforderlich. Gibt den Speicherort an, von dem Sie eine Datei oder einen Satz von Dateien kopieren möchten. Die *Quelle* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen. |
| `<destination>` | Erforderlich. Gibt den Speicherort an, an den Sie eine Datei oder einen Satz von Dateien kopieren möchten. Das *Ziel* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Sie können eine ASCII-Textdatei mit einem Dateiendezeichen (STRG + Z) kopieren, um das Ende der Datei anzugeben.

- Wenn **/a** einer Liste von Dateien in der Befehlszeile vorangestellt oder befolgt wird, gilt sie für alle Dateien, die aufgelistet sind, bis die **Kopie** auf **/b**trifft. In diesem Fall gilt **/b** für die Datei vor **/b**.

    Die Auswirkung von **/a** hängt von seiner Position in der Befehlszeilen Zeichenfolge ab:
      - Wenn **/a** auf *Quelle*folgt, behandelt der **Kopier** Befehl die Datei als ASCII-Datei und kopiert Daten, die dem ersten Dateiendezeichen (STRG + Z) vorausgegangen sind.
      - Wenn **/a** auf *Destination*folgt, fügt der **Copy** -Befehl ein Dateiendezeichen (STRG + Z) als letztes Zeichen der Datei hinzu.

- , Wenn **/b** den Befehls Interpreter anweist, die Anzahl der Bytes zu lesen, die durch die Dateigröße im Verzeichnis angegeben werden. **/b** ist der Standardwert für **Copy**, es sei denn, der **Kopier** Vorgang kombiniert Dateien.

- Wenn **/b** einer Liste von Dateien in der Befehlszeile vorausgeht oder diese befolgt, gilt sie für alle aufgelisteten Dateien, bis die **Kopie** auf **/a**trifft. In diesem Fall gilt **/a** für die Datei vor **/a**.

    Die Wirkung von **/b** hängt von der Position im Befehl – der Zeilen Zeichenfolge ab:-Wenn **/b** auf die *Quelle*folgt, kopiert der **Kopier** Befehl die gesamte Datei, einschließlich jedes dateiendezeichens (STRG + Z).
        -Wenn **/b** dem *Ziel*folgt, fügt der **Kopier** Befehl kein Dateiendezeichen (STRG + Z) hinzu.

- Wenn ein Schreibvorgang nicht überprüft werden kann, wird eine Fehlermeldung angezeigt. Obwohl das Aufzeichnen von Fehlern selten mit dem **Kopier** Befehl auftritt, können Sie **/v** verwenden, um zu überprüfen, ob wichtige Daten ordnungsgemäß aufgezeichnet wurden. Die Befehlszeilenoption **/v** verlangsamt auch den **Kopier** Befehl, da jeder auf dem Datenträger aufgezeichnete Sektor geprüft werden muss.

- Wenn **/y** in der **COPYCMD** -Umgebungsvariablen voreingestellt ist, können Sie diese Einstellung mithilfe von **/-y** in der Befehlszeile überschreiben. Standardmäßig werden Sie aufgefordert, wenn Sie diese Einstellung ersetzen, es sei denn, der **Copy** -Befehl wird in einem Batch Skript ausgeführt.
  
- Um Dateien anzufügen, geben Sie eine einzelne Datei für das *Ziel*an, aber mehrere Dateien für die *Quelle* (verwenden Sie Platzhalter Zeichen oder das *file1*+*file2*+*datei3* -Format).

- Wenn die Verbindung während der Kopier Phase unterbrochen wird (z. b. wenn der Server, der offline geschaltet wird, die Verbindung unterbrochen), können Sie **Copy "/z** verwenden, um den Vorgang fortzusetzen, nachdem die Verbindung wieder hergestellt wurde. Die Option **"/z** zeigt auch den Prozentsatz des Kopiervorgangs an, der für jede Datei abgeschlossen ist.

- Sie können einen Gerätenamen für ein oder mehrere Vorkommen von *Quelle* oder *Ziel*ersetzen.

- Wenn das *Ziel* ein Gerät ist (z. b. COM1 oder LPT1), kopiert die Option **/b** Daten im Binärmodus auf das Gerät. Im Binärmodus kopiert **copy/b** alle Zeichen (einschließlich Sonderzeichen wie STRG + C, STRG + S, STRG + Z und EINGABETASTE) als Daten auf das Gerät. Wenn Sie jedoch **/b**weglassen, werden die Daten im ASCII-Modus auf das Gerät kopiert. Im ASCII-Modus können Sonderzeichen während des Kopiervorgangs zum Kombinieren von Dateien führen.

- Wenn Sie keine Zieldatei angeben, wird eine Kopie mit dem gleichen Namen, Änderungsdatum und der geänderten Zeit wie die ursprüngliche Datei erstellt. Die neue Kopie wird im aktuellen Verzeichnis auf dem aktuellen Laufwerk gespeichert. Wenn sich die Quelldatei auf dem aktuellen Laufwerk und im aktuellen Verzeichnis befindet und Sie kein anderes Laufwerk oder Verzeichnis für die Zieldatei angeben, wird der **Kopier** Befehl angehalten, und die folgende Fehlermeldung wird angezeigt:

    ```
    File cannot be copied onto itself
    0 File(s) copied
    ```

- Wenn Sie mehr als eine Datei in der *Quelle*angeben, werden Sie mit dem **Kopier** Befehl in einer einzigen Datei zusammengefasst, wobei der in *Ziel*angegebene Dateiname verwendet wird. Der **Kopier** Befehl setzt voraus, dass die kombinierten Dateien ASCII-Dateien sind, es sei denn, Sie verwenden die Option **/b**

- Um Dateien mit einer Länge von 0 Bytes zu kopieren oder alle Dateien und Unterverzeichnisse eines Verzeichnisses zu kopieren, verwenden Sie den [xcopy-Befehl](xcopy.md).

- Verwenden Sie die folgende Syntax, um die aktuelle Uhrzeit und das aktuelle Datum einer Datei zuzuweisen, ohne die Datei zu ändern:  

    ```
    copy /b <source> +,,
    ```

    Gibt an, dass die Kommas angeben, dass der *Ziel* Parameter absichtlich ausgelassen wurde.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Datei namens *Memo. doc* in *Letter. doc* auf dem aktuellen Laufwerk zu kopieren und sicherzustellen, dass sich das Dateiendezeichen (STRG + Z) am Ende der kopierten Datei befindet:

```
copy memo.doc letter.doc /a
```

Geben Sie Folgendes ein, um eine Datei mit dem Namen " *Robin.* Type" aus dem aktuellen Laufwerk und Verzeichnis in ein vorhandenes Verzeichnis mit dem Namen " *Birds* " auf Laufwerk C zu kopieren:

```
copy robin.typ c:\birds
```

> [!NOTE]
> Wenn das *vogelverzeichnis* nicht vorhanden ist, wird die Datei " *Robin.* d" in eine Datei mit dem Namen " *Vögel* " kopiert, die sich im Stammverzeichnis auf dem Datenträger in Laufwerk C befindet.

Um *Mar89. rpt*, *Apr89. rpt*und *May89. rpt*zu kombinieren, die sich im aktuellen Verzeichnis befinden, und platzieren Sie Sie in einer Datei namens *Report* (auch im aktuellen Verzeichnis), geben Sie Folgendes ein:

```
copy mar89.rpt + apr89.rpt + may89.rpt Report
```

> [!NOTE]
> Wenn Sie Dateien kombinieren, markiert der **Kopier** Befehl die Zieldatei mit dem aktuellen Datum und der aktuellen Uhrzeit. Wenn Sie das *Ziel*weglassen, werden die Dateien kombiniert und unter dem Namen der ersten Datei in der Liste gespeichert.

Wenn Sie alle Dateien im *Bericht*kombinieren möchten, wenn bereits eine Datei namens *Report* vorhanden ist, geben Sie Folgendes ein:

```
copy report + mar89.rpt + apr89.rpt + may89.rpt
```

Geben Sie Folgendes ein, um alle Dateien im aktuellen Verzeichnis mit der Dateinamenerweiterung ". txt" in einer einzelnen Datei mit dem Namen " *kombinierte. doc*" zu kombinieren:

```
copy *.txt Combined.doc
```

Wenn Sie mehrere Binärdateien mithilfe von Platzhalter Zeichen in einer Datei kombinieren möchten, schließen Sie **/b**ein. Dadurch wird verhindert, dass Windows Strg + Z als Dateiendezeichen behandelt. Beispiel:

```
copy /b *.exe Combined.exe
```

> [!CAUTION]
> Wenn Sie Binärdateien kombinieren, kann die resultierende Datei aufgrund interner Formatierung nicht verwendet werden.

- Wenn Sie jede Datei mit der Erweiterung. txt und der entsprechenden Ref-Datei kombinieren, wird eine Datei mit dem gleichen Dateinamen erstellt, aber mit der Erweiterung. doc. Der **Copy** -Befehl kombiniert *File1. txt* mit *File1. Ref* , um *File1. doc*zu bilden, und der Befehl kombiniert *File2. txt* mit *File2. Ref* , um *File2. doc*zu bilden usw. Beispiel:

```
copy *.txt + *.ref *.doc
```

Wenn Sie alle Dateien mit der Erweiterung. txt kombinieren und dann alle Dateien mit der Erweiterung. ref in einer Datei mit dem Namen " *kombinierte. doc*" kombinieren möchten, geben Sie Folgendes ein:

```
copy *.txt + *.ref Combined.doc
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [xcopy-Befehl](xcopy.md)
