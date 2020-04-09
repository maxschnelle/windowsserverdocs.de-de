---
title: exit
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 23d1044b-f5c1-4180-ae6d-f553b48da4d9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13cf7a7658394e59ce6cc7e66c3083cd3d359574
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844883"
---
# <a name="exit"></a>exit

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet das Programm "cmd. exe" (der Befehls Interpreter) oder das aktuelle Batch Skript.  
Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).  
## <a name="syntax"></a>Syntax  
```  
exit [/b] [<exitCode>]  
```  
### <a name="parameters"></a>Parameter  

| Parameter  |                                                                                         Beschreibung                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      Beendet das aktuelle Batch Skript, anstatt "cmd. exe" zu beenden. Wenn die Ausführung von außerhalb eines Batch Skripts erfolgt, wird "cmd. exe" beendet.                                      |
| `<exitCode>` | Gibt eine numerische Zahl an. Wenn **/b** angegeben wird, wird die ERRORLEVEL-Umgebungsvariable auf diese Zahl festgelegt. Wenn Sie " **cmd. exe**" beenden, wird der Prozessexitcode auf diese Zahl festgelegt. |
|     /?     |                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                             |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Zum Schließen des Befehls Interpreters, cmd. exe, geben Sie Folgendes ein:  
```  
exit  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  

