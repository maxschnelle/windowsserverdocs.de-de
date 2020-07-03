---
title: offline disk
description: Referenz Artikel für den Befehl "Offline Datenträger", bei dem der Online Datenträger in den Offline Zustand versetzt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cc8a746e09e5756eec1890d1715a88e60696cd49
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936754"
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

| Parameter | Beschreibung |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

### <a name="examples"></a>Beispiele

Wenn Sie den Fokus offline schalten möchten, geben Sie Folgendes ein:

```
offline disk
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
