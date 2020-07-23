---
title: delete disk
description: Referenz Artikel für den Befehl "Datenträger löschen", mit dem ein fehlender dynamischer Datenträger aus der Liste der Datenträger gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55eabb19e10a7ca6fe4dd705ab91961919bb2b7c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958402"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DELETE-Befehl](delete.md)
