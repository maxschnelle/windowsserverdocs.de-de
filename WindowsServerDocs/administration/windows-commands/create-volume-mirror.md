---
title: volumespiegelung erstellen
description: Referenz Thema zum Erstellen einer volumespiegelung, das eine volumespiegelung mithilfe der beiden angegebenen dynamischen Datenträger erstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eda0a6d799fc88c8382e128df1bd260b9e9426b7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716948"
---
# <a name="create-volume-mirror"></a>volumespiegelung erstellen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine volumespiegelung mithilfe der beiden angegebenen dynamischen Datenträger.  
  
> [!NOTE]  
> Dieser Befehl ist nur in Windows 7 und Windows Server 2008 R2 verfügbar.

## <a name="syntax"></a>Syntax  
  
```  
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|         Parameter         |                                                                                                                                     BESCHREIBUNG                                                                                                                                     |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Größe\=<n>         |                 Gibt die Größe des Speicherplatzes in Megabyte ( \(MB\)) an, die das Volume auf den einzelnen Datenträgern einnimmt. Wenn keine Größe angegeben ist, nimmt das neue Volume den verbleibenden freien Speicherplatz auf dem kleinsten Datenträger und den gleichen Speicherplatz auf jedem nachfolgenden Datenträger an.                 |
| fest\=<n>Platte<n>\[,<n>,,...\] |                       Gibt die dynamischen Datenträger an, auf denen das Spiegelungs Volume erstellt wird. Zum Erstellen eines Spiegelungs Volumes benötigen Sie zwei dynamische Datenträger. Eine Menge an Speicherplatz, die der Größe entspricht, die mit dem **size** -Parameter angegeben wird, wird auf jedem Datenträger zugeordnet.                        |
|        abzustimmen\=<n>         | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Dieser Parameter wird in der Regel mit der Hardware-RAID \(-LUN\) -Arrays der logischen Gerätenummer verwendet, um die Leistung der *Wert für die* Anzahl der \(KB\) liegt zwischen dem Anfang des Datenträgers und der nächstgelegenen Ausrichtungs Grenze. |
|           Noerr           |                                        Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehler beendet wird.                                         |
  
## <a name="remarks"></a>Bemerkungen  
  
-   Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.  
  
## <a name="examples"></a>Beispiele  
Geben Sie auf den Datenträgern 1 und 2 Folgendes ein, um ein gespiegeltes Volume mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create volume mirror size=1000 disk=1,2  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

