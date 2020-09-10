---
title: offline volume
description: Referenz Artikel für den Befehl "Offline Volume", bei dem das Online Volume mit dem Fokus in den Offline Zustand versetzt wird.
ms.topic: reference
ms.assetid: b8f7192f-ea38-47d0-9d4e-58ef68336ae6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7902ef109c7e893d2610ae308a391d9efafbabfd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627375"
---
# <a name="offline-volume"></a>offline volume

Schaltet das Online Volume mit dem Fokus in den Offline Zustand.

> [!NOTE]
> Ein Volume muss ausgewählt werden, damit der Befehl **Offline Volume** erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl [Volume auswählen](select-volume.md) einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="syntax"></a>Syntax

```
offline volume [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

### <a name="examples"></a>Beispiele

Wenn Sie den Fokus offline schalten möchten, geben Sie Folgendes ein:

```
offline volume
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
