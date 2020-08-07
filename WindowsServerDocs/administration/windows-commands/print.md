---
title: print
description: Referenz Artikel für den Print-Befehl, der eine Textdatei an einen Drucker sendet.
ms.topic: article
ms.assetid: aa2325d5-a993-4ed3-b996-255165452db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: be955faa38af6a81ce5f61c255828470d906528c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884830"
---
# <a name="print"></a>print

Sendet eine Textdatei an einen Drucker. Eine Datei kann im Hintergrund gedruckt werden, wenn Sie an einen Drucker gesendet wird, der mit einem seriellen oder parallelen Port auf dem lokalen Computer verbunden ist.

> [!NOTE]
> Sie können über die Eingabeaufforderung viele Konfigurationsaufgaben ausführen, indem Sie den [Modus-Befehl](mode.md)verwenden, einschließlich des Konfigurierens eines Druckers, der mit einem parallelen oder seriellen Anschluss verbunden ist, den Druckerstatus anzeigt oder einen Drucker für den Code Page Wechsel vorbereitet.

## <a name="syntax"></a>Syntax

```
print [/d:<printername>] [<drive>:][<path>]<filename>[ ...]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /d`<printername>` | Gibt den Drucker an, den Sie den Auftrag drucken möchten. Geben Sie den Port auf dem Computer an, auf dem der Drucker angeschlossen ist, um auf einem lokal verbundenen Drucker zu drucken. Gültige Werte für parallele Ports sind **LPT1**, **LPT2**und **LPT3**. Gültige Werte für serielle Ports sind **COM1**, **COM2**, **COM3**und **COM4**. Sie können auch einen Netzwerkdrucker angeben, indem Sie den Warteschlangen Namen ( `\\server_name\printer_name` ) verwenden. Wenn Sie keinen Drucker angeben, wird der Druckauftrag standardmäßig an **LPT1** gesendet. |
| `<drive>`: | Gibt das logische oder physische Laufwerk an, auf dem sich die Datei befindet, die Sie drucken möchten. Dieser Parameter ist nicht erforderlich, wenn sich die Datei, die Sie drucken möchten, auf dem aktuellen Laufwerk befindet. |
| `<path>` | Gibt den Speicherort der Datei an, die gedruckt werden soll. Dieser Parameter ist nicht erforderlich, wenn sich die Datei, die Sie drucken möchten, im aktuellen Verzeichnis befindet. |
| `<filename>[ ...]` | Erforderlich. Gibt die Datei an, die Sie drucken möchten. Sie können mehrere Dateien in einem Befehl einschließen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Wenn Sie die **report.txt** Datei, die sich im aktuellen Verzeichnis befindet, an einen Drucker senden möchten, der mit **LPT2** auf dem lokalen Computer verbunden ist, geben Sie Folgendes ein:

```
print /d:lpt2 report.txt
```

Geben Sie Folgendes ein, um die **report.txt** Datei, die sich im Verzeichnis **c:\Accounting** befindet, an die **printer1** -Druck Warteschlange auf dem **/d: \\ copyroom** -Server zu senden:

```
print /d:\\copyroom\printer1 c:\accounting\report.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)

- [Mode-Befehl](mode.md)