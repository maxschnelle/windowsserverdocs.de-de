---
title: pause
description: Referenz Artikel für den anhaltebefehl, der die Verarbeitung von Batch-Programmen anhält.
ms.topic: reference
ms.assetid: cab3afc3-d046-432f-a0bf-6282f0099032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0da314b5b73935fa895b613b827f832492428cc7
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032477"
---
# <a name="pause"></a>pause

Hält die Verarbeitung eines Batch Programms an und zeigt die Eingabeaufforderung an. `Press any key to continue . . .`

## <a name="syntax"></a>Syntax

```
pause
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Bemerkungen

- Wenn Sie STRG + C drücken, um ein Batch-Programm anzuhalten, wird die folgende Meldung angezeigt: `Terminate batch job (Y/N)?` . Wenn Sie als Antwort auf diese Meldung **Y** (für ja) drücken, wird das Batch Programm beendet, und die Steuerung wird an das Betriebssystem zurückgegeben.

- Sie können den Befehl **Pause** vor einem Abschnitt der Batchdatei einfügen, den Sie möglicherweise nicht verarbeiten möchten. Wenn **Anhalten** die Verarbeitung des Batch Programms anhält, können Sie STRG + C drücken und dann **Y** drücken, um das Batch Programm zu beenden.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Batch-Programm zu erstellen, das den Benutzer auffordert, Datenträger auf einem der Laufwerke zu ändern:

```
@echo off
:Begin
copy a:*.*
echo Put a new disk into Drive A
pause
goto begin
```

In diesem Beispiel werden alle Dateien auf dem Datenträger in Laufwerk A in das aktuelle Verzeichnis kopiert. Nachdem Sie in der Meldung aufgefordert werden, einen neuen Datenträger in Laufwerk a einzufügen, hält der **Pause** -Befehl die Verarbeitung an, sodass Sie die Datenträger ändern und dann eine beliebige Taste drücken können, um die Verarbeitung fortzusetzen. Dieses Batch-Programm wird in einer Endlosschleife ausgeführt – der Befehl Gehe **zu Begin** sendet den Befehls Interpreter an die BEGIN-Bezeichnung der Batchdatei.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)