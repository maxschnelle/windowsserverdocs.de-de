---
title: Import
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7e098e7133bca18e1a6ba683e525783af17c3958
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842133"
---
# <a name="import"></a>Import



Importiert eine fremde Datenträger Gruppe in die Datenträger Gruppe des lokalen Computers.

## <a name="syntax"></a>Syntax

```
import [noerr]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Der Import-Befehl importiert jeden Datenträger, der sich in derselben Gruppe wie der Datenträger mit dem Fokus befindet.
-   Ein dynamischer Datenträger in einer Gruppe von fremden Datenträgern muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um alle Datenträger zu importieren, die sich in der gleichen Datenträger Gruppe wie der Datenträger mit dem Fokus auf die Datenträger Gruppe des lokalen Computers befinden
```
import
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

