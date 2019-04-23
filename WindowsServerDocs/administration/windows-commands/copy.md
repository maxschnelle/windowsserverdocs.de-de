---
title: copy
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d593fbdbffd2a5ee4e4dfb4a817ad4708162160a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853771"
---
# <a name="copy"></a>copy



Kopiert eine oder mehrere Dateien von einem Speicherort.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
copy [/d] [/v] [/n] [/y | /-y] [/z] [/a | /b] <Source> [/a | /b] [+<Source> [/a | /b] [+ ...]] [<Destination> [/a | /b]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/d|Können die verschlüsselten Dateien, die zum Speichern als entschlüsselte Dateien am Ziel kopiert werden.|
|/v|Stellt sicher, dass neue Dateien richtig geschrieben sind.|
|/n|Verwendet einen kurzen Dateinamen ein, falls verfügbar, wenn eine Datei mit einem Namen, die länger als acht Zeichen oder eine Dateinamenerweiterung, die länger als drei Zeichen kopiert.|
|/y|Unterdrückt die Aufforderung zum bestätigen, dass eine vorhandene Zieldatei überschrieben werden soll.|
|/-y|Aufgefordert zu bestätigen, dass eine vorhandene Zieldatei überschrieben werden soll.|
|/z|Kopieren einer Datei neustartbaren Modus.|
|/a|Gibt eine ASCII-Textdatei an.|
|/b|Gibt eine binäre Datei an.|
|\<Quelle >|Erforderlich. Gibt den Speicherort, von dem Sie eine Datei oder einen Satz von Dateien kopieren möchten. *Quelle* kann einen Laufwerkbuchstaben und Doppelpunkt, ein Verzeichnisname, einen Dateinamen oder eine Kombination aus diesen bestehen.|
|\<Ziel >|Erforderlich. Gibt den Speicherort, den eine Datei oder einen Satz von Dateien kopiert werden soll. *Ziel* kann einen Laufwerkbuchstaben und Doppelpunkt, ein Verzeichnisname, einen Dateinamen oder eine Kombination aus diesen bestehen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Sie können eine ASCII-Textdatei kopieren, die ein EOF Zeichen (STRG + Z) verwendet, um das Ende der Datei anzugeben.
-   Mithilfe von   **/a**

    Wenn **/a** vor oder nach oder eine Liste von Dateien in der Befehlszeile angegeben, gilt für alle Dateien aufgeführt, die bis **Kopie** trifft **/b**. In diesem Fall **/b** gilt für die vorherige Datei **/b**.

    Die Auswirkungen der **/a** hängt von seiner Position in der Befehlszeilen-Zeichenfolge. Wenn **/a** folgt *Quelle*, **Kopie** behandelt die Datei als ASCII-Datei, und kopiert Daten, die das erste EOF Zeichen (STRG + Z) vorangestellt ist.

    Wenn **/a** folgt *Ziel*, **Kopie** Fügt ein EOF Zeichen (STRG + Z) als das letzte Zeichen der Datei.
-   Mithilfe von   **/b**

    **/ b** weist den Befehlsinterpreter, lesen die Anzahl der Bytes, die Dateigröße in das Verzeichnis angegeben. **/ b** ist der Standardwert für **Kopie**, es sei denn, **Kopie** Dateien kombiniert.

    Wenn **/b** vor oder nach oder eine Liste von Dateien in der Befehlszeile angegeben, gilt für alle aufgelisteten Dateien bis **Kopie** trifft **/a**. In diesem Fall **/a** gilt für die vorherige Datei **/a**.

    Die Auswirkungen der **/b** hängt von seiner Position in der Befehlszeile. Wenn **/b** folgt *Quelle*, **Kopie** kopiert die gesamte Datei, einschließlich jedes EOF Zeichen (STRG + Z).

    Wenn **/b** folgt *Ziel*, **Kopie** ein EOF Zeichen (STRG + Z) werden nicht hinzugefügt.
-   Mithilfe von   **/v**

    Wenn ein Schreibvorgang nicht kann, dass eine Fehlermeldung angezeigt überprüft werden. Obwohl nur selten auftreten, Aufzeichnen von Fehlern mit **Kopie**, können Sie **/v** um sicherzustellen, dass wichtige Daten ordnungsgemäß aufgezeichnet wurde. Die **/v** Befehlszeilenoption auch verlangsamt die **Kopie** Befehl, da jeder Sektor auf dem Datenträger aufgezeichnet geprüft werden muss.
-   Mithilfe von **/y** und   **/-y**

    Wenn **/y** ist voreingestellt in-y, können Sie diese Einstellung überschreiben, indem **/-y** an der Befehlszeile eingeben. Standardmäßig werden Sie aufgefordert, wenn Sie diese Einstellung, ersetzen, es sei denn, die **Kopie** Befehl in einem Batchskript ausgeführt wird.
-   Anfügen von Dateien

    Geben Sie Dateien an eine einzelne Datei für *Ziel*, aber mehrere Dateien für *Quelle* (verwenden Sie Platzhalterzeichen oder *"file1"* +  *Datei2*+*Datei3* Format).
-   Mithilfe von **Neustartmodus anzugeben**

    Wenn die Verbindung unterbrochen wird, während der Kopierphase "(z. B., wenn der Server offline geschaltet, um die Verbindung unterbrochen), **kopieren/z** fortgesetzt wird, nachdem die Verbindung wieder hergestellt ist. **/ z** auch zeigt den Prozentsatz des Vorgangs zum Kopieren, die für jede Datei abgeschlossen ist.
-   Kopieren in und aus-Geräte

    Sie können einen Gerätenamen für eine oder mehrere Vorkommen von ersetzen *Quelle* oder *Ziel*.
-   Verwenden oder weglassen **/b** beim Kopieren von auf einem Gerät

    Wenn *Ziel* ist ein Gerät (z. B. Com1 oder Lpt1) **/b** kopiert Daten in das Gerät im binären Modus. In diesem Modus **kopieren/b** kopiert alle Zeichen (einschließlich Sonderzeichen wie z. B. STRG + C, STRG + S, STRG + Z und EINGABETASTE) auf dem Gerät als Daten. Aber wenn Sie weglassen **/b**, Daten an das Gerät im ASCII-Modus kopiert. Im ASCII-Modus können Sonderzeichen dazu führen, dass Dateien während des Kopiervorgangs zu kombinieren.
-   Verwenden die Standard-Zieldatei

    Wenn Sie eine Datei nicht angeben, wird eine Kopie wird erstellt, mit dem gleichen Namen, Änderungsdatum und Zeit wie die ursprüngliche Datei geändert. Die neue Kopie wird im aktuellen Verzeichnis in das aktuelle Laufwerk gespeichert. Wenn die Quelldatei, auf das aktuelle Laufwerk und im aktuellen Verzeichnis ist, und Sie kein anderes Laufwerk oder das Verzeichnis für der Zieldatei, die **Kopie** Befehl beendet und die folgende Fehlermeldung angezeigt:

    `File cannot be copied onto itself`

    `0 File(s) copied`
-   Kombinieren von Dateien

    Bei Angabe von mehr als eine Datei im *Quelle*, **Kopie** kombiniert diese Elemente alle in einer einzelnen Datei mit dem Dateinamen im angegebenen *Ziel*. **Kopie** geht davon aus, die kombinierte Dateien sind ASCII-Dateien, es sei denn, Sie verwenden die **/b** Option.
-   Kopieren von Dateien der Länge 0 (null)

    **Kopie** kopiert keine Dateien, die 0 Byte lang sind. Verwendung **Xcopy** auf diese Dateien zu kopieren.
-   Ändern das Datum und einer Datei

    Wenn Sie weisen Sie die aktuelle Uhrzeit und Datum, an dem eine Datei ohne die Datei ändern möchten, verwenden Sie die folgende Syntax:  
    ```
    copy /b <Source> +,,
    ```  
    Die Kommas zeigen an, dass die von der *Ziel* Parameter.
-   Kopieren von Dateien in Unterverzeichnissen

    Verwenden Sie zum Kopieren aller Dateien und Unterverzeichnisse des Verzeichnisses der **Xcopy** Befehl.
-   Die **Kopie** -Befehl, mit verschiedenen Parametern finden Sie in der Wiederherstellungskonsole.

## <a name="BKMK_examples"></a>Beispiele für

Um eine Datei namens Memo.doc zu Brief.doc in das aktuelle Laufwerk kopieren, und stellen Sie sicher, dass ein EOF Zeichen (STRG + Z) am Ende der kopierten Datei ist, geben Sie Folgendes ein:
```
copy memo.doc letter.doc /a
```
Zum Kopieren einer Datei namens Amsel.Typ über das aktuelle Laufwerk und Verzeichnis, auf ein vorhandenes Verzeichnis mit dem Namen Vögel, das auf Laufwerk C: befindet, geben Sie Folgendes ein:
```
copy robin.typ c:\birds
```
Wenn das Unternehmens-Verzeichnis nicht vorhanden ist, von wird die Datei Amsel.Typ in eine Datei namens Vögel kopiert, die im Stammverzeichnis auf dem Datenträger im Laufwerk c: befindet

Kombinieren Sie Mar89.rpt Apr89.rpt und May89.rpt, die im aktuellen Verzeichnis befinden, und platzieren sie in einer Datei namens Berichts (ebenfalls in das aktuelle Verzeichnis), geben Sie Folgendes ein:
```
copy mar89.rpt + apr89.rpt + may89.rpt Report
```
Wenn Sie Dateien kombinieren **Kopie** kennzeichnet die Datei mit dem aktuellen Datum und Uhrzeit. Wenn Sie weglassen *Ziel*, die Dateien werden zusammengefasst und unter dem Namen der ersten Datei in der Liste gespeichert. Z. B. alle Dateien im Bericht kombinieren, wenn eine Datei mit dem Namen Berichts ist bereits vorhanden ist, geben Sie ein:
```
copy report + mar89.rpt + apr89.rpt + may89.rpt
```
Alle Dateien im aktuellen Verzeichnis zu integrieren, die the.txt in einer einzelnen Datei Dateinamenerweiterung mit dem Namen Combined.doc, Typ:
```
copy *.txt Combined.doc 
```
Wenn Sie verwenden möchten, kombinieren mehrere Binärdateien in einer Datei mithilfe von Platzhalterzeichen, einschließlich **/b**. Dadurch wird verhindert, dass Windows zum Behandeln von STRG + Z als EOF Zeichen. Beispiel:
```
copy /b *.exe Combined.exe
```

> [!CAUTION]
> Kombinieren von Binärdateien kann die resultierende Datei kann aufgrund eines internen Formatierung nicht genutzt werden.

Im folgenden Beispiel **Kopie** jede Datei mit der Erweiterung ".txt" mit der entsprechenden ref-Datei kombiniert. Das Ergebnis ist eine Datei mit demselben Namen, aber mit der Erweiterung .doc. **Kopie** File1.txt mit File1.ref kombiniert, um Datei1.doc, und klicken Sie dann **Kopie** kombiniert File2.txt mit File2.ref zu Datei2.doc und So weiter. Beispiel:
```
copy *.txt + *.ref *.doc
```
Kombinieren alle Dateien mit der Erweiterung TXT, und klicken Sie dann alle Dateien mit der Erweiterung REF in einer Datei, die mit dem Namen Combined.doc zusammenzufassen, geben Sie Folgendes ein:
```
copy *.txt + *.ref Combined.doc
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)