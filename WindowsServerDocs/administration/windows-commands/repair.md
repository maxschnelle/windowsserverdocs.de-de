---
title: Reparieren
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e9afb6c418558078496871b71bfaff706753b0a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936761"
---
# <a name="repair"></a>Reparieren

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

repariert das RAID \- 5-Volume mit dem Fokus, indem der fehlerhafte Datenträger Bereich durch die angegebene dynamische Festplatte ersetzt wird.



## <a name="syntax"></a>Syntax

```
repair disk=<n> [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter  |                                                                                             Beschreibung                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Diskette\=<n>  |                                                                 Gibt den dynamischen Datenträger an, durch den der fehlerhafte Datenträger Bereich ersetzt wird.                                                                 |
| abzustimmen\=<n> |          Richtet alle Volumes oder Partitions Blöcke an der nächstgelegenen Ausrichtungs Grenze aus. der *Wert für die* Anzahl der \( KB liegt \) zwischen dem Anfang des Datenträgers und der nächstgelegenen Ausrichtungs Grenze.           |
|   Noerr    | nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="remarks"></a>Hinweise

-   Der angegebene dynamische Datenträger muss über einen freien Speicherplatz verfügen, der größer oder gleich der Gesamtgröße des fehlerhaften Datenträger Bereichs auf dem RAID \- 5-Volume ist.

-   Ein Volume in einem RAID \- 5-Array muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.

## <a name="examples"></a>Beispiele
Wenn Sie das Volume durch einen dynamischen Datenträger 4 ersetzen möchten, geben Sie Folgendes ein:

```
repair disk=4
```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)




