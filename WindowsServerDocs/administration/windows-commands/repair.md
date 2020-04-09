---
title: Reparatur
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46b98938394c10e31d4999ff0e060e10f7da9bdc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835933"
---
# <a name="repair"></a>Reparatur

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

repariert das RAID\-5-Volume mit dem Fokus, indem der fehlerhafte Datenträger Bereich durch den angegebenen dynamischen Datenträger ersetzt wird.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
repair disk=<n> [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
| Parameter  |                                                                                             Beschreibung                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Datenträger\=<n>  |                                                                 Gibt den dynamischen Datenträger an, durch den der fehlerhafte Datenträger Bereich ersetzt wird.                                                                 |
| \=<n> ausrichten |          Richtet alle Volumes oder Partitions Blöcke an der nächstgelegenen Ausrichtungs Grenze aus. " *n* " ist die Anzahl der Kilobyte \(KB\) vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze.           |
|   Noerr    | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |
  
## <a name="remarks"></a>Hinweise  
  
-   Der angegebene dynamische Datenträger muss über einen freien Speicherplatz verfügen, der größer oder gleich der Gesamtgröße des fehlerhaften Datenträger Bereichs im RAID-\-5-Volume ist.  
  
-   Ein Volume in einem RAID-\-5-Array muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Wenn Sie das Volume durch einen dynamischen Datenträger 4 ersetzen möchten, geben Sie Folgendes ein:  
  
```  
repair disk=4  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

