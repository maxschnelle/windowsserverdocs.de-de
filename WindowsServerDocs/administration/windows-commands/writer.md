---
title: writer
description: Referenz Artikel für Writer, mit dem überprüft wird, ob ein Writer oder eine Komponente ein Writer oder eine Komponente aus dem Sicherungs-oder Wiederherstellungsverfahren umfasst oder ausschließt.
ms.topic: reference
ms.assetid: 7cf98295-411d-4705-8573-f898ff45c140
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 061def6ad0aa0240f1c50b92fa567bc1636650d8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628495"
---
# <a name="writer"></a>writer



Überprüft, ob ein Writer oder eine Komponente ein Writer oder eine Komponente aus dem Sicherungs-oder Wiederherstellungsverfahren enthält bzw. schließt. Bei Verwendung ohne Parameter zeigt **Writer** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

### <a name="parameters"></a>Parameter

| Parameter  |                                                                                      BESCHREIBUNG                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   Überprüfen   | Überprüft, ob der angegebene Writer oder die angegebene Komponente in der Sicherungs-oder Wiederherstellungs Prozedur enthalten ist. Die Sicherungs-oder Wiederherstellungs Prozedur schlägt fehl, wenn der Writer oder die Komponente nicht enthalten ist. |
|  Ausschließen   |                                                   Schließt den angegebenen Writer oder die Komponente vom Sicherungs-oder Wiederherstellungsverfahren aus.                                                    |
| [\<Writer> |                                                                                     <Component>]                                                                                      |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen Writer zu überprüfen, indem Sie die GUID angeben (in diesem Beispiel 4dc3bdd4-AB48-4d07-adb0-3bee2926fd7f):
```
writer verify {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
```
Um einen Writer mit dem Namen System-Writer auszuschließen, geben Sie Folgendes ein:
```
writer exclude System Writer
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)