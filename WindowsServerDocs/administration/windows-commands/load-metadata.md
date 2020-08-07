---
title: load metadata
description: Referenz Artikel für den Befehl "Metadaten laden", der vor dem Importieren einer austauschen-Schatten Kopie eine Datei vom Typ "Metadata. cab" lädt oder die Writer-Metadaten bei einer Wiederherstellung lädt.
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b0f5412ee189814fcdf1f020f238e19dc308b7d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887484"
---
# <a name="load-metadata"></a>Metadaten laden

Lädt eine Datei "Metadata. cab" vor dem Importieren einer austauschen-Schatten Kopie oder lädt die Writer-Metadaten im Fall einer Wiederherstellung. Bei Verwendung ohne Parameter zeigt die Eingabe **Metadaten** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
load metadata [<drive>:][<path>]<metadata.cab>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `[<drive>:][<path>]` | Gibt den Speicherort der Metadatendatei an. |
| metadata.cab | Gibt die zu ladende Datei "Metadata. cab" an. |

## <a name="remarks"></a>Bemerkungen

- Sie können den **Import** -Befehl verwenden, um eine austauschen-Schatten Kopie auf Grundlage der Metadaten zu importieren, die durch **Laden von Metadaten**angegeben werden.

- Sie müssen diesen Befehl vor dem Befehl **Restore BEGIN** ausführen, um die ausgewählten Writer und Komponenten für die Wiederherstellung zu laden.

## <a name="examples"></a>Beispiele

Zum Laden einer Metadatendatei namens metafile.cab vom Standard Speicherort geben Sie Folgendes ein:

```
load metadata metafile.cab
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "DiskShadow importieren"](import.md)

- [Befehl "Wiederherstellen"](begin-restore.md)
