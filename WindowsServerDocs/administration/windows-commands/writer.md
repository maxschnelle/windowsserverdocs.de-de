---
title: writer
description: Windows-Befehls Thema für Writer, mit dem überprüft wird, ob ein Writer oder eine Komponente ein Writer oder eine Komponente aus dem Sicherungs-oder Wiederherstellungsverfahren umfasst oder ausschließt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7cf98295-411d-4705-8573-f898ff45c140
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb13de162b8e5eb8150d145a4afacccf47bb25f0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828983"
---
# <a name="writer"></a>writer



Überprüft, ob ein Writer oder eine Komponente ein Writer oder eine Komponente aus dem Sicherungs-oder Wiederherstellungsverfahren enthält bzw. schließt. Bei Verwendung ohne Parameter zeigt **Writer** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

### <a name="parameters"></a>Parameter

| Parameter  |                                                                                      Beschreibung                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   Überprüfen   | Überprüft, ob der angegebene Writer oder die angegebene Komponente in der Sicherungs-oder Wiederherstellungs Prozedur enthalten ist. Die Sicherungs-oder Wiederherstellungs Prozedur schlägt fehl, wenn der Writer oder die Komponente nicht enthalten ist. |
|  ausschließen   |                                                   Schließt den angegebenen Writer oder die Komponente vom Sicherungs-oder Wiederherstellungsverfahren aus.                                                    |
| [\<Writer-> |                                                                                     <Component>]                                                                                      |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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