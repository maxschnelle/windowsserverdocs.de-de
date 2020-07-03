---
title: delete partition
description: Referenz Artikel für den Befehl "Partition löschen", mit dem die Partition mit dem Fokus gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 65752312-cb16-46f6-870f-1b95c507b101
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b45cb060a5d82e254fe371269dbdbcb9d46fee92
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928727"
---
# <a name="delete-partition"></a>delete partition

Löscht die Partition mit dem Fokus. Bevor Sie beginnen, müssen Sie eine Partition auswählen, damit dieser Vorgang erfolgreich ausgeführt werden kann. Wählen Sie mit dem Befehl [Partition auswählen](select-partition.md) eine Partition aus, und verschieben Sie den Fokus auf die Partition.

> [!WARNING]
> Durch das Löschen einer Partition auf einem dynamischen Datenträger können alle dynamischen Volumes auf dem Datenträger gelöscht, sämtliche Daten zerstört und der Datenträger beschädigt werden.
>
> Sie können die Systempartition, die Start Partition oder eine beliebige Partition, die die aktive Auslagerungs Datei oder die Absturz Abbild Informationen enthält, nicht löschen.

## <a name="syntax"></a>Syntax

```
delete partition [noerr] [override]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |
| override | Ermöglicht DiskPart das Löschen beliebiger Partitionen unabhängig vom Typ. In der Regel gestattet DiskPart nur das Löschen bekannter Daten Partitionen. |

#### <a name="remarks"></a>Hinweise

- Wenn Sie ein dynamisches Volume löschen möchten, verwenden Sie stattdessen immer den Befehl [Volume löschen](delete-volume.md) .

- Partitionen können aus dynamischen Datenträgern gelöscht, aber nicht erstellt werden. Beispielsweise ist es möglich, eine nicht erkannte GPT-Partition (GUID-Partitionstabelle) auf einem dynamischen GPT-Datenträger zu löschen. Das Löschen einer solchen Partition führt nicht dazu, dass der resultierende freie Speicherplatz verfügbar wird. Stattdessen soll dieser Befehl es Ihnen ermöglichen, in einer Notfallsituation, in der der [Clean](clean.md) -Befehl in DiskPart verwendet werden kann, Speicherplatz auf einem beschädigten Offline-Datenträger freizugeben.

## <a name="examples"></a>Beispiele

Um die Partition mit dem Fokus zu löschen, geben Sie Folgendes ein:

```
delete partition
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [select partition](select-partition.md)

- [DELETE-Befehl](delete.md)

- [Befehl "Volume löschen"](delete-volume.md)

- [Befehl "Clean"](clean.md)
