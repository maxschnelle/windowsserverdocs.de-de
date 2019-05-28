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
ms.openlocfilehash: 94be02aa25867845436b83d052c4990ff9212975
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564681"
---
# <a name="writer"></a>Writer



Überprüft, ob ein Writer oder eine Komponente enthalten ist oder ein Writer oder eine Komponente aus der Sicherung oder Wiederherstellung Prozedur schließt. Wenn Sie ohne Angabe von Parametern **Writer** zeigt die Hilfe an der Eingabeaufforderung.

## <a name="syntax"></a>Syntax

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|verify|Stellt sicher, dass die angegebenen Writer oder die Komponente in der Backup- oder Restore-Prozedur enthalten ist. Die Backup- oder Restore-Prozedur schlägt fehl, wenn der Writer oder die Komponente nicht enthalten ist.|
|exclude|Schließt die angegebenen Writer oder die Komponente aus der Backup- oder Restore-Prozedur aus.|
|[\<Writer> | <Component>]|Gibt an, der Writer oder die Komponente, um zu überprüfen oder ausschließen. Autoren werden vom Autor GUID oder den Namen der Writer, z. B. "Systemgenerator." angegeben.|

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