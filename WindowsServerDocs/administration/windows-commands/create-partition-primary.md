---
title: create partition primary
description: Referenz Thema für den Befehl create partition primary, mit dem eine primäre Partition auf dem Basis Datenträger mit dem Fokus erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6d652d8e-3935-4a91-8ced-b17c0e7937be
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ac1763d52d8caf90112fb371aeac5e6b501bd2ea
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993240"
---
# <a name="create-partition-primary"></a>create partition primary

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine primäre Partition auf dem Basis Datenträger mit dem Fokus. Nachdem die Partition erstellt wurde, wird der Fokus automatisch auf die neue Partition verlagert.

> [!IMPORTANT]
> Ein Basis Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Sie müssen den Befehl "Datenträger [auswählen](select-disk.md) " verwenden, um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

## <a name="syntax"></a>Syntax

```
create partition primary [size=<n>] [offset=<n>] [id={ <byte> | <guid> }] [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Größe =`<n>` | Gibt die Größe der Partition in Megabyte (MB) an. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis nicht mehr zugewiesener Speicherplatz in der aktuellen Region vorhanden ist. |
| Offset =`<n>` | Der Offset in Kilobyte (KB), an dem die Partition erstellt wird. Wenn kein Offset angegeben wird, wird die Partition am Anfang des größten Datenträger Blocks gestartet, der groß genug ist, um Sie zu speichern. |
| ausrichten =`<n>` | Richtet alle Partitions Blöcke an die nächstgelegene Ausrichtungs Grenze aus. Wird in der Regel mit den Hardware-RAID-Arrays der logischen Gerätenummer verwendet, um die Leistung zu verbessern. `<n>`die Anzahl der Kilobyte (KB) vom Anfang des Datenträgers bis zur nächsten Ausrichtungs Grenze. |
| ID = { `<byte>  | <guid>` } | Gibt den Partitionstyp an. Dieser Parameter ist nur für die Verwendung durch Originalgerätehersteller (Original Equipment Manufacturer, OEM) vorgesehen. Mit diesem Parameter können beliebige Byte-oder GUID-Partitionstypen angegeben werden. DiskPart überprüft den Partitionstyp nicht auf Gültigkeit, außer um sicherzustellen, dass es sich um ein Byte in Hexadezimal Form oder eine GUID handelt. **Vorsicht:** Das Erstellen von Partitionen mit diesem Parameter kann dazu führen, dass der Computer ausfällt oder nicht gestartet werden kann. Wenn Sie kein OEM-oder IT-Experte mit GPT-Datenträgern sind, erstellen Sie keine Partitionen auf GPT-Datenträgern mithilfe dieses Parameters. Verwenden Sie stattdessen immer den Befehl [create partition efi](create-partition-efi.md) , um EFI-System Partitionen, den [create partition msr](create-partition-msr.md) -Befehl zum Erstellen von reservierten Microsoft-Partitionen und den [create partition primary](create-partition-primary.md)-Befehl `id={ <byte>  | <guid>` (ohne den-Parameter) zu erstellen, um primäre Partitionen auf GPT-Datenträgern zu erstellen.<p>**Für Master Boot Record-Datenträger (MBR)** müssen Sie für die Partition ein Byte des Partitions Typs (in Hexadezimal Form) angeben. Wenn dieser Parameter nicht angegeben wird, erstellt der Befehl eine Partition des `0x06`Typs, die angibt, dass ein Dateisystem nicht installiert ist. Beispiele:<ul><li>**LDM-Daten Partition:** 0x42</li><li>**Wiederherstellungs Partition:** 0x27</li><li>**Erkannte OEM-Partition:** 0x12, 0x84, 0xde, 0xFE, 0xa0</li></ul><p>**Für GPT-Datenträger (GUID-Partitionstabelle)** können Sie für die Partition, die Sie erstellen möchten, eine GUID für den Partitionstyp angeben. Zu den erkannten GUIDs zählen:<ul><li>**EFI-Systempartition:** c12a7328-f81f-11d2-ba4b-00a0c93ec93b</li><li>**Reservierte Microsoft-Partition:** e3c9e316-0b5c-4db8-817d-f92df00215ae</li><li>**Grundlegende Daten Partition:** ebd0a0a2-b9e5-4433-87c0-68b6b72699c7</li><li>**LDM-Metadatenpartition (dynamischer Datenträger):** 5808c8aa-7e8f-42e0-85d2-e1e90434cfb3</li><li>**LDM-Daten Partition (dynamischer Datenträger):** af9b60a0-1431-4f62-bc68-3311714a69ad</li><li>**Wiederherstellungs Partition:** de94bba4-06d1-4d40-a16a-bfd50179d6ac<p>Wenn dieser Parameter für einen GPT-Datenträger nicht angegeben wird, erstellt der Befehl eine grundlegende Daten Partition.</li></ul> |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne den Noerr-Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine primäre Partition mit einer Größe von 1000 Megabyte zu erstellen:

```
create partition primary size=1000
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl zuweisen](assign.md)

- [Create-Befehl](create.md)

- [select disk](select-disk.md)
