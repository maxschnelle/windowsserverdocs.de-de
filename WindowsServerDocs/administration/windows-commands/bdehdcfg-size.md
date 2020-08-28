---
title: bdehdcfg size
description: Referenz Artikel für den bdehdcfg size-Befehl, der die Größe der Systempartition angibt, wenn ein neues Systemlaufwerk erstellt wird.
ms.topic: reference
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f4aaedbbac5783fdf54814d7cf97ef9c70c9d346
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031478"
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

| Parameter | Beschreibung |
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
