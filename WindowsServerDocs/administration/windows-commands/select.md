---
title: select
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4c3723dd414adca68c22011ef3f6be02eb6531d5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889901"
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
|[Wählen Sie Datenträger](select-disk.md)|Verschiebt den Fokus auf einen Datenträger an.|
|[Wählen Sie die partition](select-partition.md)|Verschiebt den Fokus auf eine Partition an.|
|[Wählen Sie volume](select-volume.md)|Verschiebt den Fokus auf ein Volume an.|
|[Wählen Sie die virtuellen Datenträger](select-vdisk.md)|Verschiebt den Fokus auf eine virtuelle Festplatte an.|

## <a name="remarks"></a>Hinweise

-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.
-   Wenn eine Partition mit einer entsprechenden Menge ausgewählt ist, wird das Volume automatisch ausgewählt.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

