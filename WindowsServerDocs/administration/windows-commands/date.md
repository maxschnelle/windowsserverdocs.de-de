---
title: date
description: Windows-Befehls Thema für Date, das das Systemdatum anzeigt oder festlegt. Bei Verwendung ohne Parameter
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce6700fb-32f9-4350-a1af-5aee61d4448c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8f9e32240eb27d651e324becefd72e9b1a545215
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846743"
---
# <a name="date"></a>date

Zeigt das Systemdatum an oder legt es fest. Bei Verwendung ohne Parameter zeigt **Date** die aktuelle Einstellung für das Systemdatum an und fordert Sie auf, ein neues Datum einzugeben.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
date [/t | <Month-Day-Year>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Monat-Tag-Jahr >|Legt das angegebene Datum fest, wobei *Month* der Monat (eine oder zwei Ziffern), *Day* der Tag (eine oder zwei Ziffern) und *year* das Jahr (zwei oder vier Ziffern) ist.|
|/t|Zeigt das aktuelle Datum an, ohne Sie zur Eingabe eines neuen Datums aufzufordern.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn Sie das aktuelle Datum ändern möchten, müssen Sie über Administrator Anmelde Informationen verfügen.
-   Sie müssen Werte für " *Month*", " *Day*" und " *year* " durch Punkte (.), Bindestriche (-) oder Schrägstriche (/) aufteilen.
-   Gültige *Monats* Werte sind 1 bis 12.
-   Gültige *Tages* Werte liegen zwischen 1 und 31.
-   Gültige *Jahres* Werte sind entweder 00 bis 99, 1980 bis 2099. Wenn Sie zwei Ziffern verwenden, entsprechen die Werte 80 bis 99 den Jahren 1980 bis 1999.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Wenn Befehls Erweiterungen aktiviert sind, geben Sie Folgendes ein, um das aktuelle Systemdatum anzuzeigen:
```
date /t
```
Zum Ändern des aktuellen Systemdatums in den 3. August 2007 können Sie Folgendes eingeben:
```
date 08.03.2007
date 08-03-07
date 8/3/07
```
Um das aktuelle Systemdatum anzuzeigen, gefolgt von einer Eingabeaufforderung, um ein neues Datum einzugeben, geben Sie Folgendes ein:
```
The current date is: Mon 04/02/2007
Enter the new date: (mm-dd-yy)
```
Drücken Sie die EINGABETASTE, um das aktuelle Datum beizubehalten und zur Eingabeaufforderung zurückzukehren. Um das aktuelle Datum zu ändern, geben Sie das neue Datum ein, und drücken Sie dann die EINGABETASTE.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)