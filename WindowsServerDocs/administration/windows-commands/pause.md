---
title: pause
description: Referenz Artikel für den anhaltebefehl, der die Verarbeitung von Batch-Programmen anhält.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cab3afc3-d046-432f-a0bf-6282f0099032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f604bbd205a074d8966cd2c1a1bc65506e7ca5e0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922900"
---
# <a name="pause"></a>pause

Hält die Verarbeitung eines Batch Programms an und zeigt die Eingabeaufforderung an.`Press any key to continue . . .`

## <a name="syntax"></a>Syntax

```
pause
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

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