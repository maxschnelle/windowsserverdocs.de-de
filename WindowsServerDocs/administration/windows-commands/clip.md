---
title: Clip
description: Referenz Artikel für den Clip-Befehl, der die Befehlszeile von der Befehlszeile an die Windows-Zwischenablage umleitet.
ms.topic: reference
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a94003a700f3dc08d97a78911f844adcbbfe646a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025964"
---
# <a name="clip"></a>Clip

Leitet die Befehlsausgabe von der Befehlszeile an die Windows-Zwischenablage um. Mit diesem Befehl können Sie Daten direkt in eine beliebige Anwendung kopieren, die Text aus der Zwischenablage empfangen kann. Sie können diese Textausgabe auch in andere Programme einfügen.

## <a name="syntax"></a>Syntax

```
<command> | clip
clip < <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<command>` | Gibt einen Befehl an, dessen Ausgabe Sie an die Windows-Zwischenablage senden möchten. |
| `<filename>` | Gibt eine Datei an, deren Inhalt Sie an die Windows-Zwischenablage senden möchten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Um die aktuelle Verzeichnisliste in die Windows-Zwischenablage zu kopieren, geben Sie Folgendes ein:

```
dir | clip
```

Geben Sie Folgendes ein, um die Ausgabe eines Programms namens *Generic. awk* in die Windows-Zwischenablage zu kopieren:

```
awk -f generic.awk input.txt | clip
```

Um den Inhalt einer Datei mit dem Namen *readme.txt* in die Windows-Zwischenablage zu kopieren, geben Sie Folgendes ein:

```
clip < readme.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)