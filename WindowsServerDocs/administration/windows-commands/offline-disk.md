---
title: offline disk
description: Referenz Artikel für den Befehl "Offline Datenträger", bei dem der Online Datenträger in den Offline Zustand versetzt wird.
ms.topic: reference
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 678ab63327523e06ae4946413557cc7d45466de0
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627407"
---
# <a name="offline-disk"></a>offline disk

Schaltet den Online Datenträger mit dem Fokus in den Offline Zustand. Wenn ein dynamischer Datenträger in einer Datenträger Gruppe offline geschaltet wird, ändert sich der Status des Datenträgers in **fehlt** , und in der Gruppe wird ein Datenträger angezeigt, der offline ist. Der fehlende Datenträger wird in die ungültige Gruppe verschoben. Wenn die dynamische Festplatte der letzte Datenträger in der Gruppe ist, wird der Status des Datenträgers in **Offline**geändert, und die leere Gruppe wird entfernt.

> [!NOTE]
> Ein Datenträger muss ausgewählt werden, damit der **Offline** -Datenträger Befehl erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger [auswählen](select-disk.md) einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.
>
> Dieser Befehl funktioniert auch auf Datenträgern im San Online-Modus, indem der San-Modus in Offline geändert wird.

## <a name="syntax"></a>Syntax

```
offline disk [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

### <a name="examples"></a>Beispiele

Wenn Sie den Fokus offline schalten möchten, geben Sie Folgendes ein:

```
offline disk
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
