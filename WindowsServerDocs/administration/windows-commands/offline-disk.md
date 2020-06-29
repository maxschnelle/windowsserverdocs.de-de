---
title: offline disk
description: Referenz Thema für den Befehl "Offline Datenträger", bei dem der Online Datenträger in den Offline Zustand versetzt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c62a79db39a7c36e14a8430b47c634f80c0c0c8
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472746"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
