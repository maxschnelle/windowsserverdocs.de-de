---
title: Zeit
description: Informationen Sie zum Festlegen und Anzeigen der Systemzeit.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1276a257-7283-41da-ae80-fb4cfb311f9d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b5c1f43be98a19c4b150c247cc7fd48d62edeb5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861911"
---
# <a name="time"></a>Zeit



Zeigt an, oder legt die Systemzeit. Wenn Sie ohne Angabe von Parametern **Zeit** zeigt die aktuelle Systemzeit, und fordert Sie auf eine neue Zeit einzugeben.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
time [/t | [<HH>[:<MM>[:<SS>]] [am|pm]]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<HH>[:\<MM>[:\<SS>[.\<NN>]]] [am\|pm]|Stellt die Systemzeit auf die neue Zeit angegeben, wobei *HH* wird in Stunden (erforderlich), *MM* wird in Minuten und *SS* wird in Sekunden angegeben. *NN* können verwendet werden, um die Hundertstelsekunden angeben. Wenn **bin** oder **Uhr** nicht angegeben ist, **Zeit** wird standardmäßig das 24-Stunden-Format verwendet.|
|/t|Die aktuelle Uhrzeit angezeigt, ohne dass Sie eine neue Zeit eingeben.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Um die aktuelle Uhrzeit zu ändern, müssen Sie die administrative Anmeldeinformationen verfügen.
-   Sie müssen die Werte für trennen *HH*, *MM*, und *SS* mit Doppelpunkten (:). *SS* und *NN* müssen mit einem Punkt (.) getrennt werden.
-   Gültige *HH* Werte sind 0 bis 24.
-   Gültige *MM* und *SS* Werte sind 0 bis 59.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie eine Falls befehlserweiterungen aktiviert sind, um die aktuelle Systemzeit, anzuzeigen:
```
time /t
```
Geben Sie eine der folgenden Schritte aus, um die aktuelle Systemzeit um 17:30 Uhr zu ändern:
```
time 17:30:00
time 5:30 pm
```
Geben Sie Folgendes ein, um die aktuelle Systemzeit, gefolgt von einer Aufforderung zur Eingabe der Zeit, anzuzeigen:
```
The current time is: 17:33:31.35
Enter the new time:
```
Um die aktuelle Uhrzeit und zur Eingabeaufforderung zurückzukehren, drücken Sie die EINGABETASTE. Um die aktuelle Uhrzeit zu ändern, geben Sie den neuen Zeitraum aus, und drücken Sie dann die EINGABETASTE.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)