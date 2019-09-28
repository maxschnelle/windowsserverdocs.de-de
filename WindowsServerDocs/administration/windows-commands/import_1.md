---
title: Importieren
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca0a15e73e4aa913ece34e083a8070be3b4b190d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375408"
---
# <a name="import"></a>Importieren



Importiert eine fremde Datenträger Gruppe in die Datenträger Gruppe des lokalen Computers.

## <a name="syntax"></a>Syntax

```
import [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Der Import-Befehl importiert jeden Datenträger, der sich in derselben Gruppe wie der Datenträger mit dem Fokus befindet.
-   Ein dynamischer Datenträger in einer Gruppe von fremden Datenträgern muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Datenträger zu importieren, die sich in der gleichen Datenträger Gruppe wie der Datenträger mit dem Fokus auf die Datenträger Gruppe des lokalen Computers befinden
```
import
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

