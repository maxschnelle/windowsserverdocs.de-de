---
title: Datenträger löschen
description: Windows-Befehls Thema zum Löschen von Datenträgern, wodurch ein fehlender dynamischer Datenträger aus der Liste der Datenträger gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1a767e0689d5fbabb193df37528a0909ab63a1ab
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846653"
---
# <a name="delete-disk"></a>Datenträger löschen

Löscht eine fehlende dynamische Festplatte aus der Liste der Datenträger.

Anweisungen zur Verwendung dieses Befehls finden Sie unter [Entfernen eines fehlenden dynamischen](https://go.microsoft.com/fwlink/?LinkId=207055) Datenträgers (https://go.microsoft.com/fwlink/?LinkId=207055).

## <a name="syntax"></a>Syntax

```
delete disk [noerr] [override]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|
|override|Ermöglicht DiskPart das Löschen aller einfachen Volumes auf dem Datenträger. Wenn der Datenträger die Hälfte eines gespiegelten Volumes enthält, wird die Hälfte der Spiegelung auf dem Datenträger gelöscht. Der Befehl zum Überschreiben des Datenträgers löschen schlägt fehl, wenn der Datenträger Mitglied eines RAID-5-Volumes ist.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um einen fehlenden dynamischen Datenträger aus der Liste der Datenträger zu löschen, geben Sie Folgendes ein:
```
delete disk
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

