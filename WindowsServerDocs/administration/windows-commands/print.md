---
title: print
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa2325d5-a993-4ed3-b996-255165452db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 36966d8d3beb032ee0dcee50d9bd5bc0111bf4f5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837373"
---
# <a name="print"></a>print



Sendet eine Textdatei an einen Drucker.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Print [/d:<PrinterName>] [<Drive>:][<Path>]<FileName>[ ...]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/d:\<PrinterName >|Gibt den Drucker an, den Sie den Auftrag drucken möchten. Geben Sie den Port auf dem Computer an, auf dem der Drucker angeschlossen ist, um auf einem lokal verbundenen Drucker zu drucken.</br>-Gültige Werte für parallele Ports sind LPT1, LPT2 und LPT3.</br>-Gültige Werte für serielle Ports sind COM1, COM2, COM3 und COM4.</br>Sie können einen Netzwerkdrucker auch angeben, indem Sie den Warteschlangen Namen (\\\\*Server* Name\*PrinterName *) verwenden. Wenn Sie keinen Drucker angeben, wird der Druckauftrag standardmäßig an LPT1 gesendet.|
|\<Laufwerk >:|Gibt das logische oder physische Laufwerk an, auf dem sich die Datei befindet, die Sie drucken möchten. Dieser Parameter ist nicht erforderlich, wenn sich die Datei, die Sie drucken möchten, auf dem aktuellen Laufwerk befindet.|
|\<Pfad >|Gibt den Speicherort der Datei an, die gedruckt werden soll. Dieser Parameter ist nicht erforderlich, wenn sich die Datei, die Sie drucken möchten, im aktuellen Verzeichnis befindet.|
|\<Dateiname > [...]|Erforderlich Gibt die Datei an, die Sie drucken möchten. Sie können mehrere Dateien in einem Befehl einschließen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Eine Datei kann im Hintergrund gedruckt werden, wenn Sie an einen Drucker gesendet wird, der mit einem seriellen oder parallelen Port auf dem lokalen Computer verbunden ist.
-   Sie können viele Konfigurationsaufgaben über die Eingabeaufforderung ausführen, indem Sie den **Modus** -Befehl verwenden.

    Weitere Informationen zu den folgenden Informationen finden Sie im [Modus](mode.md) :  
    -   Konfigurieren eines mit einem parallelen Port verbundenen Druckers
    -   Konfigurieren eines mit einem seriellen Anschluss verbundenen Druckers
    -   Anzeigen des Status eines Druckers
    -   Vorbereiten eines Druckers für den Code Page Wechsel

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um die Datei "Report. txt" im aktuellen Verzeichnis an einen Drucker zu senden, der mit LPT2 auf dem lokalen Computer verbunden ist, geben Sie Folgendes ein:
```
print /d:lpt2 report.txt
```
Geben Sie Folgendes ein, um die Datei "Report. txt" im Verzeichnis "c:\Accounting" an die printer1-Warteschlange auf der \\\\copyroom-Server zu senden:
```
print /d:\\copyroom\printer1 c:\accounting\report.txt 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Druckbefehlsreferenz](print-command-reference.md)

[Modus](mode.md)