---
title: ren
description: Referenz Artikel für den Befehl "ren", der eine Datei oder ein Verzeichnis umbenennt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60398e12-a05d-4524-a73a-0a925943e21d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: c5f873de224ff335be097d97c7d8933a70af726d
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409671"
---
# <a name="ren"></a>ren

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Benennt Dateien oder Verzeichnisse um.

> [!NOTE]
> Dieser Befehl ist mit dem Befehl [Rename](rename.md)identisch.

## <a name="syntax"></a>Syntax

```
ren [<drive>:][<path>]<filename1> <filename2>
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
ren *.txt *.doc
```

Um den Namen eines Verzeichnisses von *Chap10* zu *part10*zu ändern, geben Sie Folgendes ein:

```
ren chap10 part10
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl Umbenennen](rename.md)
