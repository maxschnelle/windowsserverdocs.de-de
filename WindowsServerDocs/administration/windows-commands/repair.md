---
title: Reparieren
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 89c09608e64b408db9c7c79269046195e005c187
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722393"
---
# <a name="repair"></a>Reparieren

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

repariert das RAID\-5-Volume mit dem Fokus, indem der fehlerhafte Datenträger Bereich durch die angegebene dynamische Festplatte ersetzt wird.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
repair disk=<n> [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
| Parameter  |                                                                                             BESCHREIBUNG                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Diskette\=<n>  |                                                                 Gibt den dynamischen Datenträger an, durch den der fehlerhafte Datenträger Bereich ersetzt wird.                                                                 |
| abzustimmen\=<n> |          Richtet alle Volumes oder Partitions Blöcke an der nächstgelegenen Ausrichtungs Grenze aus. der *Wert für die* Anzahl der \(KB\) liegt zwischen dem Anfang des Datenträgers und der nächstgelegenen Ausrichtungs Grenze.           |
|   Noerr    | nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |
  
## <a name="remarks"></a>Bemerkungen  
  
-   Der angegebene dynamische Datenträger muss über einen freien Speicherplatz verfügen, der größer oder gleich der Gesamtgröße des fehlerhaften Daten\-Träger Bereichs auf dem RAID 5-Volume ist.  
  
-   Ein Volume in einem RAID\-5-Array muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.  
  
## <a name="examples"></a>Beispiele  
Wenn Sie das Volume durch einen dynamischen Datenträger 4 ersetzen möchten, geben Sie Folgendes ein:  
  
```  
repair disk=4  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

