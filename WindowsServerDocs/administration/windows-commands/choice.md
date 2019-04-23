---
title: choice
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c65a9119-410b-4dcf-9fa7-4e07d2a7238b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78d2816bff754ef04558cf37eaada7c7fafba823
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841551"
---
# <a name="choice"></a>choice



Fordert den Benutzer auf ein Element aus einer Liste von Optionen der einzelnen Zeichen in einem Batchprogramm auswählen, und gibt dann den Index der getroffenen Auswahl zurück. Wenn Sie ohne Angabe von Parametern **Wahl** zeigt die Standardoptionen **Y** und **N**.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
choice [/c [<Choice1><Choice2><…>]] [/n] [/cs] [/t <Timeout> /d <Choice>] [/m <"Text">]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ c \<Choice1 ><Choice2><... >|Gibt die Liste von Optionen, die erstellt werden. Gültige Optionen sind a – Z, A-Z, 0-9 und erweiterten ASCII-Zeichen (128-254). Die Standardliste ist "YN", die angezeigt wird, als `[Y,N]?`.|
|/n|Blendet Sie aus der Liste der Optionen, jedoch immer noch die Auswahlmöglichkeiten aktiviert sind und der Nachrichtentext (angegeben durch **/m**) wird weiterhin angezeigt.|
|/cs|Gibt an, dass die Optionen Groß-/Kleinschreibung beachtet. Standardmäßig sind die Optionen nicht Groß-/Kleinschreibung beachtet.|
|/ t / \<Timeout >|Gibt die Anzahl der Sekunden anhalten, bevor Sie die Standardauswahl durch angegeben mit **/d**. Gültige Werte liegen zwischen **0** zu **9999**. Wenn **/t /** nastaven NA hodnotu **0**, **Wahl** wird nicht unterbrochen werden, vor der Rückgabe der Standardauswahl.|
|/ d \<Wahl >|Gibt an, die Standardauswahl, verwenden Sie nach einer Wartezeit auf die Anzahl der Sekunden, die anhand des **/t /**. Die Standardauswahl muss in der Liste der Optionen, die anhand des **/c**.|
|/m <"Text">|Gibt eine Meldung, der vor der Liste der Optionen angezeigt. Wenn **/m** nicht angegeben ist, wird nur die Option Eingabeaufforderung wird angezeigt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Auf den Index des Schlüssels, die aus der Liste der Optionen der Benutzer auswählt, wird der Umgebungsvariablen ERRORLEVEL festgelegt. Die erste Wahl in der Liste gibt einen Wert von 1 und der zweite Wert 2 usw. zurück. Wenn der Benutzer eine Taste drückt, die nicht auf eine gültige Auswahl ist, ist **Wahl** akustisches Signal. Wenn **Wahl** eine fehlerbedingung erkennt wird einen ERRORLEVEL-Wert von 255 aufweisen. Wenn der Benutzer STRG + UNTBR oder STRG + C drückt **Wahl** einen ERRORLEVEL-Wert 0 zurückgegeben.

> [!NOTE]
> Wenn Sie die ERRORLEVEL-Werte in einem Batchprogramm verwenden, in absteigender Reihenfolge auflisten.

## <a name="BKMK_examples"></a>Beispiele für

Um die Auswahlmöglichkeiten, Y, N und C vorhanden ist, geben Sie die folgende Zeile in einer Batchdatei aus:
```
choice /c ync
```
Die folgende Aufforderung angezeigt wird, wenn die Batchdatei ausgeführt wird. die **Wahl** Befehl:
```
[Y,N,C]?
```
Die Auswahlmöglichkeiten, Y, N und C ausblenden, sondern zeigt den Text "Ja, Nein oder Continue", geben Sie die folgende Zeile in einer Batchdatei:
```
choice /c ync /n /m "Yes, No, or Continue?"
```
Die folgende Aufforderung angezeigt wird, wenn die Batchdatei ausgeführt wird. die **Wahl** Befehl:
```
Yes, No, or Continue?
```

> [!NOTE]
> Bei Verwendung der **/n** -Parameter verwenden Sie jedoch nicht **/m**, der Benutzer ist nicht dazu aufgefordert werden, wenn **Wahl** darauf wartet, Input.

Um sowohl das Text-als auch die Optionen, die in den vorherigen Beispielen verwendete anzuzeigen, geben Sie die folgende Zeile in einer Batchdatei aus:
```
choice /c ync /m "Yes, No, or Continue"
```
Die folgende Aufforderung angezeigt wird, wenn die Batchdatei ausgeführt wird. die **Wahl** Befehl:
```
Yes, No, or Continue [Y,N,C]?
```
Zum Festlegen eines Zeitlimits von fünf Sekunden, und geben Sie **N** als den Standardwert, geben Sie die folgende Zeile in einer Batchdatei:
```
choice /c ync /t 5 /d n
```
Die folgende Aufforderung angezeigt wird, wenn die Batchdatei ausgeführt wird. die **Wahl** Befehl:
```
[Y,N,C]?
```

> [!NOTE]
> In diesem Beispiel, wenn der Benutzer einen Schlüssel innerhalb von fünf Sekunden keine Taste **Wahl** wählt **N** standardmäßig und gibt einen Fehlerwert 2 zurück. Andernfalls **Wahl** gibt den Wert für die Auswahl des Benutzers zurück.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)