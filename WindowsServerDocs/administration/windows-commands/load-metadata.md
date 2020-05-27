---
title: Metadaten laden
description: Referenz Thema für den Befehl "Metadaten laden", mit dem eine Datei "Metadata. cab" geladen wird, bevor eine austauschen-Schatten Kopie importiert wird, oder die Writer-Metadaten im Fall einer Wiederherstellung geladen werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c7dc967476412261e7afc228088566f74ec4208c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820190"
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
| Metadaten. cab | Gibt die zu ladende Datei "Metadata. cab" an. |

## <a name="remarks"></a>Hinweise

- Sie können den **Import** -Befehl verwenden, um eine austauschen-Schatten Kopie auf Grundlage der Metadaten zu importieren, die durch **Laden von Metadaten**angegeben werden.

- Sie müssen diesen Befehl vor dem Befehl **Restore BEGIN** ausführen, um die ausgewählten Writer und Komponenten für die Wiederherstellung zu laden.

## <a name="examples"></a>Beispiele

Zum Laden einer Metadatendatei namens "Metafile. cab" aus dem Standard Speicherort geben Sie Folgendes ein:

```
load metadata metafile.cab
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "DiskShadow importieren"](import.md)

- [Befehl "Wiederherstellen"](begin-restore.md)
