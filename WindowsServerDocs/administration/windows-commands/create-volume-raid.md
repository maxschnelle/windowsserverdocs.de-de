---
title: Erstellen eines Volume-RAID
description: Referenz Thema für Create Volume RAID, mit dem ein RAID-5-Volume mit drei oder mehr angegebenen dynamischen Datenträgern erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9f257950-9240-4d5f-9537-8ad653d48ebf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 15a165439d0b19023fa5270eb372a17af8d558a4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716933"
---
# <a name="create-volume-raid"></a>Erstellen eines Volume-RAID

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt ein RAID-5-Volume mit drei oder mehr angegebenen dynamischen Datenträgern.  

> [!IMPORTANT]  
> Dieser Diskpart-Befehl ist in keiner Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax  
  
```  
create volume raid [size=<n>] disk=<n>,<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|           Parameter           |                                                                                                                                                                                                                                              BESCHREIBUNG                                                                                                                                                                                                                                              |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           Größe\=<n>           | Die Menge des Speicherplatzes (in Megabyte \(MB\)), die das Volume auf den einzelnen Datenträgern einnimmt. Wenn keine Größe angegeben wird, wird das größtmögliche RAID\-5-Volume erstellt. Der Datenträger mit dem kleinsten verfügbaren verfügbaren freien Speicherplatz bestimmt die Größe für\-das RAID 5-Volume, und der Speicherplatz wird von jedem Datenträger zugeordnet. Die tatsächliche Menge an nutzbarem Speicherplatz auf dem\-RAID 5-Volume ist geringer als die kombinierte Menge an Speicherplatz, da ein Teil des Speicherplatzes für die Parität benötigt wird. |
| fest\=<n>Platte<n>,<n>\[,<n>,,...\] |                                                                                                                                               Die dynamischen Datenträger, auf denen das RAID\-5-Volume erstellt werden soll. Sie benötigen mindestens drei dynamische Datenträger, um ein RAID\-5-Volume zu erstellen. Der Größe des Speicherplatzes, der gleich der **Größe\= ** ist, wird auf jedem Datenträger zugeordnet.                                                                                                                                                |
|          abzustimmen\=<n>           |                                                                                                                   Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit Hardware-RAID \(-LUN\) -Arrays für die logische Gerätenummer verwendet der *Wert für die* Anzahl der \(KB\) liegt zwischen dem Anfang des Datenträgers und der nächstgelegenen Ausrichtungs Grenze.                                                                                                                   |
|             Noerr             |                                                                                                                                                 nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                                                                                                                                  |
  
## <a name="remarks"></a>Bemerkungen  
  
-   Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.  
  
## <a name="examples"></a>Beispiele  
Geben Sie Folgendes ein\-, um ein RAID 5-Volume mit einer Größe von 1000 Megabyte zu erstellen, indem Sie die Datenträger 1, 2 und 3 verwenden:  
  
```  
create volume raid size=1000 disk=1,2,3  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

