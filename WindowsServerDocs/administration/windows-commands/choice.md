---
title: choice
description: Referenz Artikel für den Choice-Befehl, der den Benutzer auffordert, ein Element aus einer Liste von Einzelzeichen in einem Batch Programm auszuwählen, und dann den Index der ausgewählten Auswahl zurückgibt.
ms.topic: reference
ms.assetid: c65a9119-410b-4dcf-9fa7-4e07d2a7238b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 382e3618e66f56e05ebd0a7d6b6034e6d7543d64
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629680"
---
# <a name="choice"></a>choice

Fordert den Benutzer auf, ein Element aus einer Liste von Einzelzeichen in einem Batch Programm auszuwählen, und gibt dann den Index der ausgewählten Auswahl zurück. Wenn die Option ohne Parameter verwendet **wird, werden** die Standardoptionen **Y** und **N**angezeigt.

## <a name="syntax"></a>Syntax

```
choice [/c [<choice1><choice2><…>]] [/n] [/cs] [/t <timeout> /d <choice>] [/m <text>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /c `<choice1><choice2><…>` | Gibt die Liste der zu erstellenden Optionen an. Gültige Optionen sind a-z, a-z, 0-9 und erweiterte ASCII-Zeichen (128-254). Die Standardliste ist yn, das als angezeigt wird `[Y,N]?` . |
| /n | Blendet die Liste der Auswahlmöglichkeiten aus, obwohl die Auswahl weiterhin aktiviert ist und der Meldungs Text (falls durch **/m**angegeben) weiterhin angezeigt wird. |
| /CS | Gibt an, dass die Groß-/Kleinschreibung beachtet werden soll. Standardmäßig wird die Groß-/Kleinschreibung nicht beachtet. |
| /t `<timeout>` | Gibt die Anzahl der Sekunden an, die angehalten werden soll, bevor die von **/d**angegebene Standardauswahl verwendet wird. Zulässige Werte liegen zwischen **0** und **9999**. Wenn **/t** auf **0**festgelegt ist, wird die **Auswahl** nicht angehalten, bevor die Standardauswahl zurückgegeben wird. |
| /d `<choice>` | Gibt die Standardauswahl an, die nach der Wartezeit der von **/t**angegebenen Anzahl von Sekunden verwendet werden soll. Die Standardauswahl muss in der Liste der von **/c**angegebenen Optionen stehen. |
| /m `<text>` | Gibt eine Meldung an, die vor der Auswahlliste angezeigt werden soll. Wenn **/m** nicht angegeben ist, wird nur die Auswahl Aufforderung angezeigt. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

- Die **ERRORLEVEL** -Umgebungsvariable wird auf den Index des Schlüssels festgelegt, den der Benutzer aus der Liste der Optionen auswählt. Die erste Auswahl in der Liste gibt den Wert zurück `1` , der zweite Wert von `2` usw. Wenn der Benutzer eine Taste drückt, bei der es sich nicht um eine gültige Auswahl handelt, wird von der **Auswahl** eine Warnung angezeigt.

- Wenn **Choice** eine Fehlerbedingung erkennt, wird der **ERRORLEVEL** -Wert zurückgegeben `255` . Wenn der Benutzer STRG + Pause oder STRG + C drückt, gibt **Choice** einen **ERRORLEVEL** -Wert von zurück `0` .

> [!NOTE]
> Wenn Sie **ERRORLEVEL** -Werte in einem Batch-Programm verwenden, müssen Sie Sie in absteigender Reihenfolge auflisten.

## <a name="examples"></a>Beispiele

Geben Sie die folgende Zeile in eine Batchdatei ein, um die Optionen **Y**, **N**und **C**anzuzeigen:

```
choice /c ync
```

Wenn die Batchdatei den Befehl " **Choice** " ausführt, wird die folgende Eingabeaufforderung angezeigt:

```
[Y,N,C]?
```

Um die Optionen **Y**, **N**und **C**auszublenden, aber den Text **Yes**, **No**oder **Continue**anzuzeigen, geben Sie die folgende Zeile in einer Batchdatei ein:

```
choice /c ync /n /m Yes, No, or Continue?
```

> [!NOTE]
> Wenn Sie den **/n** -Parameter verwenden, ohne jedoch **/m**zu verwenden, wird der Benutzer nicht aufgefordert, wenn die **Auswahl** auf Eingaben wartet.

Wenn Sie sowohl den Text als auch die in den vorherigen Beispielen verwendeten Optionen anzeigen möchten, geben Sie die folgende Zeile in einer Batchdatei ein:

```
choice /c ync /m Yes, No, or Continue
```

Wenn Sie ein Zeit Limit von fünf Sekunden festlegen und **N** als Standardwert angeben möchten, geben Sie die folgende Zeile in einer Batchdatei ein:

```
choice /c ync /t 5 /d n
```

> [!NOTE]
> Wenn der Benutzer in diesem Beispiel nicht innerhalb von fünf Sekunden eine Taste drückt, wählt **Choice** standardmäßig **N** aus und gibt einen Fehlerwert von zurück `2` . Andernfalls gibt **Choice** den Wert zurück, der der Auswahl des Benutzers entspricht.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
