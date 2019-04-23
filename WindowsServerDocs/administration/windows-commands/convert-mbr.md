---
title: MBR konvertieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a635a4c0-af73-4330-b021-51d483424537
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da8d62567863bc38a5aa0b35a8f3fe4ee24cc888
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834611"
---
# <a name="convert-mbr"></a>MBR konvertieren



Konvertiert einen leeren Basisdatenträger mit dem Partitionsstil GUID-Partitionstabelle (GPT) in einem einfachen Datenträger mit dem Partitionsstil der master Boot Record (MBR).

> [!IMPORTANT]
> Der Datenträger muss für die Konvertierung in einen MBR-Datenträger leer sein. Sichern Sie Ihre Daten, und klicken Sie dann löschen Sie alle Partitionen oder Volumes, bevor der Datenträger konvertieren.

Anweisungen dazu, wie Sie diesen Befehl verwenden, finden Sie unter [ändern, eine GUID-Partitionstabelle in einen Datenträger für das Master Boot Record](https://go.microsoft.com/fwlink/?LinkId=207050) (https://go.microsoft.com/fwlink/?LinkId=207050).

## <a name="syntax"></a>Syntax

```
convert mbr [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

-   Ein einfachen Datenträger muss ausgewählt werden, für diesen Vorgang erfolgreich ausgeführt werden kann. Verwenden der **select Disk** Befehl aus, wählen Sie einen Basisdatenträger und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie zum Konvertieren einer basic-CD von GPT-Partitionstyp in MBR-Partitionstyp >:
```
convert mbr
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

