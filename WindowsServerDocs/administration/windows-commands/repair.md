---
title: Reparatur
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 88293422519488405d94e32596c81dbe4a697dee
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371531"
---
# <a name="repair"></a>Reparatur

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

repariert das RAID @ no__t-05-Volume mit dem Fokus, indem der fehlgeschlagene Datenträger Bereich durch den angegebenen dynamischen Datenträger ersetzt wird.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
repair disk=<n> [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
| Parameter  |                                                                                             Beschreibung                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Disk @ no__t-0 @ no__t-1  |                                                                 Gibt den dynamischen Datenträger an, durch den der fehlerhafte Datenträger Bereich ersetzt wird.                                                                 |
| align @ no__t-0 @ no__t-1 |          Richtet alle Volumes oder Partitions Blöcke an der nächstgelegenen Ausrichtungs Grenze aus. *n* ist die Anzahl der Kilobyte \( KB @ no__t-2 vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze.           |
|   Noerr    | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |
  
## <a name="remarks"></a>Hinweise  
  
-   Der angegebene dynamische Datenträger muss über einen freien Speicherplatz verfügen, der größer oder gleich der Gesamtgröße des fehlerhaften Datenträger Bereichs im RAID @ no__t-05-Volume ist.  
  
-   Ein Volume in einem RAID @ no__t-05-Array muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.  
  
## <a name="BKMK_examples"></a>Beispiele  
Wenn Sie das Volume durch einen dynamischen Datenträger 4 ersetzen möchten, geben Sie Folgendes ein:  
  
```  
repair disk=4  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

