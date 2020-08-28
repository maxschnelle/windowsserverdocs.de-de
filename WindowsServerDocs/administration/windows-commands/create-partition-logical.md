---
title: create partition logical
description: Referenz Artikel zum logischen Befehl "Create Partition", der eine logische Partition in einer vorhandenen erweiterten Partition erstellt.
ms.topic: reference
ms.assetid: 1f59b79a-d690-4d0e-ad38-40df5a0ce38e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a9a95e735fcaed0e7f588a3d4ba643c1787782b5
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033238"
---
# <a name="create-partition-logical"></a>create partition logical

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine logische Partition für eine vorhandene erweiterte Partition. Nachdem die Partition erstellt wurde, wird der Fokus automatisch auf die neue Partition verlagert.

>[!IMPORTANT]
> Sie können diesen Befehl nur auf MBR-Datenträgern (Master Boot Record) verwenden. Sie müssen den Befehl "Datenträger [auswählen](select-disk.md) " verwenden, um einen einfachen MBR-Datenträger auszuwählen und den Fokus darauf zu verschieben.
>
> Sie müssen eine [erweiterte Partition](create-partition-extended.md) erstellen, bevor Sie logische Laufwerke erstellen können.

## <a name="syntax"></a>Syntax

```
create partition logical [size=<n>] [offset=<n>] [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Größe =`<n>` | Gibt die Größe der logischen Partition in Megabyte (MB) an, die kleiner als die erweiterte Partition sein muss. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis der freie Speicherplatz in der erweiterten Partition nicht mehr verfügbar ist. |
| Offset =`<n>` | Gibt den Offset in Kilobyte (KB) an, bei dem die Partition erstellt wird. Der Offset wird aufgerundet, um die verwendete Zylinder Größe vollständig auszufüllen. Wenn kein Offset angegeben wird, wird die Partition in den ersten Datenträger Block eingefügt, der groß genug ist, um Sie zu speichern. Die Partition ist mindestens so lang wie die Zahl, die durch **size = `<n>` **angegeben wird. Wenn Sie eine Größe für die logische Partition angeben, muss sie kleiner als die erweiterte Partition sein. |
| ausrichten =`<n>` | Richtet alle Volumes oder Partitions Blöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit den Hardware-RAID-Arrays der logischen Gerätenummer verwendet, um die Leistung zu verbessern. `<n>` die Anzahl der Kilobyte (KB) vom Anfang des Datenträgers bis zur nächsten Ausrichtungs Grenze. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

#### <a name="remarks"></a>Bemerkungen

- Wenn die Parameter " **size** " und " **Offset** " nicht angegeben werden, wird die logische Partition in dem größten Datenträger Block erstellt, der in der erweiterten Partition verfügbar ist.

## <a name="examples"></a>Beispiele

Geben Sie in der erweiterten Partition des ausgewählten Datenträgers Folgendes ein, um eine logische Partition mit einer Größe von 1000 Megabyte zu erstellen:

```
create partition logical size=1000
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)

- [select disk](select-disk.md)
