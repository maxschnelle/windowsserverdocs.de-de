---
title: volumespiegelung erstellen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72ecc4e0ede163857c47c5b7013aacdd49719ac8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378868"
---
# <a name="create-volume-mirror"></a>volumespiegelung erstellen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erstellt eine volumespiegelung mithilfe der beiden angegebenen dynamischen Datenträger.  
  
> [!NOTE]  
> Dieser Befehl ist nur in Windows 7 und Windows Server 2008 R2 verfügbar.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|         Parameter         |                                                                                                                                     Beschreibung                                                                                                                                     |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Size @ no__t-0 @ no__t-1         |                 Gibt die Größe des Speicherplatzes in Megabyte \(MB @ no__t-1 an, die das Volume auf den einzelnen Datenträgern einnimmt. Wenn keine Größe angegeben ist, nimmt das neue Volume den verbleibenden freien Speicherplatz auf dem kleinsten Datenträger und den gleichen Speicherplatz auf jedem nachfolgenden Datenträger an.                 |
| Disk @ no__t-0 @ no__t-1, <n> @ no__t-3, <n>,... \] |                       Gibt die dynamischen Datenträger an, auf denen das Spiegelungs Volume erstellt wird. Zum Erstellen eines Spiegelungs Volumes benötigen Sie zwei dynamische Datenträger. Eine Menge an Speicherplatz, die der Größe entspricht, die mit dem **size** -Parameter angegeben wird, wird auf jedem Datenträger zugeordnet.                        |
|        align @ no__t-0 @ no__t-1         | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Dieser Parameter wird in der Regel mit der \(lun @ no__t-1-Arrays der Hardware-RAID-Einheit verwendet, um die Leistung zu verbessern. *n* ist die Anzahl der Kilobyte \( KB @ no__t-2 vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze. |
|           Noerr           |                                        Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehler beendet wird.                                         |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie auf den Datenträgern 1 und 2 Folgendes ein, um ein gespiegeltes Volume mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create volume mirror size=1000 disk=1,2  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

