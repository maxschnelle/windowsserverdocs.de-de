---
title: time
description: Erfahren Sie, wie Sie die Systemzeit festlegen und anzeigen.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 484653ed65d5e5c16d74b2cb45b2c9da71aa62aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369953"
---
# <a name="time"></a>time



Zeigt die Systemzeit an oder legt Sie fest. Bei Verwendung ohne Parameter zeigt **Zeit** die aktuelle Systemzeit an und fordert Sie auf, einen neuen Zeitpunkt einzugeben.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
time [/t | [<HH>[:<MM>[:<SS>]] [am|pm]]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<HH > [: \<mm > [: \<SS > [. \<NN >]]] [am @ no__t-4pm]|Legt die Systemzeit auf die neue angegebene Uhrzeit fest, wobei *HH* in Stunden (erforderlich), *mm* in Minuten und *SS* in Sekunden angegeben wird. *NN* kann verwendet werden, um Hundertstel Sekunden anzugeben. Wenn **am** oder **pm** nicht angegeben ist, verwendet die **Zeit** standardmäßig das 24-Stunden-Format.|
|/t|Zeigt die aktuelle Zeit an, ohne Sie zur Eingabe eines neuen Zeitraums aufzufordern.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Zum Ändern der aktuellen Zeit müssen Sie über Administrator Anmelde Informationen verfügen.
-   Sie müssen die Werte für *HH*, *mm*und *SS* mit Doppelpunkten (:). *SS* und *NN* müssen durch einen Zeitraum (.) getrennt werden.
-   Gültige *HH* -Werte sind 0 bis 24.
-   Gültige *mm* -und *SS* -Werte sind 0 bis 59.

## <a name="BKMK_examples"></a>Beispiele

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

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)