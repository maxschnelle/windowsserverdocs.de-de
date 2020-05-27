---
title: goto
description: Referenz Thema für den GOTO-Befehl, bei dem "cmd. exe" an eine in einem Batch-Programm gekennzeichnete Zeile weitergeleitet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e0de1458-1f78-48ff-a746-c285a945a510
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1eb1b6b275887de535614fa5df4adabe33406a31
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818970"
---
# <a name="goto"></a>goto

Leitet "cmd. exe" an eine gekennzeichnete Zeile in einem Batch-Programm weiter. In einem Batch Programm leitet dieser Befehl die Befehls Verarbeitung an eine Zeile weiter, die durch eine Bezeichnung gekennzeichnet ist. Wenn die Bezeichnung gefunden wird, wird die Verarbeitung fortgesetzt, beginnend mit den Befehlen, die in der nächsten Zeile beginnen.

## <a name="syntax"></a>Syntax

```
goto <label>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<label>` | Gibt eine Text Zeichenfolge an, die im Batch Programm als Bezeichnung verwendet wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

-  Wenn Befehls Erweiterungen aktiviert sind (Standardeinstellung), und Sie den **goto** -Befehl mit der Ziel Bezeichnung **: EOF**verwenden, übertragen Sie die Steuerung an das Ende der aktuellen Batch Skriptdatei und beenden die Batch Skriptdatei, ohne eine Bezeichnung zu definieren. Wenn Sie diesen Befehl mit der Bezeichnung " **: EOF** " verwenden, müssen Sie vor der Bezeichnung einen Doppelpunkt einfügen. Beispiel: `goto:EOF`.

- Sie können Leerzeichen im *Label* -Parameter verwenden, aber Sie können keine anderen Trennzeichen (z. b. Semikolons (;) oder Gleichheitszeichen (=)).

- Der von Ihnen angegebene Bezeichnungs *Wert muss mit einer Bezeichnung im* Batch Programm identisch sein. Die Bezeichnung im Batch Programm muss mit einem Doppelpunkt (:) beginnen. Wenn eine Zeile mit einem Doppelpunkt beginnt, wird Sie als Bezeichnung behandelt, und alle Befehle in dieser Zeile werden ignoriert. Wenn das Batch Programm nicht die Bezeichnung enthält, die Sie im *Label* -Parameter angeben, wird das Batch Programm angehalten, und die folgende Meldung wird angezeigt: `Label not found` .

- Sie können " **goto** " mit anderen Befehlen verwenden, um bedingte Vorgänge auszuführen. Weitere Informationen zur Verwendung von **goto** für bedingte Vorgänge finden Sie im [if-Befehl](if.md).

## <a name="examples"></a>Beispiele

Das folgende Batch Programm formatiert einen Datenträger in Laufwerk a als System Datenträger. Wenn der Vorgang erfolgreich ist, leitet der **goto** -Befehl die Verarbeitung an die **: End** -Bezeichnung weiter:

```
echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program.
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [CMD-Befehl](cmd.md)

- [if-Befehl](if.md)