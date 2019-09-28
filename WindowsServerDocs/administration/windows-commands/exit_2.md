---
title: exit
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23d1044b-f5c1-4180-ae6d-f553b48da4d9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 105bf572c1ebeb37ea59ff8bc5c04121d2442341
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377350"
---
# <a name="exit"></a>exit

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

beendet das Programm "cmd. exe" (der Befehls Interpreter) oder das aktuelle Batch Skript.  
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).  
## <a name="syntax"></a>Syntax  
```  
exit [/b] [<exitCode>]  
```  
## <a name="parameters"></a>Parameter  

| Parameter  |                                                                                         Beschreibung                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      beendet das aktuelle Batch Skript, anstatt "cmd. exe" zu beenden. Wenn die Ausführung von außerhalb eines Batch Skripts erfolgt, wird "cmd. exe" beendet.                                      |
| <exitCode> | Gibt eine numerische Zahl an. Wenn **/b** angegeben wird, wird die ERRORLEVEL-Umgebungsvariable auf diese Zahl festgelegt. Wenn Sie " **cmd. exe**" beenden, wird der Prozessexitcode auf diese Zahl festgelegt. |
|     /?     |                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                             |

## <a name="BKMK_examples"></a>Beispiele  
Zum Schließen des Befehls Interpreters, cmd. exe, geben Sie Folgendes ein:  
```  
exit  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  

