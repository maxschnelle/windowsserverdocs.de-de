---
title: print
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa2325d5-a993-4ed3-b996-255165452db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d85fc5b2cd5f5ba09ebdf4756a5adb60c1759f2a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831551"
---
# <a name="print"></a>print



Sendet eine Text-Datei an einen Drucker an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Print [/d:<PrinterName>] [<Drive>:][<Path>]<FileName>[ ...]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ d:\<Druckername >|Gibt den Drucker, den den Auftrag gedruckt werden soll. Um mit einem lokal verbundenen Drucker zu drucken, geben Sie den Port auf dem Computer, in dem der Drucker angeschlossen ist.</br>-Gültige Werte für parallele Anschlüsse sind LPT1, LPT2 und LPT3.</br>-Die gültigen Werte für serielle Anschlüsse sind COM1, COM2, COM3 und COM4.</br>Sie können auch einen Netzwerkdrucker angeben, unter Verwendung des Warteschlangennamens (\\\\*ServerName*\*Druckername *). Wenn Sie einen Drucker nicht angeben, wird der Druckauftrag an LPT1 standardmäßig gesendet.|
|\<Laufwerk >:|Gibt das logische oder physische Laufwerk, auf dem sich die Datei, die Sie drucken möchten befindet. Dieser Parameter ist nicht erforderlich, wenn die Datei, die Sie drucken möchten, auf das aktuelle Laufwerk befindet.|
|\<Pfad >|Gibt den Speicherort der Datei, die Sie drucken möchten. Dieser Parameter ist nicht erforderlich, wenn sich die Datei, die Sie drucken möchten, im aktuellen Verzeichnis befindet.|
|\<Dateiname > [...]|Erforderlich. Gibt die Datei, die Sie drucken möchten. Sie können mehrere Dateien in einem Befehl einschließen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Eine Datei kann im Hintergrund drucken, wenn es sich bei der Übermittlung an einen Drucker mit einem seriellen oder parallelen Port auf dem lokalen Computer verbunden sind.
-   Sie können viele Konfigurationsaufgaben an der Eingabeaufforderung ausführen, mit der **Modus** Befehl.

    Finden Sie unter [Modus](mode.md) für Weitere Informationen:  
    -   Konfigurieren einen Drucker, die mit einem parallelen Anschluss verbunden sind
    -   Konfigurieren einen Drucker mit einem seriellen Anschluss verbunden
    -   Anzeigen des Status eines Druckers
    -   Vorbereiten eines Druckers zum Wechseln der Codepage

## <a name="BKMK_examples"></a>Beispiele für

Um die Datei LPT2 Report.txt im aktuellen Verzeichnis an einen Drucker auf dem lokalen Computer verbunden zu senden, geben Sie Folgendes ein:
```
print /d:lpt2 report.txt
```
Die Druckwarteschlange Drucker1 die Report.txt-Datei im Verzeichnis c:\Accounting an, auf die \\ \\Kopierraum-Server, Typ:
```
print /d:\\copyroom\printer1 c:\accounting\report.txt 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

[Druckbefehlsreferenz](print-command-reference.md)

[Modus](mode.md)