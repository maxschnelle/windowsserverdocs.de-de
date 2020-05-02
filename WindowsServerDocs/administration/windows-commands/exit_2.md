---
title: exit
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 23d1044b-f5c1-4180-ae6d-f553b48da4d9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e47dfa42f2bacb3fe9f12d1da9163bcf828e9488
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725707"
---
# <a name="exit"></a>exit

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet das Programm "cmd. exe" (der Befehls Interpreter) oder das aktuelle Batch Skript.  
  
## <a name="syntax"></a>Syntax  
```  
exit [/b] [<exitCode>]  
```  
### <a name="parameters"></a>Parameter  

| Parameter  |                                                                                         BESCHREIBUNG                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      Beendet das aktuelle Batch Skript, anstatt "cmd. exe" zu beenden. Wenn die Ausführung von außerhalb eines Batch Skripts erfolgt, wird "cmd. exe" beendet.                                      |
| `<exitCode>` | Gibt eine numerische Zahl an. Wenn **/b** angegeben wird, wird die ERRORLEVEL-Umgebungsvariable auf diese Zahl festgelegt. Wenn Sie " **cmd. exe**" beenden, wird der Prozessexitcode auf diese Zahl festgelegt. |
|     /?     |                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                             |

## <a name="examples"></a>Beispiele  
Zum Schließen des Befehls Interpreters, cmd. exe, geben Sie Folgendes ein:  
```  
exit  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  

