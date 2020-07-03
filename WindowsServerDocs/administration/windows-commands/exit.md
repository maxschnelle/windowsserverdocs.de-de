---
title: exit
description: Referenz Artikel zum Beenden, mit dem der Befehls Interpreter beendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3cee4a2-6210-46f0-b8e4-7381c3c4e530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d28f15ba1453b32d8e464fd768a3b7895819d11c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931448"
---
# <a name="exit"></a>exit

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet den Befehls Interpreter oder das aktuelle Batch Skript.

## <a name="syntax"></a>Syntax

```
exit [/b] [<exitcode>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /b | Beendet das aktuelle Batch Skript, anstatt Cmd.exe zu beenden. Wenn Sie von außerhalb eines Batch Skripts ausgeführt wird, wird Cmd.exe beendet. |
| `<exitcode>` | Gibt eine numerische Zahl an. Wenn **/b** angegeben wird, wird die ERRORLEVEL-Umgebungsvariable auf diese Zahl festgelegt. Wenn Sie den Befehls Interpreter verlassen, wird der Prozessexitcode auf diese Zahl festgelegt. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Befehls Interpreter zu schließen:

```
exit
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
