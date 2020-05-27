---
title: exit
description: Referenz Thema für Exit, mit dem der Befehls Interpreter beendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3cee4a2-6210-46f0-b8e4-7381c3c4e530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fdfec9861e63f7484a9c45c45a22d19873cabbe9
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819500"
---
# <a name="exit"></a>exit

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet den Befehls Interpreter oder das aktuelle Batch Skript.

## <a name="syntax"></a>Syntax

```
exit [/b] [<exitcode>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /b | Beendet das aktuelle Batch Skript, anstatt "cmd. exe" zu beenden. Wenn die Ausführung von außerhalb eines Batch Skripts erfolgt, wird "cmd. exe" beendet. |
| `<exitcode>` | Gibt eine numerische Zahl an. Wenn **/b** angegeben wird, wird die ERRORLEVEL-Umgebungsvariable auf diese Zahl festgelegt. Wenn Sie den Befehls Interpreter verlassen, wird der Prozessexitcode auf diese Zahl festgelegt. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Befehls Interpreter zu schließen:

```
exit
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
