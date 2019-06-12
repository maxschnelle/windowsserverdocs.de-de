---
title: Erstellen von Volume stripe
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 20dce735-5f7c-4f83-a580-d087e2913a00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55ed731df4613e215fb4d0954a5b8424035b1166
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434005"
---
# <a name="create-volume-stripe"></a>Erstellen von Volume stripe

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

erstellt ein Stripesetvolume mit zwei oder mehr angegebenen dynamischen Datenträgern.  
  
> [!IMPORTANT]  
> für Windows Vista ist dieser DiskPart-Befehl nur in der Windows Vista Ultimate, Windows Vista Enterprise und Windows Vista Business Edition verfügbar.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create volume stripe [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|         Parameter         |                                                                                                                            Beschreibung                                                                                                                            |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Größe\=<n>         |             Die Menge des Speicherplatzes in Megabyte \(MB\), die das Volume auf jedem Datenträger belegen wird. Wenn keine Größe angegeben wird, beansprucht das neue Volume der verbleibende freie Speicherplatz auf der kleinste Datenträger und gleich viel Speicherplatz auf jedem nachfolgenden Datenträger ab.             |
| Datenträger\=<n>,<n>\[,<n>,...\] |                                  Die dynamischen Datenträger, auf denen Stripesetvolume erstellt wird. Sie benötigen mindestens zwei dynamische Datenträger ein Stripesetvolume erstellen. Der Platz gleich **Größe\= <n>**  auf jedem Datenträger zugeordnet ist.                                   |
|        align\=<n>         | Richtet alle Volume-Blöcke auf der nächsten. In der Regel verwendet, mit der Hardware-RAID Logical Unit Number \(LUN\) Arrays zur Verbesserung der Leistung. *n* ist die Anzahl der Kilobytes \(KB\) vom Anfang des Datenträgers an, die am nächsten Ausrichtungsgrenze. |
|           Diskpart           |                               nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.                                |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wechselt der Fokus automatisch auf das neue Volume.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Geben Sie Folgendes ein, um ein Stripesetvolume von 1000 MB Größe auf Datenträger 1 und 2 zu erstellen:  
  
```  
create volume stripe size=1000 disk=1,2  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

