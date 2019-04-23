---
title: Attribute-Datenträger
description: Windows-Befehle Thema **Attribute Datenträger** -zeigt, Mengen oder löscht die Attribute eines Datenträgers.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eed57071-c1c6-4394-9542-62b52a878c92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7cacc2fb6b47d095f5e452ca470c89f228949594
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890351"
---
# <a name="attributes-disk"></a>Attribute-Datenträger



Zeigt an, legt fest oder löscht die Attribute eines Datenträgers.

> [!IMPORTANT]
> Dieser Parameter ist nicht in jeder Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax

```
attributes disk [{set | clear}] [readonly] [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|set|Legt das angegebene Attribut des Datenträgers mit dem Fokus fest.|
|clear|Löscht das angegebene Attribut des Datenträgers mit dem Fokus.|
|ReadOnly|Gibt an, dass es sich bei der Datenträger schreibgeschützt ist.|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

-   Wenn **Attribute Datenträger** ist zum Anzeigen der aktuellen Attribute eines Datenträgers verwendet, das Startup Disk-Attribut gibt den Datenträger, die zum Starten des Computers verwendet wird. Für eine dynamische Spiegelung wird er für den Datenträger angezeigt, die der Start-plexer des Startvolumes enthält.
-   Ein Datenträger muss ausgewählt werden, für die **Attribute Datenträger** Befehl erfolgreich ausgeführt werden kann. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie zum Anzeigen der Attribute des ausgewählten Datenträgers:
```
attributes disk
```
Um den ausgewählten Datenträger als schreibgeschützt festzulegen, geben Sie Folgendes ein:
```
attributes disk set readonly
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

