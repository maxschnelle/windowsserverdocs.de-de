---
title: select
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: da601731f9abe1f84f082fd91528db03e6a8b05a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638999"
---
# <a name="select"></a>select



Verschiebt den Fokus auf einen Datenträger, eine Partition, ein Volume oder eine virtuelle Festplatte (VHD).

## <a name="syntax"></a>Syntax

```
select disk
select partition
select volume
select vdisk
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[Datenträger auswählen](select-disk.md)|Verschiebt den Fokus auf einen Datenträger.|
|[Partition auswählen](select-partition.md)|Verschiebt den Fokus auf eine Partition.|
|[Volume auswählen](select-volume.md)|Verschiebt den Fokus auf ein Volume.|
|[Vdisk auswählen](select-vdisk.md)|Verschiebt den Fokus auf eine virtuelle Festplatte.|

## <a name="remarks"></a>Hinweise

-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.
-   Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

