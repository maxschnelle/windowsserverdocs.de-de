---
title: comp
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40319d23-704d-4da1-be93-8259547275d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d10b86176d97e1afd76085516fbfc00bdc36577f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854681"
---
# <a name="comp"></a>comp



Vergleicht den Inhalt von zwei Dateien oder Sätze von Dateien Byte-pro-Byte. Wenn Sie ohne Angabe von Parametern **Comp** fordert Sie zur Eingabe der zu vergleichenden Dateien.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
comp [<Data1>] [<Data2>] [/d] [/a] [/l] [/n=<Number>] [/c]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Data1 >|Gibt den Speicherort und Namen der ersten Datei oder die Gruppe von Dateien, die Sie vergleichen möchten. Sie können Platzhalterzeichen verwenden (**&#42;** und **?**) auf mehrere Dateien anzugeben.|
|\<Data2 >|Gibt den Speicherort und Namen der zweiten Datei oder die Gruppe von Dateien, die Sie vergleichen möchten. Sie können Platzhalterzeichen verwenden (**&#42;** und **?**) auf mehrere Dateien anzugeben.|
|/d|Zeigt die Unterschiede im Dezimalformat. (Das Standardformat ist hexadezimal).|
|/a|Zeigt die Unterschiede als-Zeichen.|
|/l|Zeigt die Nummer der Zeile, in dem ein Unterschied wird anstelle des Byteoffsets, an.|
|/ n =\<Anzahl >|Vergleicht nur die Anzahl der Zeilen, die für jede Datei angegeben werden, auch wenn die Dateien unterschiedlichen Größen sind.|
|/c|Führt einen Vergleich, der keine Groß-/Kleinschreibung beachtet wird.|
|/off[line]|Verarbeitet die Dateien mit dem offline-Attribut.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wie die **Comp** Befehl identifiziert nicht übereinstimmende Informationen

    Während des Vergleichs **Comp** zeigt an, die die Speicherorte der ungleichen-Informationen zwischen den Dateien zu identifizieren. Jeder Nachricht gibt an, die Offsets Speicheradresse der ungleichen Bytes und den Inhalt der Bytes (in der Hexadezimalnotation, wenn die **/a** oder **/d** Befehlszeilenparameter angegeben ist). Meldungen werden im folgenden Format angezeigt:

    `Compare error at OFFSET xxxxxxxx`

    `file1 = xx`

    `file2 = xx`

    Nach zehn ungleich-Vergleiche **Comp** beendet wird, vergleichen die Dateien und die folgende Meldung angezeigt:

    `10 Mismatches - ending compare`
-   Behandeln besonderer Fälle für *Data1* und *Data2*  
    -   Wenn Sie die erforderlichen Komponenten entweder weglassen *Data1* oder *Data2* oder wenn Sie weglassen *Data2*, **Comp** aufgefordert, die fehlenden Informationen.
    -   Wenn *Data1* enthält nur einen Laufwerkbuchstaben oder einen Verzeichnisnamen mit keine Dateinamen, **Comp** vergleicht alle Dateien im angegebenen Verzeichnis in die Datei im angegebenen *Data1*.
    -   Wenn *Data2* enthält nur einen Laufwerkbuchstaben oder einen Verzeichnisnamen an, der Standarddateiname für *Data2* ist identisch mit dem in *Data1*.
    -   Wenn **Comp** kann nicht gefunden werden die Dateien, die Sie angeben, sie werden Sie aufgefordert, mit der Meldung zu bestimmen, ob weitere Dateien verglichen werden soll.
-   Vergleichen von Dateien an unterschiedlichen Standorten

    **Comp** können Dateien auf dem gleichen Laufwerk oder auf verschiedenen Laufwerken und im gleichen Verzeichnis oder in verschiedenen Verzeichnissen vergleichen. Wenn **Comp** vergleicht die Dateien, deren Speicherort und die Namen angezeigt.
-   Vergleichen von Dateien mit den gleichen Namen

    Die Dateien, die Sie vergleichen, haben den gleichen Dateinamen, vorausgesetzt, dass sie in anderen Verzeichnissen oder auf verschiedenen Laufwerken sind. Wenn Sie einen Namen für nicht angeben *Data2*, der Standarddateiname für *Data2* ist identisch mit den Namen der im *Data1*. Sie können Platzhalterzeichen verwenden (**&#42;** und **?**) Dateinamen angeben.
-   Vergleichen von Dateien mit verschiedenen Größen

    Sie müssen angeben, **/n** zum Vergleichen von Dateien mit verschiedenen Größen. Wenn die Dateigrößen unterscheiden und **/n** nicht angegeben ist, **Comp** wird die folgende Meldung angezeigt:

    `Files are different sizes`

    `Compare more files (Y/N)?`

    So vergleichen Sie diese Dateien, z zum Beenden der **Comp** Befehl. Führen Sie dann erneut aus der **Comp** -Befehl mit der **/n** Option aus, um nur der erste Teil jeder Datei verglichen werden soll.
-   Vergleichen von Dateien sequenziell

    Bei Verwendung von Platzhalterzeichen (**&#42;** und **?**) an mehrere Dateien **Comp** sucht die erste Datei, die entspricht *Data1* und vergleicht ihn mit der entsprechenden Datei im *Data2*, sofern vorhanden. Die **Comp** Befehl meldet die Ergebnisse des Vergleichs für den Abgleich von jeder Datei *Data1*. Abschließend **Comp** wird die folgende Meldung angezeigt:

    `Compare more files (Y/N)?`

    Drücken Sie Y, um mehrere Dateien zu vergleichen. Die **Comp** Befehl werden Sie aufgefordert, für die Standorte und die Namen der neuen Dateien. Auf die Vergleiche Beenden drücken Sie N. Wenn Sie "Y" drücken **Comp** fordert Sie Befehlszeilenoptionen verwenden. Wenn Sie keine Befehlszeilenoptionen angeben **Comp** wird verwendet, die Sie vor dem angegebenen Werten.

## <a name="BKMK_examples"></a>Beispiele für

Um den Inhalt des Verzeichnisses C:\Reports mit Sicherungsverzeichnis vergleichen \\ \\Sales\Backup\April, Typ:
```
comp c:\reports \\sales\backup\april
```
Um die ersten zehn Zeilen der Textdateien im Verzeichnis \Invoice vergleichen und das Ergebnis im Dezimalformat angezeigt, geben Sie Folgendes ein:
```
comp \invoice\*.txt \invoice\backup\*.txt /n=10 /d
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)