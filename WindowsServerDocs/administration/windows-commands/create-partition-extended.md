---
title: Erstellen Sie erweiterte partition
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: aa8d556822bc6caf4277812be818a0cf456e75dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818881"
---
# <a name="create-partition-extended"></a>Erstellen Sie erweiterte partition

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

erstellt eine erweiterte Partition auf dem Datenträger mit dem Fokus. Sie können diesen Befehl verwenden, nur auf den Master Boot Record \(MBR\) Datenträger.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Größe\=<n>|Gibt die Größe der Partition in Megabytes \(MB\). Wenn keine Größe angegeben wird, wird die Partition erst in der erweiterten Partition nicht mehr Speicherplatz verfügbar ist.|  
|offset\=<n>|Gibt den Offset in Kilobyte \(KB\), an dem die Partition erstellt wird. Wenn kein Offset angegeben wird, startet die Partition am Anfang des freien Speicherplatzes auf dem Datenträger, die groß genug zum Speichern der neuen Partition ist.|  
|align\=<n>|Richtet alle Partition Blöcke auf der nächsten. In der Regel verwendet, mit der Hardware-RAID Logical Unit Number \(LUN\) Arrays zur Verbesserung der Leistung. <n> ist die Anzahl der Kilobytes \(KB\) vom Anfang des Datenträgers an, die am nächsten Ausrichtungsgrenze.|  
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie die Partition erstellt wurde, wechselt der Fokus automatisch auf die neue Partition.  
  
-   Pro Datenträger kann nur eine erweiterte Partition erstellt werden.  
  
-   Dieser Befehl schlägt fehl, wenn Sie versuchen, eine erweiterte Partition in einer anderen erweiterten Partition zu erstellen.  
  
-   Sie müssen eine erweiterte Partition erstellen, bevor Sie logische Laufwerke erstellen können.  
  
-   Ein grundlegende MBR-Datenträger muss ausgewählt werden, für diesen Vorgang erfolgreich ausgeführt werden kann. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Um eine erweiterte Partition von 1000 MB Größe zu erstellen, geben Sie Folgendes ein:  
  
```  
create partition extended size=1000  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

