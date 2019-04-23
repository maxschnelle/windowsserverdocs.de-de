---
title: date
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce6700fb-32f9-4350-a1af-5aee61d4448c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e774f7bfabb9b574255691dd97d2cfff36f034e7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877951"
---
# <a name="date"></a>date



Zeigt an, oder legt das Systemdatum. Wenn Sie ohne Angabe von Parametern **Datum** zeigt das aktuelle Datum festgelegt, und fordert Sie auf ein neues Datum einzugeben.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
date [/t | <Month-Day-Year>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Monat-Tag-Jahr >|Legt diese fest, in dem des Datums angegeben wird, *Monat* ist der Monat (ein oder zwei Ziffern), *Tag* ist der Tag (ein oder zwei Ziffern), und *Jahr* ist das Jahr (zwei oder vier Ziffern).|
|/t|Das aktuelle Datum angezeigt, ohne dass Sie ein neues Datum eingeben.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Um das aktuelle Datum zu ändern, müssen Sie die administrative Anmeldeinformationen verfügen.
-   Sie müssen die Werte für trennen *Monat*, *Tag*, und *Jahr* durch Punkte (.), Bindestriche (-) oder einen Schrägstrich (/) markiert.
-   Gültige *Monat* Werte sind 1 bis 12.
-   Gültige *Tag* Werte sind 1 bis 31.
-   Gültige *Jahr* Werte sind entweder 00 bis 99 oder 1980 und 2099. Bei Verwendung von zwei Ziffern entsprechen die Werten 80 bis 99 der Jahre 1980-1999.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Wenn befehlserweiterungen aktiviert sind, um das aktuelle Systemdatum anzuzeigen:
```
date /t
```
Um das aktuelle Datum in 3 August 2007 zu ändern, können Sie Folgendes eingeben:
```
date 08.03.2007
date 08-03-07
date 8/3/07
```
Geben Sie zum Anzeigen des aktuellen Systemdatums, gefolgt von aufgefordert, ein neues Datum aus, geben Folgendes ein:
```
The current date is: Mon 04/02/2007
Enter the new date: (mm-dd-yy)
```
Um das aktuelle Datum und zur Eingabeaufforderung zurückzukehren, drücken Sie die EINGABETASTE. Um das aktuelle Datum zu ändern, geben Sie das neue Datum aus, und drücken Sie dann die EINGABETASTE.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)