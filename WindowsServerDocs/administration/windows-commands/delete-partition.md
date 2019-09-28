---
title: Partition löschen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65752312-cb16-46f6-870f-1b95c507b101
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46a214f26e7c21f6ae08eb16d95fd898bd949b0f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378663"
---
# <a name="delete-partition"></a>Partition löschen



Löscht die Partition mit dem Fokus.

## <a name="syntax"></a>Syntax

```
delete partition [noerr] [override]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Dire|Ermöglicht DiskPart das Löschen beliebiger Partitionen unabhängig vom Typ. In der Regel gestattet DiskPart nur das Löschen bekannter Daten Partitionen.|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

> [!CAUTION]
> Durch das Löschen einer Partition auf einem dynamischen Datenträger können alle dynamischen Volumes auf dem Datenträger gelöscht werden. Dadurch werden alle Daten zerstört und der Datenträger in einem beschädigten Zustand belassen. Wenn Sie ein dynamisches Volume löschen möchten, verwenden Sie stattdessen immer den Befehl **Volume löschen** . Partitionen können aus dynamischen Datenträgern gelöscht, aber nicht erstellt werden. Beispielsweise ist es möglich, eine nicht erkannte GPT-Partition (GUID-Partitionstabelle) auf einem dynamischen GPT-Datenträger zu löschen. Das Löschen einer solchen Partition führt nicht dazu, dass der resultierende freie Speicherplatz verfügbar wird. Mit diesem Befehl können Sie in einer Notfallsituation, in der der **Clean** -Befehl in DiskPart nicht verwendet werden kann, den Speicherplatz auf einem beschädigten Offline-Datenträger wiederholen.
> -   Sie können die Systempartition, die Start Partition oder eine beliebige Partition, die die aktive Auslagerungs Datei oder die Absturz Abbild Informationen enthält, nicht löschen.
> -   Eine Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Partition auswählen** eine Partition aus, und verschieben Sie den Fokus auf die Partition.

## <a name="BKMK_examples"></a>Beispiele

Um die Partition mit dem Fokus zu löschen, geben Sie Folgendes ein:
```
delete partition
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

