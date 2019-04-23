---
title: Datenträger löschen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e401133854118e82a45fd5e01466288ae41f67da
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863911"
---
# <a name="delete-disk"></a>Datenträger löschen



Löscht einen fehlenden dynamischen Datenträger aus der Liste der Datenträger an.

Anweisungen dazu, wie Sie diesen Befehl verwenden, finden Sie unter [Entfernen eines dynamischen Datenträgers mit fehlenden](https://go.microsoft.com/fwlink/?LinkId=207055) (https://go.microsoft.com/fwlink/?LinkId=207055).

## <a name="syntax"></a>Syntax

```
delete disk [noerr] [override]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|
|override|Können DiskPart, um alle einfachen Volumes auf dem Datenträger zu löschen. Wenn der Datenträger Teil eines gespiegelten Volumes enthält, wird die Hälfte der Spiegelung auf dem Datenträger gelöscht. Der Löschbefehl für Datenträger außer Kraft setzen schlägt fehl, wenn der Datenträger ein RAID-5-Volume angehört.|

## <a name="BKMK_examples"></a>Beispiele für

Um einen fehlenden dynamischen Datenträger aus der Liste der Datenträger zu löschen, geben Sie Folgendes ein:
```
delete disk
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

