---
title: Import
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 569d986c57ae8b3d7253c050146ac0583c7c92df
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724846"
---
# <a name="import"></a>Import



Importiert eine fremde Datenträger Gruppe in die Datenträger Gruppe des lokalen Computers.

## <a name="syntax"></a>Syntax

```
import [noerr]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Bemerkungen

-   Der Import-Befehl importiert jeden Datenträger, der sich in derselben Gruppe wie der Datenträger mit dem Fokus befindet.
-   Ein dynamischer Datenträger in einer Gruppe von fremden Datenträgern muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Datenträger zu importieren, die sich in der gleichen Datenträger Gruppe wie der Datenträger mit dem Fokus auf die Datenträger Gruppe des lokalen Computers befinden
```
import
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

