---
title: einfaches Volume erstellen
description: Referenz Thema für Create Volume Simple, mit dem ein einfaches Volume auf dem angegebenen dynamischen Datenträger erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f92bd9cf92dea258c6a49dd4cf75c4aae357c88e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716923"
---
# <a name="create-volume-simple"></a>einfaches Volume erstellen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt ein einfaches Volume auf dem angegebenen dynamischen Datenträger.  
  
> [!IMPORTANT]  
> für Windows Vista ist dieser Diskpart-Befehl nur in den Business Editionen Windows Vista Ultimate, Windows Vista Enterprise und Windows Vista verfügbar.
  
## <a name="syntax"></a>Syntax  
  
```  
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
| Parameter  |                                                                                                                            BESCHREIBUNG                                                                                                                            |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Größe\=<n>  |                                                                  Die Größe des Volumes in Megabyte ( \(MB\)). Wenn keine Größe angegeben wird, nimmt das neue Volume den verbleibenden freien Speicherplatz auf dem Datenträger an.                                                                   |
| Diskette\=<n>  |                                                                                Der dynamische Datenträger, auf dem das Volume erstellt wird. Wenn kein Datenträger angegeben ist, wird der aktuelle Datenträger verwendet.                                                                                |
| abzustimmen\=<n> | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit Hardware-RAID \(-LUN\) -Arrays für die logische Gerätenummer verwendet der *Wert für die* Anzahl der \(KB\) liegt zwischen dem Anfang des Datenträgers und der nächstgelegenen Ausrichtungs Grenze. |
|   Noerr    |                               nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                |
  
## <a name="remarks"></a>Bemerkungen  
  
-   Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.  
  
## <a name="examples"></a>Beispiele  
Geben Sie auf Datenträger 1 Folgendes ein, um ein Volume mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create volume simple size=1000 disk=1  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

