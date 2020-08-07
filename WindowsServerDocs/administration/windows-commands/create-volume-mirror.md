---
title: create volume mirror
description: Referenz Artikel für den Befehl Volume-Spiegelung erstellen, mit dem eine volumespiegelung mithilfe der beiden angegebenen dynamischen Datenträger erstellt wird.
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f25c78a49393a0c48330a7b705c14b906f827c33
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879849"
---
# <a name="create-volume-mirror"></a>create volume mirror

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine volumespiegelung mithilfe der beiden angegebenen dynamischen Datenträger. Nachdem das Volume erstellt wurde, wird der Fokus automatisch auf das neue Volume verlagert.

## <a name="syntax"></a>Syntax

```
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Größe =`<n>` | Gibt die Menge des Speicherplatzes in Megabyte (MB) an, die das Volume auf den einzelnen Datenträgern einnimmt. Wenn keine Größe angegeben ist, nimmt das neue Volume den verbleibenden freien Speicherplatz auf dem kleinsten Datenträger und den gleichen Speicherplatz auf jedem nachfolgenden Datenträger an. |
| Disk = `<n>` , `<n>` [ `,<n>,...` ] | Gibt die dynamischen Datenträger an, auf denen das Spiegelungs Volume erstellt wird. Zum Erstellen eines Spiegelungs Volumes benötigen Sie zwei dynamische Datenträger. Eine Menge an Speicherplatz, die der Größe entspricht, die mit dem **size** -Parameter angegeben wird, wird auf jedem Datenträger zugeordnet. |
| ausrichten =`<n>` | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Dieser Parameter wird in der Regel mit den Hardware-RAID-Arrays der logischen Gerätenummer verwendet, um die Leistung zu verbessern. `<n>`die Anzahl der Kilobyte (KB) vom Anfang des Datenträgers bis zur nächsten Ausrichtungs Grenze. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehler beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie auf den Datenträgern 1 und 2 Folgendes ein, um ein gespiegeltes Volume mit einer Größe von 1000 Megabyte zu erstellen:

```
create volume mirror size=1000 disk=1,2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)
