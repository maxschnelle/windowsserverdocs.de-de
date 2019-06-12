---
title: Erstellen von Volume-Spiegelung
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 72d80fdf6eca1262a858cbe2a98ed8c9c421bff6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434079"
---
# <a name="create-volume-mirror"></a>Erstellen von Volume-Spiegelung

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

erstellt eine Spiegelung Volumes mit den zwei angegebenen dynamischen Datenträgern.  
  
> [!NOTE]  
> Dieser Befehl ist nur in Windows 7 und Windows Server 2008 R2 verfügbar.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|         Parameter         |                                                                                                                                     Beschreibung                                                                                                                                     |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Größe\=<n>         |                 Gibt die Menge des Speicherplatzes in Megabyte \(MB\), die das Volume auf jedem Datenträger belegen wird. Wenn keine Größe angegeben wird, beansprucht das neue Volume der verbleibende freie Speicherplatz auf der kleinste Datenträger und gleich viel Speicherplatz auf jedem nachfolgenden Datenträger ab.                 |
| Datenträger\=<n>,<n>\[,<n>,...\] |                       Gibt an, den dynamischen Datenträgern auf denen das Volume erstellt wird. Sie benötigen zwei dynamische Datenträger, um ein Volume für die Spiegelung zu erstellen. Der Speicherplatz, der gleich der Größe, die mit angegebenen die **Größe** Parameter wird auf jedem Datenträger zugeordnet.                        |
|        align\=<n>         | Richtet alle Volume-Blöcke auf der nächsten. Dieser Parameter wird in der Regel verwendet, mit der Hardware-RAID, logische Gerätenummer \(LUN\) Arrays zur Verbesserung der Leistung. *n* ist die Anzahl der Kilobytes \(KB\) vom Anfang des Datenträgers an, die am nächsten Ausrichtungsgrenze. |
|           Diskpart           |                                        Nur für Skripting verwendet. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit einem Fehler beendet.                                         |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wechselt der Fokus automatisch auf das neue Volume.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Geben Sie Folgendes ein, um ein gespiegeltes Volume von 1000 MB Größe auf Datenträger 1 und 2 zu erstellen:  
  
```  
create volume mirror size=1000 disk=1,2  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

