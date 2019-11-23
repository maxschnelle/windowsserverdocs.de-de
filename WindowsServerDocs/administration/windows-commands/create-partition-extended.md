---
title: Erstellen einer Partition erweitert
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ad7cb66-9c66-4153-b94e-1030a7225070
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21620da46be0e1375f320172e7ccfe2edc338114
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378913"
---
# <a name="create-partition-extended"></a>Erstellen einer Partition erweitert

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erstellt eine erweiterte Partition auf dem Datenträger mit dem Fokus. Sie können diesen Befehl nur für die Master Boot Record-\(MBR\) Disks verwenden.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                                                             Beschreibung                                                                                                                              |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Größe\=<n>  |                                                  Gibt die Größe der Partition in Megabyte \(MB\)an. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis der freie Speicherplatz in der erweiterten Partition nicht mehr verfügbar ist.                                                  |
| Offset\=<n> |                     Gibt den Offset in Kilobyte \(KB-\)an, bei dem die Partition erstellt wird. Wenn kein Offset angegeben wird, wird die Partition am Anfang des freien Speicherplatzes auf dem Datenträger gestartet, der groß genug ist, um die neue Partition zu speichern.                      |
| \=<n> ausrichten  | Richtet alle Partitions Blöcke an die nächstgelegene Ausrichtungs Grenze aus. Wird in der Regel mit der logischen Gerätenummer des Hardware-RAID-\(LUN\) Arrays verwendet, um die Leistung <n> ist die Anzahl von Kilobyte \(KB\) vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze. |
|    Noerr    |                                 nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                 |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem die Partition erstellt wurde, wird der Fokus automatisch auf die neue Partition verlagert.  
  
-   Pro Datenträger kann nur eine erweiterte Partition erstellt werden.  
  
-   Dieser Befehl schlägt fehl, wenn Sie versuchen, eine erweiterte Partition innerhalb einer anderen erweiterten Partition zu erstellen.  
  
-   Sie müssen eine erweiterte Partition erstellen, bevor Sie logische Laufwerke erstellen können.  
  
-   Ein einfacher MBR-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie Folgendes ein, um eine erweiterte Partition mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create partition extended size=1000  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

