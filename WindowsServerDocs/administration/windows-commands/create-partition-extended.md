---
title: Erstellen einer Partition erweitert
description: Referenz Thema für den erweiterten Create Partition-Befehl, mit dem eine erweiterte Partition auf dem Datenträger mit dem Fokus erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4ad7cb66-9c66-4153-b94e-1030a7225070
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d2cc591dca276f70b3ddda1827607d5e2953ed2
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993283"
---
# <a name="create-partition-extended"></a>Erstellen einer Partition erweitert

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine erweiterte Partition auf dem Datenträger mit dem Fokus. Nachdem die Partition erstellt wurde, wird der Fokus automatisch auf die neue Partition verlagert.

>[!IMPORTANT]
> Sie können diesen Befehl nur auf MBR-Datenträgern (Master Boot Record) verwenden. Sie müssen den Befehl "Datenträger [auswählen](select-disk.md) " verwenden, um einen einfachen MBR-Datenträger auszuwählen und den Fokus darauf zu verschieben.
>
> Sie müssen eine erweiterte Partition erstellen, bevor Sie logische Laufwerke erstellen können. Pro Datenträger kann nur eine erweiterte Partition erstellt werden. Dieser Befehl schlägt fehl, wenn Sie versuchen, eine erweiterte Partition innerhalb einer anderen erweiterten Partition zu erstellen.

## <a name="syntax"></a>Syntax

```
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Größe =`<n>` | Gibt die Größe der Partition in Megabyte (MB) an. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis der freie Speicherplatz in der erweiterten Partition nicht mehr verfügbar ist. |
| Offset =`<n>` | Gibt den Offset in Kilobyte (KB) an, bei dem die Partition erstellt wird. Wenn kein Offset angegeben wird, wird die Partition am Anfang des freien Speicherplatzes auf dem Datenträger gestartet, der groß genug ist, um die neue Partition zu speichern. |
| ausrichten =`<n>` | Richtet alle Partitions Blöcke an die nächstgelegene Ausrichtungs Grenze aus. Wird in der Regel mit den Hardware-RAID-Arrays der logischen Gerätenummer verwendet, um die Leistung zu verbessern. `<n>`die Anzahl der Kilobyte (KB) vom Anfang des Datenträgers bis zur nächsten Ausrichtungs Grenze. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine erweiterte Partition mit einer Größe von 1000 Megabyte zu erstellen:

```
create partition extended size=1000
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)

- [select disk](select-disk.md)
