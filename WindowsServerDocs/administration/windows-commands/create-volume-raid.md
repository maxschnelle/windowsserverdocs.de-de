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

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erstellt ein RAID\-5-Volume mit drei oder mehr angegebenen dynamischen Datenträgern.  
  
> [!IMPORTANT]  
> Dieser Diskpart-Befehl ist in keiner Edition von Windows Vista verfügbar.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create volume raid [size=<n>] disk=<n>,<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|           Parameter           |                                                                                                                                                                                                                                              Beschreibung                                                                                                                                                                                                                                              |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           Größe\=<n>           | Der Speicherplatz in Megabyte \(MB\), den das Volume auf den einzelnen Datenträgern einnimmt. Wenn keine Größe angegeben wird, wird das größte mögliche RAID-\-5 Volume erstellt. Der Datenträger mit dem kleinsten verfügbaren verfügbaren freien Speicherplatz bestimmt die Größe für das RAID-\-5 Volume, und der Speicherplatz wird von jedem Datenträger zugeordnet. Die tatsächliche Menge an nutzbarem Speicherplatz im RAID-\-5 Volume ist geringer als die kombinierte Menge an Speicherplatz, da ein Teil des Speicherplatzes für die Parität benötigt wird. |
| Datenträger\=<n>,<n>,<n>\[,<n>,...\] |                                                                                                                                               Die dynamischen Datenträger, auf denen das RAID\-5-Volume erstellt werden soll. Sie benötigen mindestens drei dynamische Datenträger, um ein RAID-\-5-Volume zu erstellen. Ein Speicherplatz gleich der **Größe\=<n>** auf jedem Datenträger zugeordnet ist.                                                                                                                                                |
|          \=<n> ausrichten           |                                                                                                                   Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit der logischen Gerätenummer des Hardware-RAID-\(LUN\) Arrays verwendet, um die Leistung " *n* " ist die Anzahl der Kilobyte \(KB\) vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze.                                                                                                                   |
|             Noerr             |                                                                                                                                                 nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                                                                                                                                  |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie Folgendes ein, um ein RAID\-5-Volume mit einer Größe von 1000 Megabyte zu erstellen. verwenden Sie dazu die Datenträger 1, 2 und 3:  
  
```  
create volume raid size=1000 disk=1,2,3  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

