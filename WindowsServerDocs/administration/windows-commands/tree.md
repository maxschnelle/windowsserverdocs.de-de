---
title: tree
description: Referenz Artikel für Tree, der die Verzeichnisstruktur eines Pfads oder des Datenträgers auf einem Laufwerk grafisch anzeigt.
ms.topic: reference
ms.assetid: 345d3192-401e-4a3b-a8ac-36a85c7be79d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c9f586dbcf9072feffe71e1c3d792f10afc951a4
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156400"
---
# <a name="tree"></a>tree

Zeigt die Verzeichnisstruktur eines Pfads oder des Datenträgers auf einem Laufwerk grafisch an. Die Struktur, die von diesem Befehl angezeigt wird, hängt von den Parametern ab, die Sie an der Eingabeaufforderung angeben. Wenn Sie kein Laufwerk oder einen Pfad angeben, zeigt dieser Befehl die Struktur an, beginnend mit dem aktuellen Verzeichnis des aktuellen Laufwerks.

## <a name="syntax"></a>Syntax

```
tree [<drive>:][<path>] [/f] [/a]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<drive>:` | Gibt das Laufwerk an, das den Datenträger enthält, für den Sie die Verzeichnisstruktur anzeigen möchten. |
| `<path>` | Gibt das Verzeichnis an, für das Sie die Verzeichnisstruktur anzeigen möchten. |
| /f | Zeigt die Namen der Dateien in jedem Verzeichnis an. |
| /a | Gibt an, dass Textzeichen anstelle von Grafikzeichen verwendet werden sollen, um die Zeilen anzuzeigen, die Unterverzeichnisse verknüpfen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Namen aller Unterverzeichnisse auf dem Datenträger auf dem aktuellen Laufwerk anzuzeigen:

```
tree \
```

Geben Sie Folgendes ein, um die Dateien in allen Verzeichnissen auf Laufwerk C anzuzeigen:

```
tree c:\ /f | more
```

Geben Sie Folgendes ein, um eine Liste aller Verzeichnisse auf Laufwerk C zu drucken:

```
tree c:\ /f  prn
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
