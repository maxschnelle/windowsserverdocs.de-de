---
title: Erstellen einer Partition erweitert
description: Referenz Thema für Create Partition Extended, das eine erweiterte Partition auf dem Datenträger mit Fokus erstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4ad7cb66-9c66-4153-b94e-1030a7225070
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b8af7247a9084b722f5b510df1d6af4622fc4ac2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719248"
---
# <a name="create-partition-extended"></a>Erstellen einer Partition erweitert

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine erweiterte Partition auf dem Datenträger mit dem Fokus. Sie können diesen Befehl nur auf MBR-Datenträgern (Master Boot Record) verwenden.

## <a name="syntax"></a>Syntax  
  
```  
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                                                             BESCHREIBUNG                                                                                                                              |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Größe\=<n>  |                                                  Gibt die Größe der Partition in Megabyte \(MB\)an. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis der freie Speicherplatz in der erweiterten Partition nicht mehr verfügbar ist.                                                  |
| kompensieren\=<n> |                     Gibt den Offset in Kilobyte \(KB\)an, bei dem die Partition erstellt wird. Wenn kein Offset angegeben wird, wird die Partition am Anfang des freien Speicherplatzes auf dem Datenträger gestartet, der groß genug ist, um die neue Partition zu speichern.                      |
| abzustimmen\=<n>  | Richtet alle Partitions Blöcke an die nächstgelegene Ausrichtungs Grenze aus. Wird in der Regel mit Hardware-RAID \(-LUN\) -Arrays für die logische Gerätenummer verwendet <n>die Anzahl von Kilobyte \((KB\) ) zwischen dem Anfang des Datenträgers und der nächstgelegenen Ausrichtungs Grenze. |
|    Noerr    |                                 nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                 |
  
## <a name="remarks"></a>Bemerkungen  
  
-   Nachdem die Partition erstellt wurde, wird der Fokus automatisch auf die neue Partition verlagert.  
  
-   Pro Datenträger kann nur eine erweiterte Partition erstellt werden.  
  
-   Dieser Befehl schlägt fehl, wenn Sie versuchen, eine erweiterte Partition innerhalb einer anderen erweiterten Partition zu erstellen.  
  
-   Sie müssen eine erweiterte Partition erstellen, bevor Sie logische Laufwerke erstellen können.  
  
-   Ein einfacher MBR-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.  
  
## <a name="examples"></a>Beispiele  
Geben Sie Folgendes ein, um eine erweiterte Partition mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create partition extended size=1000  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

