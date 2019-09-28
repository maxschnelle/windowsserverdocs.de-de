---
title: Maschine
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6c00f6067cd5f6cf741cddbd6d62c5bcbb1f37a9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361858"
---
# <a name="writer"></a>Maschine



Überprüft, ob ein Writer oder eine Komponente ein Writer oder eine Komponente aus dem Sicherungs-oder Wiederherstellungsverfahren enthält bzw. schließt. Bei Verwendung ohne Parameter zeigt **Writer** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

## <a name="parameters"></a>Parameter

| Parameter  |                                                                                      Beschreibung                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   verify   | Überprüft, ob der angegebene Writer oder die angegebene Komponente in der Sicherungs-oder Wiederherstellungs Prozedur enthalten ist. Die Sicherungs-oder Wiederherstellungs Prozedur schlägt fehl, wenn der Writer oder die Komponente nicht enthalten ist. |
|  exclude   |                                                   Schließt den angegebenen Writer oder die Komponente vom Sicherungs-oder Wiederherstellungsverfahren aus.                                                    |
| [\<writer > |                                                                                     <Component>]                                                                                      |

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um einen Writer zu überprüfen, indem Sie die GUID angeben (in diesem Beispiel 4dc3bdd4-AB48-4d07-adb0-3bee2926fd7f):
```
writer verify {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
```
Um einen Writer mit dem Namen "System Schreiber" auszuschließen, geben Sie Folgendes ein:
```
writer exclude "System Writer"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)