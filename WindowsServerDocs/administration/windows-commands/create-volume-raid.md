---
title: Erstellen eines Volume-RAID
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f257950-9240-4d5f-9537-8ad653d48ebf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a3c13cb5b78ae3e771b461a35a7130a48e7ec01
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378862"
---
# <a name="create-volume-raid"></a>Erstellen eines Volume-RAID

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erstellt ein RAID @ no__t-05-Volume mit drei oder mehr angegebenen dynamischen Datenträgern.  
  
> [!IMPORTANT]  
> Dieser Diskpart-Befehl ist in keiner Edition von Windows Vista verfügbar.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create volume raid [size=<n>] disk=<n>,<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|           Parameter           |                                                                                                                                                                                                                                              Beschreibung                                                                                                                                                                                                                                              |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           Size @ no__t-0 @ no__t-1           | Der Speicherplatz in Megabyte \(MB @ no__t-1, den das Volume auf den einzelnen Datenträgern einnimmt. Wenn keine Größe angegeben wird, wird das größtmögliche RAID @ no__t-05-Volume erstellt. Der Datenträger mit dem kleinsten verfügbaren, verfügbaren freien Speicherplatz bestimmt die Größe des RAID @ no__t-05-Volumes, und der Speicherplatz wird von jedem Datenträger zugeordnet. Die tatsächliche Menge an nutzbarem Speicherplatz im RAID @ no__t-05-Volume ist geringer als die kombinierte Menge an Speicherplatz, da ein Teil des Speicherplatzes für die Parität benötigt wird. |
| Disk @ no__t-0 @ no__t-1, <n>, <n> @ no__t-4, <n>,... \] |                                                                                                                                               Die dynamischen Datenträger, auf denen das RAID @ no__t-05-Volume erstellt werden soll. Zum Erstellen eines RAID @ no__t-05-Volumes benötigen Sie mindestens drei dynamische Datenträger. Auf jedem Datenträger ist eine Menge an Speicherplatz gleich " **size @ no__t-1 @ no__t-2** " zugeordnet.                                                                                                                                                |
|          align @ no__t-0 @ no__t-1           |                                                                                                                   Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit der Hardware-RAID-Nummer \(lun @ no__t-1 verwendet, um die Leistung zu verbessern. *n* ist die Anzahl der Kilobyte \( KB @ no__t-2 vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze.                                                                                                                   |
|             Noerr             |                                                                                                                                                 Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                                                                                                                                  |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie Folgendes ein, um ein RAID @ no__t-05-Volume mit einer Größe von 1000 Megabyte zu erstellen, indem Sie die Datenträger 1, 2 und 3 verwenden:  
  
```  
create volume raid size=1000 disk=1,2,3  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

