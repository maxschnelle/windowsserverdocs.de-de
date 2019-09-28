---
title: Verkleinern
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec87cc7c-9846-465e-a10d-4ee10db4f4e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0e5caa0103018c94671d7441a6d2349ab734be6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370900"
---
# <a name="shrink"></a>Verkleinern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der DiskPart-Verkleinerungs Befehl reduziert die Größe des ausgewählten Volumes um den von Ihnen angegebenen Betrag. Mit diesem Befehl wird freier Speicherplatz aus dem nicht verwendeten Speicherplatz am Ende des Volumes bereitgestellt.

## <a name="syntax"></a>Syntax
```
shrink [desired=<n>] [minimum=<n>] [nowait] [noerr]
shrink querymax [noerr]
```
## <a name="parameters"></a>Parameter

|  Parameter  |                                                                                             Beschreibung                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| erwünscht = <n> |                                                     Gibt die gewünschte Menge an Speicherplatz in Megabyte (MB) an, um die Größe des Volumes um zu verringern.                                                     |
| minimal = <n> |                                                           Gibt den minimalen Speicherplatz in MB an, um die Größe des Volumes zu verringern.                                                           |
|  querymax   |                       Gibt den maximalen Speicherplatz in MB zurück, um den das Volume reduziert werden kann. Dieser Wert kann sich ändern, wenn Anwendungen derzeit auf das Volume zugreifen.                        |
|   nowait    |                                                       erzwingt, dass der Befehl sofort zurückgegeben wird, während der Verkleinerungs Prozess noch ausgeführt wird.                                                        |
|    Noerr    | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="remarks"></a>Hinweise
- Sie können die Größe eines Volumes nur verringern, wenn er mit dem NTFS-Dateisystem formatiert ist oder wenn kein Dateisystem vorhanden ist.
- Dieser Befehl funktioniert auf grundlegenden Volumes und auf einfachen oder übergreifenden dynamischen Volumes.
- Wenn ein gewünschter Betrag nicht angegeben wird, wird das Volume um den minimalen Betrag (sofern angegeben) reduziert.
- Wenn ein Minimalwert nicht angegeben wird, wird das Volume um den gewünschten Betrag (falls angegeben) reduziert.
- Wenn weder ein Minimalbetrag noch ein gewünschter Betrag angegeben ist, wird das Volume so weit wie möglich reduziert.
- Wenn ein Minimalwert angegeben ist, aber nicht genügend freier Speicherplatz verfügbar ist, schlägt der Befehl fehl.
- Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.
- Dieser Befehl funktioniert nicht für OEM-Partitionen (Original Equipment Manufacturer), Extensible Firmware Interface (EFI)-Systempartitionen oder Wiederherstellungs Partitionen.
  ## <a name="BKMK_examples"></a>Beispiele
  Geben Sie Folgendes ein, um die Größe des ausgewählten Volumes um die größtmögliche Größe zwischen 250 und 500 Megabyte zu verringern:
  ```
  shrink desired=500 minimum=250
  ```
  Geben Sie Folgendes ein, um die maximale Anzahl von MB anzuzeigen, um die das Volume durch reduziert werden kann:
  ```
  shrink querymax
  ```

[Resize-Partition](https://technet.microsoft.com/library/hh848680.aspx)
