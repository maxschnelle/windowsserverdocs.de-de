---
title: Erstellen von Volume-raid
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 432d661d8c0ce4cae6fe08a2671e8f9d613ce351
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846781"
---
# <a name="create-volume-raid"></a>Erstellen von Volume-raid

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

erstellt eine RAID\-5-Volumes mit drei oder mehr angegebenen dynamische Datenträgern.  
  
> [!IMPORTANT]  
> Dieser DiskPart-Befehl ist nicht in jeder Edition von Windows Vista verfügbar.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create volume raid [size=<n>] disk=<n>,<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Größe\=<n>|Die Menge des Speicherplatzes in Megabyte \(MB\), die das Volume auf jedem Datenträger belegen wird. Wenn keine Größe angegeben wird, wird der größte mögliche RAID\-5-Volumes erstellt werden. Der Datenträger mit den kleinsten verfügbaren freien Speicherplatz bestimmt die Größe für RAID\-5-Volume und die gleiche Menge an Speicherplatz auf jedem Datenträger reserviert ist. Die tatsächliche Menge verwendbaren Speicherplatz in das RAID\-5-Volume ist kleiner als die Gesamtmenge des Speicherplatzes, da der Speicherplatz ist erforderlich, für die Parität.|  
|Datenträger\=<n>,<n>,<n>\[,<n>,...\]|Die dynamischen Datenträgern auf die Erstellung von RAID\-5-Volumes. Sie benötigen mindestens drei dynamische Datenträger aus, um erstellen Sie ein RAID\-5-Volumes. Der Platz gleich **Größe\= <n>**  auf jedem Datenträger zugeordnet ist.|  
|align\=<n>|Richtet alle Volume-Blöcke auf der nächsten. In der Regel verwendet, mit der Hardware-RAID Logical Unit Number \(LUN\) Arrays zur Verbesserung der Leistung. *n* ist die Anzahl der Kilobytes \(KB\) vom Anfang des Datenträgers an, die am nächsten Ausrichtungsgrenze.|  
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wechselt der Fokus automatisch auf das neue Volume.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Erstellen Sie eine RAID\-5-Volumes von 1000 MB groß, die mithilfe von Datenträgern, 1, 2 und 3, Typ:  
  
```  
create volume raid size=1000 disk=1,2,3  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

