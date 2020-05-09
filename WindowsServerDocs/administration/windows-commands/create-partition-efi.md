---
title: Erstellen von EFI-Partitionen
description: Referenz Thema zum create partition efi-Befehl, mit dem eine Extensible Firmware Interface (EFI)-Systempartition auf einem GPT-Datenträger (GUID-Partitionstabelle) auf Itanium-basierten Computern erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cfc1fca-6515-4a4d-bfae-615fa8045ea9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8c314d756bebd0d0ec2ed9c844f714f395d04c6b
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993291"
---
# <a name="create-partition-efi"></a>Erstellen von EFI-Partitionen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine Extensible Firmware Interface (EFI)-Systempartition auf einem GPT-Datenträger (GUID-Partitionstabelle) auf Itanium-basierten Computern. Nachdem die Partition erstellt wurde, wird der Fokus auf die neue Partition gestellt.

>[!NOTE]
> Ein GPT-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger [auswählen](select-disk.md) einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="syntax"></a>Syntax

```
create partition efi [size=<n>] [offset=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Größe =`<n>` | Die Größe der Partition in Megabyte (MB). Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis in der aktuellen Region kein freier Speicherplatz mehr verfügbar ist. |
| Offset =`<n>` | Der Offset in Kilobyte (KB), an dem die Partition erstellt wird. Wenn kein Offset angegeben wird, wird die Partition in den ersten Datenträger Block eingefügt, der groß genug ist, um Sie zu speichern. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

#### <a name="remarks"></a>Hinweise

- Sie müssen mindestens ein Volume mit dem Befehl " **Volume hinzufügen** " hinzufügen, bevor Sie den Befehl " **Create** " verwenden können.

- Nachdem Sie den **Create** -Befehl ausgeführt haben, können Sie mit dem Befehl **exec** ein duplikatskript für die Sicherung aus der Schatten Kopie ausführen.

- Mit dem Befehl **Sicherung starten** können Sie anstelle einer Kopiesicherung eine vollständige Sicherung angeben.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine EFI-Partition von 1000 Megabyte auf dem ausgewählten Datenträger zu erstellen:

```
create partition efi size=1000
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)

- [select disk](select-disk.md)
