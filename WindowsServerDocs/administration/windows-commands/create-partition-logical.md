---
title: logische Partition erstellen
description: Referenz Thema für Create Partition Logical, das eine logische Partition in einer vorhandenen erweiterten Partition erstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f59b79a-d690-4d0e-ad38-40df5a0ce38e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43d1c26d785fcecbb81a99c7484a15b3ea8b58a2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719232"
---
# <a name="create-partition-logical"></a>logische Partition erstellen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine logische Partition in einer vorhandenen erweiterten Partition. Sie können diesen Befehl nur auf Master Boot Record (MBR)-Datenträgern verwenden.

## <a name="syntax"></a>Syntax  
  
```  
create partition logical [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                                                                                                                                                       BESCHREIBUNG                                                                                                                                                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Größe\=<n>  |                                                                                                              Gibt die Größe der logischen Partition in Megabyte ( \(MB\)) an, die kleiner als die erweiterte Partition sein muss. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis der freie Speicherplatz in der erweiterten Partition nicht mehr verfügbar ist.                                                                                                               |
| kompensieren\=<n> | Gibt den Offset in Kilobyte \(KB\)an, bei dem die Partition erstellt wird. Der Offset wird aufgerundet, um die verwendete Zylinder Größe vollständig auszufüllen. Wenn kein Offset angegeben wird, wird die Partition in den ersten Datenträger Block eingefügt, der groß genug ist, um Sie zu speichern. Die Partition ist mindestens so lang wie die Zahl, die durch die **Größe\=** angegeben wird. Wenn Sie eine Größe für die logische Partition angeben, muss sie kleiner als die erweiterte Partition sein. |
| abzustimmen\=<n>  |                                                                                     Richtet alle Volumes oder Partitions Blöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit Hardware-RAID \(-LUN\) -Arrays für die logische Gerätenummer verwendet  <n>die Anzahl von Kilobyte \((KB\) ) zwischen dem Anfang des Datenträgers und der nächstgelegenen Ausrichtungs Grenze.                                                                                      |
|    Noerr    |                                                                                                                           nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                                                                                                           |
  
## <a name="remarks"></a>Bemerkungen  
  
-   Wenn die Parameter " **size** " und " **Offset** " nicht angegeben werden, wird die logische Partition in dem größten Datenträger Block erstellt, der in der erweiterten Partition verfügbar ist.  
  
-   Nachdem die Partition erstellt wurde, wird der Fokus automatisch auf die neue logische Partition verlagert.  
  
-   Ein einfacher MBR-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.  
  
## <a name="examples"></a>Beispiele  
Geben Sie in der erweiterten Partition des ausgewählten Datenträgers Folgendes ein, um eine logische Partition mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create partition logical size=1000  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

