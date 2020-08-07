---
title: rename
description: Referenz Artikel für den RENAME-Befehl, der eine Datei oder ein Verzeichnis umbenennt.
ms.topic: article
ms.assetid: 7f2ea658-0fa9-4015-8031-22c2b0089231
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a2ab634be010f470314658b25daac92c00d4706c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883795"
---
# <a name="rename"></a>rename

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Benennt Dateien oder Verzeichnisse um.

> [!NOTE]
> Dieser Befehl ist mit dem Befehl " [ren](ren.md)" identisch.

## <a name="syntax"></a>Syntax

```
rename [<drive>:][<path>]<filename1> <filename2>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `[<drive>:][<path>]<filename1>` | Gibt den Speicherort und den Namen der Datei oder des Satzes von Dateien an, die Sie umbenennen möchten. *Filename1* kann Platzhalter Zeichen (**&#42;** und **?**) enthalten. |
| `<filename2>` | Gibt den neuen Namen für die Datei an. Mit Platzhalter Zeichen können Sie neue Namen für mehrere Dateien angeben. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Beim Umbenennen von Dateien können Sie kein neues Laufwerk oder einen neuen Pfad angeben. Sie können diesen Befehl auch nicht verwenden, um Dateien auf mehreren Laufwerken umzubenennen oder um Dateien in ein anderes Verzeichnis zu verschieben.

- Zeichen, die durch Platzhalter Zeichen in *filename2* dargestellt werden, sind mit den entsprechenden Zeichen in *filename1*identisch.

- *Filename2* muss ein eindeutiger Dateiname sein. Wenn *filename2* mit einem vorhandenen Dateinamen übereinstimmt, wird die folgende Meldung angezeigt: `Duplicate file name or file not found` .

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Dateinamen Erweiterungen von. txt im aktuellen Verzeichnis in doc-Erweiterungen zu ändern:

```
rename *.txt *.doc
```

Um den Namen eines Verzeichnisses von *Chap10* zu *part10*zu ändern, geben Sie Folgendes ein:

```
rename chap10 part10
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [ren-Befehl](ren.md)
