---
title: select vdisk
description: Referenz Artikel für den Befehl Vdisk auswählen, der die angegebene virtuelle Festplatte (VHD) auswählt und den Fokus darauf verschiebt.
ms.topic: reference
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 19e842115f914711cc59cfb770ee19f732b3a388
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389206"
---
# <a name="select-vdisk"></a>select vdisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wählt die angegebene virtuelle Festplatten \( -VHD aus \) und verschiebt den Fokus darauf.

## <a name="syntax"></a>Syntax

```
select vdisk file=<full path> [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Datei =`<full path>` | Gibt den vollständigen Pfad und den Dateinamen einer vorhandenen VHD-Datei an. |
| Noerr | Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Um den Fokus auf die virtuelle Festplatte namens *c:\test\test.VHD*zu verschieben, geben Sie Folgendes ein:

```
select vdisk file=c:\test\test.vhd
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [attach vdisk](attach-vdisk.md)

- [compact vdisk](compact-vdisk.md)

- [detach vdisk](detach-vdisk.md)

- [detail vdisk](detail-vdisk.md)

- [expand vdisk](expand-vdisk.md)

- [merge vdisk](merge-vdisk.md)

- [list](list.md)

- [Datenträger Befehl auswählen](select-disk.md)

- [Partitions Befehl auswählen](select-partition.md)

- [Befehl "Volume auswählen"](select-volume.md)