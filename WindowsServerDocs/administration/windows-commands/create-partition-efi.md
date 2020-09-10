---
title: create partition efi
description: Referenz Artikel zum create partition efi-Befehl, mit dem eine Extensible Firmware Interface (EFI)-Systempartition auf einem GPT-Datenträger (GUID-Partitionstabelle) auf Itanium-basierten Computern erstellt wird.
ms.topic: reference
ms.assetid: 3cfc1fca-6515-4a4d-bfae-615fa8045ea9
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a3eacad949a4a5c14c40da0469155e277cb274b6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629206"
---
# <a name="create-partition-efi"></a>create partition efi

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)

- [select disk](select-disk.md)
