---
title: Auswählen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9ad7051978f4b509f54bf783f71943b65617bc7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834653"
---
# <a name="select"></a>Auswählen



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

