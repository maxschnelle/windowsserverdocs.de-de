---
title: bdehdcfg size
description: Referenz Artikel für den bdehdcfg size-Befehl, der die Größe der Systempartition angibt, wenn ein neues Systemlaufwerk erstellt wird.
ms.topic: reference
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c68322fe999a39c4a2913826f520f0b401a9d0ac
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632826"
---
# <a name="bdehdcfg-size"></a>bdehdcfg: Größe

Gibt die Größe der Systempartition an, wenn ein neues Systemlaufwerk erstellt wird. Wenn Sie keine Größe angeben, verwendet das Tool den Standardwert von 300 MB. Die minimale Größe des Systemlaufwerks beträgt 100 MB. Wenn Sie die Systemwiederherstellung oder andere Systemtools auf der Systempartition speichern, sollten Sie die Größe entsprechend anpassen.

> [!NOTE]
> Der **size** -Befehl kann nicht mit dem `target <drive_letter> merge` Befehl kombiniert werden.

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink} -size <size_in_mb>
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<size_in_mb>` | Gibt die Anzahl der Megabytes (MB) an, die für die neue Partition verwendet werden soll. |

## <a name="examples"></a>Beispiele

So weisen Sie 500 MB dem Standardsystem Laufwerk zu:

```
bdehdcfg -target default -size 500
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
