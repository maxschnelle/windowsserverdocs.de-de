---
title: shrink
description: Referenz Artikel zum Verkleinern von Diskpart, wodurch die Größe des ausgewählten Volumes um den von Ihnen angegebenen Betrag verringert wird.
ms.topic: article
ms.assetid: ec87cc7c-9846-465e-a10d-4ee10db4f4e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ccae64b5f54c197f8eb1cd684a74c44945b3d069
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882382"
---
# <a name="shrink"></a>shrink

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der DiskPart-Verkleinerungs Befehl reduziert die Größe des ausgewählten Volumes um den von Ihnen angegebenen Betrag. Mit diesem Befehl wird freier Speicherplatz aus dem nicht verwendeten Speicherplatz am Ende des Volumes bereitgestellt.

## <a name="syntax"></a>Syntax
```
shrink [desired=<n>] [minimum=<n>] [nowait] [noerr]
shrink querymax [noerr]
```
### <a name="parameters"></a>Parameter

|  Parameter  |                                                                                             BESCHREIBUNG                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| gewünscht =<n> |                                                     Gibt die gewünschte Menge an Speicherplatz in Megabyte (MB) an, um die Größe des Volumes um zu verringern.                                                     |
| minimal =<n> |                                                           Gibt den minimalen Speicherplatz in MB an, um die Größe des Volumes zu verringern.                                                           |
|  querymax   |                       Gibt den maximalen Speicherplatz in MB zurück, um den das Volume reduziert werden kann. Dieser Wert kann sich ändern, wenn Anwendungen derzeit auf das Volume zugreifen.                        |
|   nowait    |                                                       erzwingt, dass der Befehl sofort zurückgegeben wird, während der Verkleinerungs Prozess noch ausgeführt wird.                                                        |
|    Noerr    | nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="remarks"></a>Bemerkungen
- Sie können die Größe eines Volumes nur verringern, wenn er mit dem NTFS-Dateisystem formatiert ist oder wenn kein Dateisystem vorhanden ist.
- Dieser Befehl funktioniert auf grundlegenden Volumes und auf einfachen oder übergreifenden dynamischen Volumes.
- Wenn ein gewünschter Betrag nicht angegeben wird, wird das Volume um den minimalen Betrag (sofern angegeben) reduziert.
- Wenn ein Minimalwert nicht angegeben wird, wird das Volume um den gewünschten Betrag (falls angegeben) reduziert.
- Wenn weder ein Minimalbetrag noch ein gewünschter Betrag angegeben ist, wird das Volume so weit wie möglich reduziert.
- Wenn ein Minimalwert angegeben ist, aber nicht genügend freier Speicherplatz verfügbar ist, schlägt der Befehl fehl.
- Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.
- Dieser Befehl funktioniert nicht für OEM-Partitionen (Original Equipment Manufacturer), Extensible Firmware Interface (EFI)-Systempartitionen oder Wiederherstellungs Partitionen.
  ## <a name="examples"></a>Beispiele
  Geben Sie Folgendes ein, um die Größe des ausgewählten Volumes um die größtmögliche Größe zwischen 250 und 500 Megabyte zu verringern:
  ```
  shrink desired=500 minimum=250
  ```
  Geben Sie Folgendes ein, um die maximale Anzahl von MB anzuzeigen, um die das Volume durch reduziert werden kann:
  ```
  shrink querymax
  ```

[Resize-Partition](/powershell/module/storage/resize-partition?view=win10-ps)
