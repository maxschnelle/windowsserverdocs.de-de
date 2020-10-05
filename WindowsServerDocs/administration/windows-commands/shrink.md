---
title: shrink
description: Referenz Artikel für den Befehl DiskPart Shrink, der die Größe des ausgewählten Volumes um den von Ihnen angegebenen Betrag reduziert.
ms.topic: reference
ms.assetid: ec87cc7c-9846-465e-a10d-4ee10db4f4e6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8b03c006243f263a4f1c7fe991580d5e74f9a7a7
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718317"
---
# <a name="shrink"></a>shrink

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der DiskPart-Verkleinerungs Befehl reduziert die Größe des ausgewählten Volumes um den von Ihnen angegebenen Betrag. Mit diesem Befehl wird freier Speicherplatz aus dem nicht verwendeten Speicherplatz am Ende des Volumes bereitgestellt.

Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.

> [!NOTE]
> Dieser Befehl funktioniert auf grundlegenden Volumes und auf einfachen oder übergreifenden dynamischen Volumes. Es funktioniert nicht für OEM-Partitionen (Original Equipment Manufacturer), Extensible Firmware Interface (EFI)-Systempartitionen oder Wiederherstellungs Partitionen.

## <a name="syntax"></a>Syntax

```
shrink [desired=<n>] [minimum=<n>] [nowait] [noerr]
shrink querymax [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| gewünscht =`<n>` | Gibt die gewünschte Menge an Speicherplatz in Megabyte (MB) an, um die Größe des Volumes um zu verringern. |
| minimal =`<n>` | Gibt den minimalen Speicherplatz in MB an, um die Größe des Volumes zu verringern. |
| querymax | Gibt den maximalen Speicherplatz in MB zurück, um den das Volume reduziert werden kann. Dieser Wert kann sich ändern, wenn Anwendungen derzeit auf das Volume zugreifen. |
| nowait | Erzwingt, dass der Befehl sofort zurückgegeben wird, während der Verkleinerungs Prozess noch ausgeführt wird. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

#### <a name="remarks"></a>Bemerkungen

- Sie können die Größe eines Volumes nur verringern, wenn er mit dem NTFS-Dateisystem formatiert ist oder wenn kein Dateisystem vorhanden ist.

- Wenn ein gewünschter Betrag nicht angegeben wird, wird das Volume um den minimalen Betrag (falls angegeben) reduziert.

- Wenn eine minimale Menge nicht angegeben wird, wird das Volume um den gewünschten Betrag (falls angegeben) reduziert.

- Wenn weder ein Minimalbetrag noch ein gewünschter Betrag angegeben ist, wird das Volume so weit wie möglich reduziert.

- Wenn ein Minimalwert angegeben ist, aber nicht genügend freier Speicherplatz verfügbar ist, schlägt der Befehl fehl.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Größe des ausgewählten Volumes um die größtmögliche Größe zwischen 250 und 500 Megabyte zu verringern:

```
shrink desired=500 minimum=250
```

Geben Sie Folgendes ein, um die maximale Anzahl von MB anzuzeigen, um die das Volume durch reduziert werden kann:

```
shrink querymax
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Resize-Partition](/powershell/module/storage/resize-partition?view=win10-ps&preserve-view=true)
