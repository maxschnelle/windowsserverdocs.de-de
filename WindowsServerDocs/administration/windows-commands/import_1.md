---
title: Importieren von DiskPart
description: Referenz Artikel für den Import-Befehl, mit dem eine fremde Datenträger Gruppe in die Datenträger Gruppe des lokalen Computers importiert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 072c012e5e2cc8d49811fbfa1cff5140b2c745a1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924423"
---
# <a name="import-diskpart"></a>import (diskpart)

Importiert eine fremde Datenträger Gruppe in die Datenträger Gruppe des lokalen Computers. Mit diesem Befehl wird jeder Datenträger importiert, der sich in derselben Gruppe wie der Datenträger mit dem Fokus befindet.

> Wichtig Bevor Sie diesen Befehl verwenden können, müssen Sie den Befehl "Datenträger [auswählen](select-disk.md) " verwenden, um einen dynamischen Datenträger in einer fremden Datenträger Gruppe auszuwählen und den Fokus darauf zu verschieben.

## <a name="syntax"></a>Syntax

```
import [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
