---
title: Importieren von DiskPart
description: Referenz Artikel für den Import-Befehl, mit dem eine fremde Datenträger Gruppe in die Datenträger Gruppe des lokalen Computers importiert wird.
ms.topic: reference
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c20154e4f687aaaba5639baf4cbbbc6b536c72bd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634514"
---
# <a name="import-diskpart"></a>import (diskpart)

Importiert eine fremde Datenträger Gruppe in die Datenträger Gruppe des lokalen Computers. Mit diesem Befehl wird jeder Datenträger importiert, der sich in derselben Gruppe wie der Datenträger mit dem Fokus befindet.

> Wichtig Bevor Sie diesen Befehl verwenden können, müssen Sie den Befehl "Datenträger [auswählen](select-disk.md) " verwenden, um einen dynamischen Datenträger in einer fremden Datenträger Gruppe auszuwählen und den Fokus darauf zu verschieben.

## <a name="syntax"></a>Syntax

```
import [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Datenträger zu importieren, die sich in der gleichen Datenträger Gruppe wie der Datenträger mit dem Fokus auf die Datenträger Gruppe des lokalen Computers befinden

```
import
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Diskpart-Befehl](diskpart.md)
