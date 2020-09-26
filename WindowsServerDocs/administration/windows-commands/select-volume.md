---
title: select volume
description: Referenz Artikel für den Befehl Volume auswählen, mit dem das angegebene Volume ausgewählt und der Fokus auf das Volume verlagert wird.
ms.topic: reference
ms.assetid: 5d70d776-80ad-4f20-8288-a7997fb1df28
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 643db6484842e8a67462b0460a1ecdeac653e577
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389188"
---
# <a name="select-volume"></a>select volume

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wählt das angegebene Volume aus und verschiebt den Fokus auf das Volume. Dieser Befehl kann auch verwendet werden, um das Volume anzuzeigen, das derzeit den Fokus auf dem ausgewählten Datenträger hat.

## <a name="syntax"></a>Syntax

```
select volume={<n>|<d>}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<n>` | Die Nummer des Volumes, das den Fokus erhalten soll. Sie können die Zahlen für alle Volumes auf dem aktuell ausgewählten Datenträger anzeigen, indem Sie den Befehl **Volume auflisten** in DiskPart verwenden. |
| `<d> `| Der Laufwerk Buchstabe oder der einstellungspunktpfad des Volumes, das den Fokus erhalten soll. |

## <a name="remarks"></a>Hinweise

- Wenn kein Volume angegeben ist, zeigt dieser Befehl das Volume an, das derzeit den Fokus auf dem ausgewählten Datenträger hat.

- Auf einem Basis Datenträger wird beim Auswählen eines Volumes auch der Fokus auf die entsprechende Partition fest.

  - Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.

  - Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.

## <a name="examples"></a>Beispiele

Wenn Sie den Fokus auf *Volume 2*verschieben möchten, geben Sie Folgendes ein:

```
select volume=2
```

Um den Fokus auf *Laufwerk C*zu verschieben, geben Sie Folgendes ein:

```
select volume=c
```

Um den Fokus auf das Volume zu verschieben, das in einem Ordner namens *c:\mountpath*eingebunden ist, geben Sie Folgendes ein:

```
select volume=c:\mountpath
```

Geben Sie Folgendes ein, um das Volume anzuzeigen, das derzeit den Fokus auf dem ausgewählten Datenträger hat:

```
select volume
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl Volume hinzufügen](add-volume.md)

- [Attribute Volume (Befehl)](attributes-volume.md)

- [volumespiegelungs-Befehl erstellen](create-volume-mirror.md)

- [Create Volume-RAID-Befehl](create-volume-raid.md)

- [Create Volume Simple-Befehl](create-volume-simple.md)

- [Create Volume Stripe-Befehl](create-volume-stripe.md)

- [Befehl "Volume löschen"](delete-volume.md)

- [Befehl "Detail Volume"](detail-volume.md)

- [Befehl "ssutil Volume"](fsutil-volume.md)

- [Befehl "Volume auflisten"](list-volume.md)

- [Befehl "Offline Volume"](offline-volume.md)

- [Befehl "Onine Volume"](online-volume.md)

- [Datenträger Befehl auswählen](select-disk.md)

- [Partitions Befehl auswählen](select-partition.md)

- [Vdisk-Befehl auswählen](select-vdisk.md)
