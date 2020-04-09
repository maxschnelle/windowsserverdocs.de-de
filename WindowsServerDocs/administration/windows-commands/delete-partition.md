---
title: Partition löschen
description: Windows-Befehls Artikel zum Löschen einer Partition, die die Partition mit dem Fokus löscht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 65752312-cb16-46f6-870f-1b95c507b101
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a24c18cf98f2899fbb57f1f5f2d2776824d637b7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846573"
---
# <a name="delete-partition"></a>Partition löschen

Löscht die Partition mit dem Fokus.

## <a name="syntax"></a>Syntax

```
delete partition [noerr] [override]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|override|Ermöglicht DiskPart das Löschen beliebiger Partitionen unabhängig vom Typ. In der Regel gestattet DiskPart nur das Löschen bekannter Daten Partitionen.|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

> [!CAUTION]
> Durch das Löschen einer Partition auf einem dynamischen Datenträger können alle dynamischen Volumes auf dem Datenträger gelöscht werden. Dadurch werden alle Daten zerstört und der Datenträger in einem beschädigten Zustand belassen. Wenn Sie ein dynamisches Volume löschen möchten, verwenden Sie stattdessen immer den Befehl **Volume löschen** . Partitionen können aus dynamischen Datenträgern gelöscht, aber nicht erstellt werden. Beispielsweise ist es möglich, eine nicht erkannte GPT-Partition (GUID-Partitionstabelle) auf einem dynamischen GPT-Datenträger zu löschen. Das Löschen einer solchen Partition führt nicht dazu, dass der resultierende freie Speicherplatz verfügbar wird. Mit diesem Befehl können Sie in einer Notfallsituation, in der der **Clean** -Befehl in DiskPart nicht verwendet werden kann, den Speicherplatz auf einem beschädigten Offline-Datenträger wiederholen.
> -   Sie können die Systempartition, die Start Partition oder eine beliebige Partition, die die aktive Auslagerungs Datei oder die Absturz Abbild Informationen enthält, nicht löschen.
> -   Eine Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Partition auswählen** eine Partition aus, und verschieben Sie den Fokus auf die Partition.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um die Partition mit dem Fokus zu löschen, geben Sie Folgendes ein:
```
delete partition
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

