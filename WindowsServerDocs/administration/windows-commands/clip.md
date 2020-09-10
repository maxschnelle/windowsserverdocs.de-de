---
title: Clip
description: Referenz Artikel für den Clip-Befehl, der die Befehlszeile von der Befehlszeile an die Windows-Zwischenablage umleitet.
ms.topic: reference
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9f6820d60a8c94ed07bbb23bbbd86be3f1f289b7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629619"
---
# <a name="clip"></a>Clip

Leitet die Befehlsausgabe von der Befehlszeile an die Windows-Zwischenablage um. Mit diesem Befehl können Sie Daten direkt in eine beliebige Anwendung kopieren, die Text aus der Zwischenablage empfangen kann. Sie können diese Textausgabe auch in andere Programme einfügen.

## <a name="syntax"></a>Syntax

```
<command> | clip
clip < <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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