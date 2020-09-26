---
title: select partition
description: Referenz Artikel für den Befehl Partition auswählen, der die angegebene Partition auswählt und den Fokus darauf verschiebt.
ms.topic: reference
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6418ff1a08bdc12355d2b2dc75bbb7151539ae02
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389233"
---
# <a name="select-partition"></a>select partition

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wählt die angegebene Partition aus und verschiebt den Fokus darauf. Dieser Befehl kann auch verwendet werden, um die Partition anzuzeigen, die derzeit den Fokus auf dem ausgewählten Datenträger hat.

## <a name="syntax"></a>Syntax

```
select partition=<n>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Partition =`<n>` | Die Nummer der Partition, die den Fokus erhalten soll. Sie können die Zahlen für alle Partitionen auf dem aktuell ausgewählten Datenträger anzeigen, indem Sie den Befehl **Partition auflisten** in DiskPart verwenden. |

#### <a name="remarks"></a>Hinweise

- Bevor Sie eine Partition auswählen können, müssen Sie zunächst mithilfe des Befehls **Select Disk** (Datenträger auswählen) einen Datenträger auswählen.

  - Wenn keine Partitionsnummer angegeben ist, zeigt diese Option die Partition an, die derzeit den Fokus auf dem ausgewählten Datenträger hat.

  - Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.

  - Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.

## <a name="examples"></a>Beispiele

Wenn Sie den Fokus auf *Partition 3*verschieben möchten, geben Sie Folgendes ein:

```
select partitition=3
```

Geben Sie Folgendes ein, um die Partition anzuzeigen, die derzeit den Fokus auf dem ausgewählten Datenträger hat:

```
select partition
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create Partition (EFI-Befehl)](create-partition-efi.md)

- [Befehl "erweiterte Partition erstellen"](create-partition-extended.md)

- [Create Partition (logischer Befehl)](create-partition-logical.md)

- [Create Partition (MSR-Befehl)](create-partition-msr.md)

- [create partition primary-Befehl](create-partition-primary.md)

- [Befehl "Partition löschen"](delete-partition.md)

- [Detail Partitions Befehl](detail-partition.md)

- [Datenträger Befehl auswählen](select-disk.md)

- [Vdisk-Befehl auswählen](select-vdisk.md)

- [Befehl "Volume auswählen"](select-volume.md)
