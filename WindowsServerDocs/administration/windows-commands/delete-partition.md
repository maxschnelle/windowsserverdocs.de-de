---
title: Löschen einer partition
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 3b47338b74cf71a4754b7320d6b3842f342d324d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436139"
---
# <a name="delete-partition"></a>Löschen einer partition



Löscht die Partition mit dem Fokus.

## <a name="syntax"></a>Syntax

```
delete partition [noerr] [override]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|override|Können DiskPart, um jede Partition unabhängig von der Art zu löschen. DiskPart lässt in der Regel nur bekannte Datenpartitionen zu löschen.|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

> [!CAUTION]
> Durch das Löschen einer Partitions auf einem dynamischen Datenträger können alle dynamischen Volumes auf dem Datenträger somit dadurch alle Daten beschädigt werden und des Datenträgers beschädigt. Um ein dynamisches Volume löschen, verwenden Sie immer die **Volume löschen** stattdessen den Befehl. Partitionen können dynamische Datenträger gelöscht werden, aber sie sollten nicht erstellt werden. Beispielsweise ist es möglich, eine unbekanntes GUID-Partitionstabelle (GPT) Partition auf einem dynamischen GPT-Datenträger zu löschen. Löschen einer solchen Partition bewirkt nicht, den sich ergebenden freien Speicherplatz verfügbar wird. Mit diesem Befehl Reclame Speicherplatz auf einem beschädigten offline dynamischen Datenträger in einer Notsituation ermöglichen soll, in denen die **Bereinigen** Befehl in DiskPart kann nicht verwendet werden.
> -   Die Systempartition, Startpartition oder eine Partition, die die aktive Paging-Datei oder ein Absturz Dumpinformationen enthält, kann nicht gelöscht werden.
> -   Eine Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Partition** Befehl aus, um eine Partition auswählen, und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Um die Partition mit den Fokus zu löschen, geben Sie Folgendes ein:
```
delete partition
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

