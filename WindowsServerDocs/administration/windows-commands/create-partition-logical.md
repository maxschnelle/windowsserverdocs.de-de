---
title: Erstellen Sie eine logische partition
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d3af60aed6c8305e410c6ebfba3cf2e006034ad7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434151"
---
# <a name="create-partition-logical"></a>Erstellen Sie eine logische partition

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

erstellt eine logische Partition in einer vorhandenen erweiterten Partition an. Sie können diesen Befehl nur verwenden, auf den master Boot Records \(MBR\) Datenträger.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create partition logical [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                                                                                                                                                       Beschreibung                                                                                                                                                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Größe\=<n>  |                                                                                                              Gibt die Größe der logischen Partition in Megabytes \(MB\), die kleiner als der erweiterten Partition sein muss. Wenn keine Größe angegeben wird, wird die Partition erst in der erweiterten Partition nicht mehr Speicherplatz verfügbar ist.                                                                                                               |
| offset\=<n> | Gibt den Offset in Kilobyte \(KB\), an dem die Partition erstellt wird. Der Offset wird aufgerundet, vollständig ausgefüllt verwendete ist. Wird kein Offset angegeben wird, wird die Partition in der ersten Datenträgerbereich platziert, die groß genug für die sie enthalten ist. Die Partition ist als die angegebene Anzahl mindestens so lange in Byte **Größe\=<n>** . Wenn Sie eine Größe für die logische Partition angeben, muss er kleiner als der erweiterten Partition sein. |
| align\=<n>  |                                                                                     Richtet alle Volumes oder einer Partition Blöcke auf der nächsten. In der Regel verwendet, mit der Hardware-RAID Logical Unit Number \(LUN\) Arrays zur Verbesserung der Leistung.  <n> ist die Anzahl der Kilobytes \(KB\) vom Anfang des Datenträgers an, die am nächsten Ausrichtungsgrenze.                                                                                      |
|    Diskpart    |                                                                                                                           nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.                                                                                                                           |
  
## <a name="remarks"></a>Hinweise  
  
-   Wenn die **Größe** und **Offset** Parameter nicht angegeben werden, die logische Partition wird erstellt, in dem größten Datenträgerbereich, die in der erweiterten Partition verfügbar.  
  
-   Nachdem Sie die Partition erstellt wurde, wechselt der Fokus automatisch auf die neue logische Partition.  
  
-   Ein grundlegende MBR-Datenträger muss ausgewählt werden, für diesen Vorgang erfolgreich ausgeführt werden kann. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Geben Sie Folgendes ein, um eine logische Partition 1000 MB Größe, in der erweiterten Partition des ausgewählten Datenträgers zu erstellen:  
  
```  
create partition logical size=1000  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

