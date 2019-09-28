---
title: select
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7dc3bc8775f971968f096ba4344348e77c112cfa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384110"
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

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Datenträger auswählen](select-disk.md)|Verschiebt den Fokus auf einen Datenträger.|
|[Partition auswählen](select-partition.md)|Verschiebt den Fokus auf eine Partition.|
|[Volume auswählen](select-volume.md)|Verschiebt den Fokus auf ein Volume.|
|[Vdisk auswählen](select-vdisk.md)|Verschiebt den Fokus auf eine virtuelle Festplatte.|

## <a name="remarks"></a>Hinweise

-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.
-   Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

