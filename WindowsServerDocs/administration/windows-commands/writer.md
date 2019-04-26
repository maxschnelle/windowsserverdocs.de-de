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
ms.openlocfilehash: 87b10952c6a851b5536a1589b994b265e8699f59
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826401"
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
Auszuschließende Autor mit dem Namen "Systemgenerator? Typ:
```
writer exclude "System Writer"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)