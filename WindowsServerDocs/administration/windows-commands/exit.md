---
title: exit
description: Referenz Artikel zum Beenden, mit dem der Befehls Interpreter beendet wird.
ms.topic: reference
ms.assetid: d3cee4a2-6210-46f0-b8e4-7381c3c4e530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e065a25f339a093492a05102b10455b11da5ecb
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035858"
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
