---
title: create volume raid
description: Referenz Artikel zum Create Volume RAID-Befehl, mit dem ein RAID-5-Volume mit drei oder mehr angegebenen dynamischen Datenträgern erstellt wird.
ms.topic: reference
ms.assetid: 9f257950-9240-4d5f-9537-8ad653d48ebf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c936205f6132a8a2bc06e455dd07761715df684f
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033148"
---
# <a name="create-volume-raid"></a>create volume raid

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt ein RAID-5-Volume mit drei oder mehr angegebenen dynamischen Datenträgern. Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.

## <a name="syntax"></a>Syntax

```
create volume raid [size=<n>] disk=<n>,<n>,<n>[,<n>,...] [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Größe =`<n>` | Die Menge des Speicherplatzes in Megabyte (MB), die das Volume auf den einzelnen Datenträgern einnimmt. Wenn keine Größe angegeben wird, wird das größte mögliche RAID-5-Volume erstellt. Der Datenträger mit dem kleinsten verfügbaren, verfügbaren freien Speicherplatz bestimmt die Größe des RAID-5-Volumes, und der Speicherplatz wird von jedem Datenträger zugeordnet. Der tatsächliche Speicherplatz auf dem RAID-5-Volume ist geringer als die kombinierte Menge an Speicherplatz, da ein Teil des Speicherplatzes für die Parität benötigt wird. |
| Festplatte =`<n>,<n>,<n>[,<n>,...]` | Die dynamischen Datenträger, auf denen das RAID-5-Volume erstellt werden soll. Zum Erstellen eines RAID-5-Volumes benötigen Sie mindestens drei dynamische Datenträger. Eine Menge an Speicherplatz, der gleich `size=<n>` ist, wird auf jedem Datenträger zugeordnet. |
| ausrichten =`<n>` | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit den Hardware-RAID-Arrays der logischen Gerätenummer verwendet, um die Leistung zu verbessern. `<n>` die Anzahl der Kilobyte (KB) vom Anfang des Datenträgers bis zur nächsten Ausrichtungs Grenze. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein RAID-5-Volume mit einer Größe von 1000 Megabyte zu erstellen, indem Sie die Datenträger 1, 2 und 3 verwenden:

```
create volume raid size=1000 disk=1,2,3
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)
