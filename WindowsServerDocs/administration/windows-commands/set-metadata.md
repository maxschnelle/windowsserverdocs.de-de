---
title: set metadata
description: Referenz Artikel für den Befehl Set Metadata, der den Namen und den Speicherort der Metadatendatei für die Schatten Erstellung festlegt, die zum Übertragen von Schatten Kopien von einem Computer auf einen anderen verwendet wird.
ms.topic: reference
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2ff03661d953ae7afc39117ced89734c5df02c14
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389074"
---
# <a name="set-metadata"></a>set metadata

Legt den Namen und den Speicherort der Metadatendatei für die Schatten Erstellung fest, mit der Schatten Kopien von einem Computer auf einen anderen übertragen werden Bei Verwendung ohne Parameter zeigt **Set Metadata** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
set metadata [<drive>:][<path>]<metadata.cab>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `[<drive>:][<path>]` | Gibt den Speicherort zum Erstellen der Metadatendatei an. |
| `<metadata.cab>` | Gibt den Namen der CAB-Datei zum Speichern von Metadaten für die Schatten Erstellung an. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Kontext Befehl festlegen](set-context.md)

- [Befehl "Set Option"](set-option.md)

- [Befehl "ausführliche festlegen"](set-verbose.md)
