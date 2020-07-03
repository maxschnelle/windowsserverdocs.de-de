---
title: select
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6004d39e225b1ac4acd96b4108accff2ccfc485c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935934"
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

|Parameter|Beschreibung|
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

