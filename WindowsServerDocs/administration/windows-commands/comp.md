---
title: comp
description: Referenz Artikel für den Comp-Befehl, der den Inhalt von zwei Dateien oder Datei Sätzen Byte für Byte vergleicht.
ms.topic: article
ms.assetid: 40319d23-704d-4da1-be93-8259547275d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18bd39483957959c746913a4ee18014be40c9eaa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880038"
---
# <a name="comp"></a>comp

Vergleicht den Inhalt von zwei Dateien oder Dateigruppen byteweise. Diese Dateien können auf demselben Laufwerk oder auf unterschiedlichen Laufwerken, im gleichen Verzeichnis oder in verschiedenen Verzeichnissen gespeichert werden. Wenn mit diesem Befehl Dateien verglichen werden, werden Ihre Speicherort-und Dateinamen angezeigt. Wenn Sie ohne Parameter verwendet wird, werden Sie von **Comp** aufgefordert, die zu vergleichenden Dateien einzugeben.

## <a name="syntax"></a>Syntax

```
comp [<data1>] [<data2>] [/d] [/a] [/l] [/n=<number>] [/c]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<data1>` | Gibt den Speicherort und den Namen der ersten Datei oder Gruppe von Dateien an, die Sie vergleichen möchten. Sie können Platzhalter Zeichen (**&#42;** und **?**) verwenden, um mehrere Dateien anzugeben. |
| `<data2>` | Gibt den Speicherort und den Namen der zweiten Datei oder Gruppe von Dateien an, die Sie vergleichen möchten. Sie können Platzhalter Zeichen (**&#42;** und **?**) verwenden, um mehrere Dateien anzugeben. |
| /d | Zeigt Unterschiede im Dezimal Format an. (Das Standardformat ist hexadezimal.) |
| /a | Zeigt Unterschiede als Zeichen an. |
| /l | Zeigt die Nummer der Zeile an, in der ein Unterschied auftritt, anstatt den Byte Offset anzuzeigen. |
| /n =`<number>` | Vergleicht nur die Anzahl der Zeilen, die für jede Datei angegeben werden, auch wenn die Dateien unterschiedlich groß sind. |
| /C | Führt einen Vergleich aus, bei dem keine Groß-/Kleinschreibung beachtet wird |
| /Off [Zeile] | Verarbeitet Dateien mit dem Offline-Attribut Satz. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Bemerkungen

- Während des Vergleichs zeigt **Comp** Meldungen an, die die Positionen der ungleichen Informationen zwischen den Dateien identifizieren. Jede Meldung gibt die Offset-Speicheradresse der ungleichen Bytes und den Inhalt der Bytes an (in Hexadezimal Schreibweise, es sei denn, der **/a** -oder **/d** -Befehlszeilenparameter wird angegeben). Nachrichten werden im folgenden Format angezeigt:

    ```
    Compare error at OFFSET xxxxxxxx
    file1 = xx
    file2 = xx
    ```

    Nach zehn ungleichen vergleichen hält **Comp** den Vergleich der Dateien an und zeigt die folgende Meldung an:

    `10 Mismatches - ending compare`

- Wenn Sie erforderliche Komponenten von " *data1* " oder " *data2*" weglassen oder " *data2* " vollständig weglassen, werden Sie mit diesem Befehl aufgefordert, die fehlenden Informationen einzugeben.

- Wenn *data1* nur einen Laufwerk Buchstaben oder einen Verzeichnisnamen ohne Dateinamen enthält, vergleicht dieser Befehl alle Dateien im angegebenen Verzeichnis mit der in *data1*angegebenen Datei.

- Wenn *data2* nur einen Laufwerk Buchstaben oder einen Verzeichnisnamen enthält, wird der Standard Dateiname für *data2* zum gleichen Namen wie für *data1*.

- Wenn der **Comp** -Befehl die angegebenen Dateien nicht finden kann, werden Sie aufgefordert, eine Meldung darüber zu erhalten, ob Sie zusätzliche Dateien vergleichen möchten.

- Die Dateien, die Sie vergleichen, können den gleichen Dateinamen haben, vorausgesetzt, Sie befinden sich in verschiedenen Verzeichnissen oder auf unterschiedlichen Laufwerken. Sie können Platzhalter Zeichen (**&#42;** und **?**) verwenden, um Dateinamen anzugeben.

- Sie müssen **/n** angeben, um Dateien mit unterschiedlichen Größen zu vergleichen. Wenn die Dateigrößen unterschiedlich sind und **/n** nicht angegeben wird, wird die folgende Meldung angezeigt:

    ```
    Files are different sizes
    Compare more files (Y/N)?
    ```

    Wenn Sie diese Dateien trotzdem vergleichen möchten, drücken Sie **N** , um den Befehl zu unterbrechen. Führen Sie dann den Befehl **Comp** erneut aus, und verwenden Sie die Option **/n** , um nur den ersten Teil der einzelnen Dateien zu vergleichen.

- Wenn Sie Platzhalter Zeichen (**&#42;** und **?**) verwenden, um mehrere Dateien anzugeben, sucht **Comp** die erste Datei, die mit *data1* übereinstimmt, und vergleicht sie mit der entsprechenden Datei in *data2*, sofern vorhanden. Der **Comp** -Befehl meldet die Ergebnisse des Vergleichs für jede Datei, die mit *data1*übereinstimmt. Nach Abschluss zeigt **Comp** die folgende Meldung an:

    `Compare more files (Y/N)?`

    Drücken Sie **Y**, um weitere Dateien zu vergleichen. Mit dem Befehl **Comp** werden Sie aufgefordert, die Speicherorte und Namen der neuen Dateien einzugeben. Um die Vergleiche zu unterbrechen, drücken Sie **N**. Wenn Sie **Y**drücken, werden Sie aufgefordert, die zu verwendenden Befehlszeilenoptionen zu verwenden. Wenn Sie keine Befehlszeilenoptionen angeben, verwendet **Comp** die Werte, die Sie zuvor angegeben haben.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Inhalt des Verzeichnisses *c:\Reports* mit dem Sicherungs Verzeichnis zu vergleichen `\\sales\backup\april` :

```
comp c:\reports \\sales\backup\april
```

Wenn Sie die ersten zehn Zeilen der Textdateien im Verzeichnis " *\rechnungs* " vergleichen und das Ergebnis im Dezimal Format anzeigen möchten, geben Sie Folgendes ein:

```
comp \invoice\*.txt \invoice\backup\*.txt /n=10 /d
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)