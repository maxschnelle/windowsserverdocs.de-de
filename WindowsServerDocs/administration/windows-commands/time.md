---
title: time
description: Referenz Artikel zum Zeit Befehl, mit dem die Systemzeit angezeigt oder festgelegt wird.
ms.topic: reference
ms.assetid: 1276a257-7283-41da-ae80-fb4cfb311f9d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b69db2fce1af52d8f284e79fe83f5ac20c398cd6
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156475"
---
# <a name="time"></a>time

Zeigt die Systemzeit an oder legt Sie fest. Bei Verwendung ohne Parameter zeigt **Zeit** die aktuelle Systemzeit an und fordert Sie auf, einen neuen Zeitpunkt einzugeben.

> [!NOTE]
> Sie müssen ein Administrator sein, um die aktuelle Zeit ändern zu können.

## <a name="syntax"></a>Syntax

```
time [/t | [<HH>[:<MM>[:<SS>]] [am|pm]]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<HH>[:<MM>[:<SS>[.<NN>]]] [am | pm]` | Legt die Systemzeit auf die neue angegebene Uhrzeit fest, wobei *HH* in Stunden (erforderlich), *mm* in Minuten und *SS* in Sekunden angegeben wird. *NN* kann verwendet werden, um Hundertstel Sekunden anzugeben. Sie müssen die Werte für *HH*, *mm*und *SS* mit Doppelpunkten (:). *SS* und *NN* müssen durch einen Zeitraum (.) getrennt werden.<p>Wenn **am** oder **pm** nicht angegeben ist, verwendet die **Zeit** standardmäßig das 24-Stunden-Format. |
| /t | Zeigt die aktuelle Zeit an, ohne Sie zur Eingabe eines neuen Zeitraums aufzufordern. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Gültige *HH* -Werte sind 0 bis 24.

- Gültige *mm* -und *SS* -Werte sind 0 bis 59.

## <a name="examples"></a>Beispiele

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
