---
title: SELECT-Befehle
description: Referenz Artikel zu den Select-Befehlen, die den Fokus auf einen Datenträger, eine Partition, ein Volume oder eine virtuelle Festplatte (VHD) verschieben.
ms.topic: reference
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2b322fc7bf9355e64fbe14a0823c85dddadd6171
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389178"
---
# <a name="select-commands"></a>SELECT-Befehle

Verschiebt den Fokus auf einen Datenträger, eine Partition, ein Volume oder eine virtuelle Festplatte (VHD).

## <a name="syntax"></a>Syntax

```
select disk
select partition
select vdisk
select volume
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [Datenträger auswählen](select-disk.md) | Verschiebt den Fokus auf einen Datenträger. |
| [Partition auswählen](select-partition.md) | Verschiebt den Fokus auf eine Partition. |
| [Vdisk auswählen](select-vdisk.md) | Verschiebt den Fokus auf eine virtuelle Festplatte. |
| [Volume auswählen](select-volume.md) | Verschiebt den Fokus auf ein Volume. |

#### <a name="remarks"></a>Hinweise

- Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.

- Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
