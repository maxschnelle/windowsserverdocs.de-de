---
title: md
description: Referenz Artikel für den MD-Befehl, der ein Verzeichnis oder ein Unterverzeichnis erstellt.
ms.topic: article
ms.assetid: 82162d00-cc34-4776-9e55-4b4836dbd6a9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94dd8f696b97d56fe082f73287a3d50dc7f70883
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886515"
---
# <a name="md"></a>md

Erstellt ein Verzeichnis oder ein Unterverzeichnis. Befehls Erweiterungen, die standardmäßig aktiviert sind, ermöglichen die Verwendung eines einzelnen **MD** -Befehls, um zwischen Verzeichnisse in einem angegebenen Pfad zu erstellen.

> [!NOTE]
> Dieser Befehl ist mit dem Befehl " [mkdir](mkdir.md)" identisch.

## <a name="syntax"></a>Syntax

```
md [<drive>:]<path>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<drive>`: | Gibt das Laufwerk an, auf dem das neue Verzeichnis erstellt werden soll. |
| `<path>` | Gibt den Namen und den Speicherort des neuen Verzeichnisses an. Die maximale Länge eines einzelnen Pfads wird vom Dateisystem festgelegt. Dies ist ein erforderlicher Parameter. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Verzeichnis mit dem Namen *directory1* innerhalb des aktuellen Verzeichnisses zu erstellen:

```
md Directory1
```

Geben Sie Folgendes ein, um die Verzeichnisstruktur *taxes\property\current* innerhalb des Stamm Verzeichnisses mit aktivierter Befehls Erweiterung zu erstellen:

```
md \Taxes\Property\Current
```

Um die Verzeichnisstruktur *taxes\property\current* innerhalb des Stamm Verzeichnisses wie im vorherigen Beispiel zu erstellen, aber mit deaktivierten Befehls Erweiterungen, geben Sie die folgende Befehlssequenz ein:

```
md \Taxes
md \Taxes\Property
md \Taxes\Property\Current
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [mkdir-Befehl](mkdir.md)