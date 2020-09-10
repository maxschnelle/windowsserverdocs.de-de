---
title: Reparieren
description: Referenz Artikel für den Repair-Befehl, mit dem RAID-5-Volumes repariert werden, indem der fehlerhafte Datenträger Bereich durch einen angegebenen dynamischen Datenträger ersetzt wird.
ms.topic: reference
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 969a677f72af9ab5e99770983308db6e88c28c29
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89641000"
---
# <a name="repair"></a>Reparieren

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Repariert das RAID-5-Volume mit dem Fokus, indem der fehlerhafte Datenträger Bereich durch die angegebene dynamische Festplatte ersetzt wird.

Ein Volume in einem RAID-5-Array muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.

## <a name="syntax"></a>Syntax

```
repair disk=<n> [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Festplatte =`<n>` | Gibt den dynamischen Datenträger an, durch den der fehlerhafte Datenträger Bereich ersetzt wird. Dabei muss *n* über einen freien Speicherplatz verfügen, der größer oder gleich der Gesamtgröße des fehlerhaften Datenträger Bereichs im RAID-5-Volume ist. |
| ausrichten =`<n>` | Richtet alle Volumes oder Partitions Blöcke an der nächstgelegenen Ausrichtungs Grenze aus. Dabei steht *n* für die Anzahl der Kilobyte (KB) vom Anfang des Datenträgers bis zur nächsten Ausrichtungs Grenze. |
| Noerr | nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

### <a name="examples"></a>Beispiele

Wenn Sie das Volume durch einen dynamischen Datenträger 4 ersetzen möchten, geben Sie Folgendes ein:

```
repair disk=4
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Volume auswählen"](select-volume.md)