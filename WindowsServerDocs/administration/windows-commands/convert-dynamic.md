---
title: Dynamische konvertieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 353c1e4558ab2b0c948ec78c0cd87b579c738ec8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841611"
---
# <a name="convert-dynamic"></a>Dynamische konvertieren



Konvertiert einen Basisdatenträger in einen dynamischen Datenträger.

Anweisungen dazu, wie Sie diesen Befehl verwenden, finden Sie unter [ändern Sie einen Basisdatenträger in einen dynamischen Datenträger](https://go.microsoft.com/fwlink/?LinkId=207047) (https://go.microsoft.com/fwlink/?LinkId=207047).

## <a name="syntax"></a>Syntax

```
convert dynamic [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

-   Alle vorhandenen Partitionen auf der Basisfestplatte werden einfache Volumes.
-   Ein einfachen Datenträger muss ausgewählt werden, für diesen Vorgang erfolgreich ausgeführt werden kann. Verwenden der **select Disk** Befehl aus, wählen Sie einen Basisdatenträger und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Um einen Basisdatenträger in einen dynamischen Datenträger konvertieren möchten, geben Sie Folgendes ein:
```
convert dynamic
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

