---
title: bdehdcfg-Größe
description: Windows-Befehls Thema für **bdehdcfg size**, das die Größe der Systempartition angibt, wenn ein neues Systemlaufwerk erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c72bdfd0b8bf4dfd0aa36885ceb7fd249a18c332
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851023"
---
# <a name="bdehdcfg-size"></a>bdehdcfg: Größe

Gibt die Größe der Systempartition an, wenn ein neues Systemlaufwerk erstellt wird.

Ein Beispiel für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink} -size <SizeinMB>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<SizeinMB>` | Gibt die Anzahl der Megabytes (MB) an, die für die neue Partition verwendet werden soll. |

## <a name="remarks"></a>Hinweise

Wenn Sie keine Größe angeben, verwendet das Tool den Standardwert von 300 MB. Die minimale Größe des Systemlaufwerks beträgt 100 MB. Wenn Sie die Systemwiederherstellung oder andere Systemtools auf der Systempartition speichern, sollten Sie die Größe entsprechend anpassen.

> [!NOTE]
> Der **size** -Befehl kann nicht mit dem **Ziel** `<DriveLetter>` **Merge** -Befehl kombiniert werden.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Im folgenden Beispiel wird die Verwendung des Befehls **size** zum Zuordnen von 500 MB zum Standardsystem Laufwerk veranschaulicht.

```
bdehdcfg -target default -size 500
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)