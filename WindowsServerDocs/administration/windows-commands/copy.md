---
title: copy
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9624d4a1-349a-4693-ad00-1d1d4e59e9ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 102fd6b59516b04b8986ee47b52f521be73f04de
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379041"
---
# <a name="copy"></a>copy



Kopiert eine oder mehrere Dateien von einem Speicherort in einen anderen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
copy [/d] [/v] [/n] [/y | /-y] [/z] [/a | /b] <Source> [/a | /b] [+<Source> [/a | /b] [+ ...]] [<Destination> [/a | /b]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/d|Ermöglicht, dass verschlüsselte Dateien, die kopiert werden, als entschlüsselte Dateien am Ziel gespeichert werden.|
|/v|Überprüft, ob neue Dateien ordnungsgemäß geschrieben werden.|
|/n|Verwendet einen kurzen Dateinamen, falls verfügbar, beim Kopieren einer Datei mit einem Namen, der länger als acht Zeichen ist, oder mit einer Dateinamenerweiterung, die länger als drei Zeichen ist.|
|/y|Unterdrückt die Eingabeaufforderung, um zu bestätigen, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|/-y|Sie werden aufgefordert, zu bestätigen, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|"/z|Kopiert vernetzte Dateien im neu startbaren Modus.|
|/a|Gibt eine ASCII-Textdatei an.|
|/b|Gibt eine Binärdatei an.|
|> der @no__t 0quelle|Erforderlich. Gibt den Speicherort an, von dem Sie eine Datei oder einen Satz von Dateien kopieren möchten. Die *Quelle* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen.|
|\<Ziel >|Erforderlich. Gibt den Speicherort an, an den Sie eine Datei oder einen Satz von Dateien kopieren möchten. Das *Ziel* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Sie können eine ASCII-Textdatei mit einem Dateiendezeichen (STRG + Z) kopieren, um das Ende der Datei anzugeben.
-   Verwenden von **/a**

    Wenn **/a** einer Liste von Dateien in der Befehlszeile vorausgeht oder diese befolgt, gilt sie für alle Dateien, die bis zum **Kopieren** von **/b**aufgeführt sind. In diesem Fall gilt **/b** für die Datei vor **/b**.

    Die Auswirkung von **/a** hängt von seiner Position in der Befehlszeilen Zeichenfolge ab. Wenn **/a** auf *Quelle*folgt, behandelt **Copy** die Datei als ASCII-Datei und kopiert Daten, die dem ersten Dateiendezeichen (STRG + Z) vorausgegangen sind.

    Wenn **/a** auf *Destination*folgt, fügt **Copy** ein Dateiendezeichen (STRG + Z) als letztes Zeichen der Datei hinzu.
-   Verwenden von **/b**

    **/b** weist den Befehls Interpreter an, die Anzahl der Bytes zu lesen, die durch die Dateigröße im Verzeichnis angegeben werden. **/b** ist der Standardwert für **Copy**, es sei denn, der **Kopier** Vorgang kombiniert Dateien.

    Wenn **/b** einer Liste von Dateien in der Befehlszeile vorausgeht oder diese befolgt, gilt sie für alle aufgelisteten Dateien, bis die **Kopie** auf **/a**trifft. In diesem Fall gilt **/a** für die Datei vor **/a**.

    Die Auswirkung von **/b** hängt von seiner Position in der –-Zeilen Zeichenfolge des Befehls ab. Wenn **/b** auf *Quelle*folgt, kopiert **Copy** die gesamte Datei, einschließlich eines beliebigen dateiendezeichens (STRG + Z).

    Wenn **/b** auf das *Ziel*folgt, fügt **Copy** kein Dateiendezeichen (STRG + Z) hinzu.
-   Verwenden von **/v**

    Wenn ein Schreibvorgang nicht überprüft werden kann, wird eine Fehlermeldung angezeigt. Obwohl das Aufzeichnen von Fehlern selten mit **Copy**auftritt, können Sie **/v** verwenden, um zu überprüfen, ob wichtige Daten ordnungsgemäß aufgezeichnet wurden. Die Befehlszeilenoption **/v** verlangsamt auch den **Kopier** Befehl, da jeder auf dem Datenträger aufgezeichnete Sektor geprüft werden muss.
-   Verwenden von **/y** und **/-y**

    Wenn **/y** in der COPYCMD-Umgebungsvariablen voreingestellt ist, können Sie diese Einstellung mithilfe von **/-y** in der Befehlszeile überschreiben. Standardmäßig werden Sie aufgefordert, wenn Sie diese Einstellung ersetzen, es sei denn, der **Copy** -Befehl wird in einem Batch Skript ausgeführt.
-   Anhängen von Dateien

    Um Dateien anzufügen, geben Sie eine einzelne Datei für das *Ziel*an, aber mehrere Dateien für die *Quelle* (verwenden Sie Platzhalter Zeichen oder *file1*+*file2*+*datei3* Format).
-   Verwenden von **"/z**

    Wenn die Verbindung während der Kopier Phase unterbrochen wird (z. b. wenn der Server, der offline geschaltet wird, die Verbindung unterbrochen), wird **Copy "/z** fortgesetzt, nachdem die Verbindung wieder hergestellt wurde. **"/z** zeigt auch den Prozentsatz des Kopiervorgangs an, der für jede Datei abgeschlossen ist.
-   Kopieren von und von Geräten

    Sie können einen Gerätenamen für ein oder mehrere Vorkommen von *Quelle* oder *Ziel*ersetzen.
-   Verwenden oder weglassen von **/b** beim Kopieren auf ein Gerät

    Wenn das *Ziel* ein Gerät ist (z. b. COM1 oder LPT1), kopiert **/b** Daten im Binärmodus auf das Gerät. Im Binärmodus kopiert **copy/b** alle Zeichen (einschließlich Sonderzeichen wie STRG + C, STRG + S, STRG + Z und EINGABETASTE) als Daten auf das Gerät. Wenn Sie jedoch **/b**weglassen, werden die Daten im ASCII-Modus auf das Gerät kopiert. Im ASCII-Modus können Sonderzeichen während des Kopiervorgangs zum Kombinieren von Dateien führen.
-   Verwenden der Standardzieldatei

    Wenn Sie keine Zieldatei angeben, wird eine Kopie mit dem gleichen Namen, Änderungsdatum und der geänderten Zeit wie die ursprüngliche Datei erstellt. Die neue Kopie wird im aktuellen Verzeichnis auf dem aktuellen Laufwerk gespeichert. Wenn sich die Quelldatei auf dem aktuellen Laufwerk und im aktuellen Verzeichnis befindet und Sie kein anderes Laufwerk oder Verzeichnis für die Zieldatei angeben, wird der **Kopier** Befehl angehalten, und die folgende Fehlermeldung wird angezeigt:

    `File cannot be copied onto itself`

    `0 File(s) copied`
-   Kombinieren von Dateien

    Wenn Sie mehr als eine Datei in der *Quelle*angeben, werden Sie durch **Kopieren** in einer einzelnen Datei unter Verwendung des unter *Ziel*angegebenen Datei namens kombiniert. **Copy** geht davon aus, dass die kombinierten Dateien ASCII-Dateien sind, sofern Sie nicht die Option **/b** verwenden.
-   Kopieren von Dateien der Länge 0

    Beim **Kopieren** werden keine Dateien mit einer Länge von 0 Bytes kopiert. Verwenden Sie **xcopy** , um diese Dateien zu kopieren.
-   Ändern der Uhrzeit und des Datums einer Datei

    Wenn Sie die aktuelle Uhrzeit und das aktuelle Datum einer Datei zuweisen möchten, ohne die Datei zu ändern, verwenden Sie die folgende Syntax:  
    ```
    copy /b <Source> +,,
    ```  
    Die Kommas geben an, dass der *Ziel* Parameter ausgelassen werden soll.
-   Kopieren von Dateien in Unterverzeichnissen

    Um alle Dateien und Unterverzeichnisse eines Verzeichnisses zu kopieren, verwenden Sie den **xcopy** -Befehl.
-   Der **Kopier** Befehl mit unterschiedlichen Parametern ist über die Wiederherstellungskonsole verfügbar.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Datei namens Memo. doc in Letter. doc auf dem aktuellen Laufwerk zu kopieren und sicherzustellen, dass sich das Dateiendezeichen (STRG + Z) am Ende der kopierten Datei befindet:
```
copy memo.doc letter.doc /a
```
Geben Sie Folgendes ein, um eine Datei mit dem Namen "Robin. Type" aus dem aktuellen Laufwerk und Verzeichnis in ein vorhandenes Verzeichnis mit dem Namen "Birds" auf Laufwerk C zu kopieren:
```
copy robin.typ c:\birds
```
Wenn das vogelverzeichnis nicht vorhanden ist, wird die Datei "Robin. d" in eine Datei mit dem Namen "Vögel" kopiert, die sich im Stammverzeichnis auf dem Datenträger des Laufwerks C befindet.

Um Mar89. rpt, Apr89. rpt und May89. rpt zu kombinieren, die sich im aktuellen Verzeichnis befinden, und platzieren Sie Sie in einer Datei namens Report (auch im aktuellen Verzeichnis), geben Sie Folgendes ein:
```
copy mar89.rpt + apr89.rpt + may89.rpt Report
```
Beim Kombinieren von Dateien wird die Zieldatei mit dem aktuellen Datum und der aktuellen Uhrzeit **kopiert** . Wenn Sie das *Ziel*weglassen, werden die Dateien kombiniert und unter dem Namen der ersten Datei in der Liste gespeichert. Wenn Sie z. b. alle Dateien im Bericht kombinieren möchten, wenn eine Datei mit dem Namen Report bereits vorhanden ist, geben Sie
```
copy report + mar89.rpt + apr89.rpt + may89.rpt
```
Geben Sie Folgendes ein, um alle Dateien im aktuellen Verzeichnis mit der Dateinamenerweiterung ". txt" in einer einzelnen Datei mit dem Namen "kombinierte. doc" zu kombinieren:
```
copy *.txt Combined.doc 
```
Wenn Sie mehrere Binärdateien mithilfe von Platzhalter Zeichen zu einer Datei zusammenfassen möchten, schließen Sie **/b**ein. Dadurch wird verhindert, dass Windows Strg + Z als Dateiendezeichen behandelt. Beispiel:
```
copy /b *.exe Combined.exe
```

> [!CAUTION]
> Wenn Sie Binärdateien kombinieren, kann die resultierende Datei aufgrund interner Formatierung nicht verwendet werden.

Im folgenden Beispiel kombiniert **Copy** jede Datei mit der Erweiterung TXT mit der entsprechenden Verweis Datei. Das Ergebnis ist eine Datei mit dem gleichen Dateinamen, aber mit der Erweiterung ". doc". **Copy** kombiniert "file1. txt" mit "file1. ref" in Form von "file1. doc" und **kopiert** dann "file2. txt" mit "file2. ref" in Form von "file2. doc" usw. Beispiel:
```
copy *.txt + *.ref *.doc
```
Wenn Sie alle Dateien mit der Erweiterung. txt kombinieren und dann alle Dateien mit der Erweiterung. ref in einer Datei mit dem Namen "kombinierte. doc" kombinieren möchten, geben Sie Folgendes ein:
```
copy *.txt + *.ref Combined.doc
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)