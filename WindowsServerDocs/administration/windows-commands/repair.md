---
title: Reparieren
description: Referenz Artikel für * * * *-
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d646318b41881783e12b07da1c72d2a9cc31f853
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883769"
---
# <a name="repair"></a>Reparieren

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

repariert das RAID \- 5-Volume mit dem Fokus, indem der fehlerhafte Datenträger Bereich durch die angegebene dynamische Festplatte ersetzt wird.



## <a name="syntax"></a>Syntax

```
repair disk=<n> [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter  |                                                                                             BESCHREIBUNG                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Diskette\=<n>  |                                                                 Gibt den dynamischen Datenträger an, durch den der fehlerhafte Datenträger Bereich ersetzt wird.                                                                 |
| abzustimmen\=<n> |          Richtet alle Volumes oder Partitions Blöcke an der nächstgelegenen Ausrichtungs Grenze aus. der *Wert für die* Anzahl der \( KB liegt \) zwischen dem Anfang des Datenträgers und der nächstgelegenen Ausrichtungs Grenze.           |
|   Noerr    | nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="remarks"></a>Bemerkungen

-   Der angegebene dynamische Datenträger muss über einen freien Speicherplatz verfügen, der größer oder gleich der Gesamtgröße des fehlerhaften Datenträger Bereichs auf dem RAID \- 5-Volume ist.

-   Ein Volume in einem RAID \- 5-Array muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.

## <a name="examples"></a>Beispiele
Wenn Sie das Volume durch einen dynamischen Datenträger 4 ersetzen möchten, geben Sie Folgendes ein:

```
repair disk=4
```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)




