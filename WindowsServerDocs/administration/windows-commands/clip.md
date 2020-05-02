---
title: Clip
description: Referenz Thema für den Clip-Befehl, der die Befehlszeile von der Befehlszeile an die Windows-Zwischenablage umleitet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61c905e3dcce52f3a3d35adeac55fc5df574f664
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712792"
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

Geben Sie Folgendes ein, um den Inhalt einer Datei namens "Infodatei *. txt* " in die Windows-Zwischenablage zu kopieren:

```
clip < readme.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)