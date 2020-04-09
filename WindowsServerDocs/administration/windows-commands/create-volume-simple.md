---
title: einfaches Volume erstellen
description: Windows-Befehls Artikel zum Erstellen von Volume Simple, mit dem ein einfaches Volume auf dem angegebenen dynamischen Datenträger erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45c707a92692c5531a0e33c9537705558f2ac309
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846893"
---
# <a name="create-volume-simple"></a>einfaches Volume erstellen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt ein einfaches Volume auf dem angegebenen dynamischen Datenträger.  
  
> [!IMPORTANT]  
> für Windows Vista ist dieser Diskpart-Befehl nur in den Business Editionen Windows Vista Ultimate, Windows Vista Enterprise und Windows Vista verfügbar.
  
## <a name="syntax"></a>Syntax  
  
```  
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
| Parameter  |                                                                                                                            Beschreibung                                                                                                                            |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Größe\=<n>  |                                                                  Die Größe des Volumes in Megabyte \(MB\). Wenn keine Größe angegeben wird, nimmt das neue Volume den verbleibenden freien Speicherplatz auf dem Datenträger an.                                                                   |
| Datenträger\=<n>  |                                                                                Der dynamische Datenträger, auf dem das Volume erstellt wird. Wenn kein Datenträger angegeben ist, wird der aktuelle Datenträger verwendet.                                                                                |
| \=<n> ausrichten | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit der logischen Gerätenummer des Hardware-RAID-\(LUN\) Arrays verwendet, um die Leistung " *n* " ist die Anzahl der Kilobyte \(KB\) vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze. |
|   Noerr    |                               Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Geben Sie auf Datenträger 1 Folgendes ein, um ein Volume mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create volume simple size=1000 disk=1  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

