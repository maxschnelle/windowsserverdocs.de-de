---
title: mkdir
description: Referenz Artikel für den mkdir-Befehl, der ein Verzeichnis oder ein Unterverzeichnis erstellt.
ms.topic: reference
ms.assetid: 033a57a2-5deb-4c98-aa78-61ce8df2a330
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bfefe4bc040d3e3f28adb6b37529764f28fca25b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639506"
---
# <a name="mkdir"></a>mkdir

Erstellt ein Verzeichnis oder ein Unterverzeichnis. Befehls Erweiterungen, die standardmäßig aktiviert sind, ermöglichen die Verwendung eines einzelnen **mkdir** -Befehls, um zwischen Verzeichnisse in einem angegebenen Pfad zu erstellen.

> [!NOTE]
> Dieser Befehl ist mit dem MD- [Befehl](md.md)identisch.

## <a name="syntax"></a>Syntax

```
mkdir [<drive>:]<path>
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
mkdir Directory1
```

Geben Sie Folgendes ein, um die Verzeichnisstruktur *taxes\property\current* innerhalb des Stamm Verzeichnisses mit aktivierter Befehls Erweiterung zu erstellen:

```
mkdir \Taxes\Property\Current
```

Um die Verzeichnisstruktur *taxes\property\current* innerhalb des Stamm Verzeichnisses wie im vorherigen Beispiel zu erstellen, aber mit deaktivierten Befehls Erweiterungen, geben Sie die folgende Befehlssequenz ein:

```
mkdir \Taxes
mkdir \Taxes\Property
mkdir \Taxes\Property\Current
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [MD-Befehl](md.md)