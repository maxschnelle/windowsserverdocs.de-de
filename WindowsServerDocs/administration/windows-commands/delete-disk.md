---
title: delete disk
description: Referenz Artikel für den Befehl "Datenträger löschen", mit dem ein fehlender dynamischer Datenträger aus der Liste der Datenträger gelöscht wird.
ms.topic: reference
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f26bd239c1248630da4ce684547961a239f96b8e
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628867"
---
# <a name="delete-disk"></a>delete disk

Löscht eine fehlende dynamische Festplatte aus der Liste der Datenträger.

> [!NOTE]
> Ausführliche Anweisungen zur Verwendung dieses Befehls finden Sie unter [Entfernen eines fehlenden dynamischen](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc753029(v=ws.11))Datenträgers.

## <a name="syntax"></a>Syntax

```
delete disk [noerr] [override]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |
| override | Ermöglicht DiskPart das Löschen aller einfachen Volumes auf dem Datenträger. Wenn der Datenträger die Hälfte eines gespiegelten Volumes enthält, wird die Hälfte der Spiegelung auf dem Datenträger gelöscht. Der Befehl zum Überschreiben des Datenträgers löschen schlägt fehl, wenn der Datenträger Mitglied eines RAID-5-Volumes ist. |

## <a name="examples"></a>Beispiele

Um einen fehlenden dynamischen Datenträger aus der Liste der Datenträger zu löschen, geben Sie Folgendes ein:

```
delete disk
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DELETE-Befehl](delete.md)
