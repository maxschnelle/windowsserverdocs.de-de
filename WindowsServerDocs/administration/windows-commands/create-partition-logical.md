---
title: logische Partition erstellen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f59b79a-d690-4d0e-ad38-40df5a0ce38e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4f18048272eda710f7cb53a631ddeda81784a56b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378892"
---
# <a name="create-partition-logical"></a>logische Partition erstellen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erstellt eine logische Partition in einer vorhandenen erweiterten Partition. Sie können diesen Befehl nur auf Master Boot Record \(mbr @ no__t-1-Datenträgern verwenden.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create partition logical [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                                                                                                                                                       Beschreibung                                                                                                                                                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Size @ no__t-0 @ no__t-1  |                                                                                                              Gibt die Größe der logischen Partition in Megabyte \(MB @ no__t-1 an, die kleiner als die erweiterte Partition sein muss. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis der freie Speicherplatz in der erweiterten Partition nicht mehr verfügbar ist.                                                                                                               |
| Offset @ no__t-0 @ no__t-1 | Gibt den Offset in Kilobyte \(KB @ no__t-1 an, bei dem die Partition erstellt wird. Der Offset wird aufgerundet, um die verwendete Zylinder Größe vollständig auszufüllen. Wenn kein Offset angegeben wird, wird die Partition in den ersten Datenträger Block eingefügt, der groß genug ist, um Sie zu speichern. Die Partition ist mindestens so lang wie die Zahl, die durch die **Größe @ no__t-1 @ no__t-2**angegeben wird. Wenn Sie eine Größe für die logische Partition angeben, muss sie kleiner als die erweiterte Partition sein. |
| align @ no__t-0 @ no__t-1  |                                                                                     Richtet alle Volumes oder Partitions Blöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit der Hardware-RAID-Nummer \(lun @ no__t-1 verwendet, um die Leistung zu verbessern.  <n> ist die Anzahl der Kilobyte \( KB @ no__t-2 vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze.                                                                                      |
|    Noerr    |                                                                                                                           Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                                                                                                           |
  
## <a name="remarks"></a>Hinweise  
  
-   Wenn die Parameter " **size** " und " **Offset** " nicht angegeben werden, wird die logische Partition in dem größten Datenträger Block erstellt, der in der erweiterten Partition verfügbar ist.  
  
-   Nachdem die Partition erstellt wurde, wird der Fokus automatisch auf die neue logische Partition verlagert.  
  
-   Ein einfacher MBR-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie in der erweiterten Partition des ausgewählten Datenträgers Folgendes ein, um eine logische Partition mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create partition logical size=1000  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

