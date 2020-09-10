---
title: time
description: Erfahren Sie, wie Sie die Systemzeit festlegen und anzeigen.
ms.topic: reference
ms.assetid: 1276a257-7283-41da-ae80-fb4cfb311f9d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4faa12cef8485be6b76b16ff2ab545d0eae06cb7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640447"
---
# <a name="time"></a>time



Zeigt die Systemzeit an oder legt Sie fest. Bei Verwendung ohne Parameter zeigt **Zeit** die aktuelle Systemzeit an und fordert Sie auf, einen neuen Zeitpunkt einzugeben.



## <a name="syntax"></a>Syntax

```
time [/t | [<HH>[:<MM>[:<SS>]] [am|pm]]]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<HH>[:\<MM> [:\<SS> [.\<NN>]]] [am \| pm]|Legt die Systemzeit auf die neue angegebene Uhrzeit fest, wobei *HH* in Stunden (erforderlich), *mm* in Minuten und *SS* in Sekunden angegeben wird. *NN* kann verwendet werden, um Hundertstel Sekunden anzugeben. Wenn **am** oder **pm** nicht angegeben ist, verwendet die **Zeit** standardmäßig das 24-Stunden-Format.|
|/t|Zeigt die aktuelle Zeit an, ohne Sie zur Eingabe eines neuen Zeitraums aufzufordern.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Zum Ändern der aktuellen Zeit müssen Sie über Administrator Anmelde Informationen verfügen.
-   Sie müssen die Werte für *HH*, *mm*und *SS* mit Doppelpunkten (:). *SS* und *NN* müssen durch einen Zeitraum (.) getrennt werden.
-   Gültige *HH* -Werte sind 0 bis 24.
-   Gültige *mm* -und *SS* -Werte sind 0 bis 59.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele

Wenn Befehls Erweiterungen aktiviert sind, geben Sie Folgendes ein, um die aktuelle Systemzeit anzuzeigen:
```
time /t
```
Um die aktuelle Systemzeit auf 5:30 Uhr zu ändern, geben Sie eine der folgenden Optionen ein:
```
time 17:30:00
time 5:30 pm
```
Geben Sie Folgendes ein, um die aktuelle Systemzeit, gefolgt von einer Eingabeaufforderung zur Eingabe eines neuen Zeitraums, anzuzeigen:
```
The current time is: 17:33:31.35
Enter the new time:
```
Drücken Sie die EINGABETASTE, um die aktuelle Uhrzeit beizubehalten und zur Eingabeaufforderung zurückzukehren. Um die aktuelle Uhrzeit zu ändern, geben Sie die neue Uhrzeit ein, und drücken Sie dann die EINGABETASTE.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)