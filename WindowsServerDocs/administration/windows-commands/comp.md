---
title: comp
description: Windows-Befehls Thema für Comp, das den Inhalt von zwei Dateien oder Datei Sätzen Byte Weise vergleicht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40319d23-704d-4da1-be93-8259547275d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f61743b55f38cfdebb17506368609895f48b4f6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847453"
---
# <a name="comp"></a>comp

Vergleicht den Inhalt von zwei Dateien oder Dateigruppen byteweise. Wenn Sie ohne Parameter verwendet wird, werden Sie von **Comp** aufgefordert, die zu vergleichenden Dateien einzugeben.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
comp [<Data1>] [<Data2>] [/d] [/a] [/l] [/n=<Number>] [/c]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<data1 >|Gibt den Speicherort und den Namen der ersten Datei oder Gruppe von Dateien an, die Sie vergleichen möchten. Sie können Platzhalter Zeichen ( **&#42;** und **?** ) verwenden, um mehrere Dateien anzugeben.|
|\<data2 >|Gibt den Speicherort und den Namen der zweiten Datei oder Gruppe von Dateien an, die Sie vergleichen möchten. Sie können Platzhalter Zeichen ( **&#42;** und **?** ) verwenden, um mehrere Dateien anzugeben.|
|/d|Zeigt Unterschiede im Dezimal Format an. (Das Standardformat ist hexadezimal.)|
|/a|Zeigt Unterschiede als Zeichen an.|
|/l|Zeigt die Nummer der Zeile an, in der ein Unterschied auftritt, anstatt den Byte Offset anzuzeigen.|
|/n =\<Anzahl >|Vergleicht nur die Anzahl der Zeilen, die für jede Datei angegeben werden, auch wenn die Dateien unterschiedlich groß sind.|
|/c|Führt einen Vergleich aus, bei dem keine Groß-/Kleinschreibung beachtet wird|
|/Off [Zeile]|Verarbeitet Dateien mit dem Offline-Attribut Satz.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wie der **Comp** -Befehl nicht übereinstimmende Informationen identifiziert

    Während des Vergleichs zeigt **Comp** Meldungen an, die die Positionen der ungleichen Informationen zwischen den Dateien identifizieren. Jede Meldung gibt die Offset-Speicheradresse der ungleichen Bytes und den Inhalt der Bytes an (in Hexadezimal Schreibweise, es sei denn, der **/a** -oder **/d** -Befehlszeilenparameter wird angegeben). Nachrichten werden im folgenden Format angezeigt:

    `Compare error at OFFSET xxxxxxxx`

    `file1 = xx`

    `file2 = xx`

    Nach zehn ungleichen vergleichen hält **Comp** den Vergleich der Dateien an und zeigt die folgende Meldung an:

    `10 Mismatches - ending compare`
-   Behandeln spezieller Fälle für *data1* und *data2*  
    -   Wenn Sie die erforderlichen Komponenten von " *data1* " oder " *data2* " weglassen oder wenn Sie *data2*weglassen, werden Sie von **Comp** zur Eingabe der fehlenden Informationen aufgefordert.
    -   Wenn *data1* nur einen Laufwerk Buchstaben oder einen Verzeichnisnamen ohne Dateinamen enthält, vergleicht **Comp** alle Dateien im angegebenen Verzeichnis mit der in *data1*angegebenen Datei.
    -   Wenn *data2* nur einen Laufwerk Buchstaben oder einen Verzeichnisnamen enthält, ist der Standard Dateiname für *data2* derselbe wie in *data1*.
    -   Wenn **Comp** die angegebenen Dateien nicht finden kann, wird eine Meldung angezeigt, um zu bestimmen, ob Sie weitere Dateien vergleichen möchten.
-   Vergleichen von Dateien an unterschiedlichen Speicherorten

    **Comp** kann Dateien auf demselben Laufwerk, auf verschiedenen Laufwerken und im gleichen Verzeichnis oder in verschiedenen Verzeichnissen vergleichen. Wenn **Comp** die Dateien vergleicht, werden ihre Speicherorte und Dateinamen angezeigt.
-   Vergleichen von Dateien mit denselben Namen

    Die Dateien, die Sie vergleichen, können den gleichen Dateinamen haben, vorausgesetzt, Sie befinden sich in verschiedenen Verzeichnissen oder auf unterschiedlichen Laufwerken. Wenn Sie keinen Dateinamen für *data2*angeben, ist der Standard Dateiname für *data2* mit dem Dateinamen in *data1*identisch. Sie können Platzhalter Zeichen ( **&#42;** und **?** ) verwenden, um Dateinamen anzugeben.
-   Vergleichen von Dateien mit unterschiedlichen Größen

    Sie müssen **/n** angeben, um Dateien mit unterschiedlichen Größen zu vergleichen. Wenn die Dateigrößen unterschiedlich sind und **/n** nicht angegeben wird, zeigt **Comp** die folgende Meldung an:

    `Files are different sizes`

    `Compare more files (Y/N)?`

    Zum Vergleichen dieser Dateien drücken Sie N, um den Befehl **Comp** zu unterbrechen. Führen Sie dann den **Comp** -Befehl mit der Option **/n** erneut aus, um nur den ersten Teil der einzelnen Dateien zu vergleichen.
-   Sequenzielles Vergleichen von Dateien

    Wenn Sie Platzhalter Zeichen ( **&#42;** und **?** ) verwenden, um mehrere Dateien anzugeben, sucht **Comp** die erste Datei, die mit *data1* übereinstimmt, und vergleicht sie mit der entsprechenden Datei in *data2*, sofern vorhanden. Der **Comp** -Befehl meldet die Ergebnisse des Vergleichs für jede Datei, die mit *data1*übereinstimmt. Nach Abschluss zeigt **Comp** die folgende Meldung an:

    `Compare more files (Y/N)?`

    Drücken Sie Y, um weitere Dateien zu vergleichen. Mit dem Befehl **Comp** werden Sie aufgefordert, die Speicherorte und Namen der neuen Dateien einzugeben. Um die Vergleiche zu unterbrechen, drücken Sie N. Wenn Sie Y drücken, werden Sie von **Comp** aufgefordert, die Befehlszeilenoptionen zu verwenden. Wenn Sie keine Befehlszeilenoptionen angeben, verwendet **Comp** die Werte, die Sie zuvor angegeben haben.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um den Inhalt des Verzeichnisses c:\Reports mit dem Sicherungs Verzeichnis \\\\sales\backup\april zu vergleichen:
```
comp c:\reports \\sales\backup\april
```
Wenn Sie die ersten zehn Zeilen der Textdateien im Verzeichnis "\rechnungs" vergleichen und das Ergebnis im Dezimal Format anzeigen möchten, geben Sie Folgendes ein:
```
comp \invoice\*.txt \invoice\backup\*.txt /n=10 /d
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)