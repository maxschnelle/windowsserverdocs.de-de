---
title: print
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: ada0657e2f17754e55e97e6488aac99fb0025afb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372151"
---
# <a name="print"></a>print



Sendet eine Textdatei an einen Drucker.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Print [/d:<PrinterName>] [<Drive>:][<Path>]<FileName>[ ...]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/d: \<printername >|Gibt den Drucker an, den Sie den Auftrag drucken möchten. Geben Sie den Port auf dem Computer an, auf dem der Drucker angeschlossen ist, um auf einem lokal verbundenen Drucker zu drucken.</br>-Gültige Werte für parallele Ports sind LPT1, LPT2 und LPT3.</br>-Gültige Werte für serielle Ports sind COM1, COM2, COM3 und COM4.</br>Sie können auch einen Netzwerkdrucker angeben, indem Sie den Warteschlangen Namen (\\ @ no__t-1*Servername*\*printername *) verwenden. Wenn Sie keinen Drucker angeben, wird der Druckauftrag standardmäßig an LPT1 gesendet.|
|> \<drive:|Gibt das logische oder physische Laufwerk an, auf dem sich die Datei befindet, die Sie drucken möchten. Dieser Parameter ist nicht erforderlich, wenn sich die Datei, die Sie drucken möchten, auf dem aktuellen Laufwerk befindet.|
|\<path >|Gibt den Speicherort der Datei an, die gedruckt werden soll. Dieser Parameter ist nicht erforderlich, wenn sich die Datei, die Sie drucken möchten, im aktuellen Verzeichnis befindet.|
|\<filename > [...]|Erforderlich. Gibt die Datei an, die Sie drucken möchten. Sie können mehrere Dateien in einem Befehl einschließen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Eine Datei kann im Hintergrund gedruckt werden, wenn Sie an einen Drucker gesendet wird, der mit einem seriellen oder parallelen Port auf dem lokalen Computer verbunden ist.
-   Sie können viele Konfigurationsaufgaben über die Eingabeaufforderung ausführen, indem Sie den **Modus** -Befehl verwenden.

    Weitere Informationen zu den folgenden Informationen finden Sie im [Modus](mode.md) :  
    -   Konfigurieren eines mit einem parallelen Port verbundenen Druckers
    -   Konfigurieren eines mit einem seriellen Anschluss verbundenen Druckers
    -   Anzeigen des Status eines Druckers
    -   Vorbereiten eines Druckers für den Code Page Wechsel

## <a name="BKMK_examples"></a>Beispiele

Um die Datei "Report. txt" im aktuellen Verzeichnis an einen Drucker zu senden, der mit LPT2 auf dem lokalen Computer verbunden ist, geben Sie Folgendes ein:
```
print /d:lpt2 report.txt
```
Geben Sie Folgendes ein, um die Datei "Report. txt" im Verzeichnis "c:\Accounting" an die printer1-Druck Warteschlange auf dem \\ @ no__t-1copyroom-Server zu senden:
```
print /d:\\copyroom\printer1 c:\accounting\report.txt 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Druckbefehlsreferenz](print-command-reference.md)

[Modus](mode.md)