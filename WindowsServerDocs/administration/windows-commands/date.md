---
title: date
description: Referenz Artikel zum Date-Befehl, mit dem das Systemdatum angezeigt oder festgelegt wird. Bei Verwendung ohne Parameter
ms.topic: reference
ms.assetid: ce6700fb-32f9-4350-a1af-5aee61d4448c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78c8ca51882b2559e78cc457d1fd7fa5ec8e87b8
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033038"
---
# <a name="date"></a>date

Zeigt das Systemdatum an oder legt es fest. Bei Verwendung ohne Parameter zeigt **Date** die aktuelle Einstellung für das Systemdatum an und fordert Sie auf, ein neues Datum einzugeben.

>[!IMPORTANT]
> Sie müssen ein Administrator sein, um diesen Befehl verwenden zu können.

## <a name="syntax"></a>Syntax

```
date [/t | <month-day-year>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<month-day-year>` | Legt das angegebene Datum fest, wobei *Month* der Monat ist (eine oder zwei Ziffern, einschließlich der Werte 1 bis 12), *Day* der Tag (eine oder zwei Ziffern, einschließlich der Werte 1 bis 31) und *year* das Jahr (zwei oder vier Ziffern, einschließlich der Werte 00 bis 99 oder 1980 bis 2099). Sie müssen Werte für " *Month*", " *Day*" und " *year* " durch Punkte (.), Bindestriche (-) oder Schrägstriche (/) aufteilen.<p>**Hinweis:** Beachten Sie, dass bei Verwendung von 2 Ziffern zur Darstellung des Jahres die Werte 80-99 1980 bis 1999 entsprechen. |
| /t | Zeigt das aktuelle Datum an, ohne Sie zur Eingabe eines neuen Datums aufzufordern. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

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
Enter the new date: (mm-dd-yyyy)
```

Drücken **Sie die Eingabe**Taste, um das aktuelle Datum beizubehalten und zur Eingabeaufforderung zurückzukehren. Um das aktuelle Datum zu ändern, geben Sie das neue Datum ein, und drücken Sie dann die **Eingabe**Taste.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)