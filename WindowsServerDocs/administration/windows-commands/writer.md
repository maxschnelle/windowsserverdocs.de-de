---
title: Writer
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cf98295-411d-4705-8573-f898ff45c140
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8aee4ecca85c7d5f46ee79f3ad928b746c02e7bb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439983"
---
# <a name="writer"></a>Writer



Überprüft, ob ein Writer oder eine Komponente enthalten ist oder ein Writer oder eine Komponente aus der Sicherung oder Wiederherstellung Prozedur schließt. Wenn Sie ohne Angabe von Parametern **Writer** zeigt die Hilfe an der Eingabeaufforderung.

## <a name="syntax"></a>Syntax

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

## <a name="parameters"></a>Parameter

| Parameter  |                                                                                      Beschreibung                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   verify   | Stellt sicher, dass die angegebenen Writer oder die Komponente in der Backup- oder Restore-Prozedur enthalten ist. Die Backup- oder Restore-Prozedur schlägt fehl, wenn der Writer oder die Komponente nicht enthalten ist. |
|  exclude   |                                                   Schließt die angegebenen Writer oder die Komponente aus der Backup- oder Restore-Prozedur aus.                                                    |
| [\<Writer> |                                                                                     <Component>]                                                                                      |

## <a name="BKMK_examples"></a>Beispiele für

Um einen Writer durch Angabe der GUID (für dieses Beispiel 4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f) zu überprüfen, geben Sie Folgendes ein:
```
writer verify {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
```
Um einen Writer, mit dem Namen "Systemgenerator" ausschließen möchten, geben Sie Folgendes ein:
```
writer exclude "System Writer"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)