---
title: exit
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4e599f84389b23e527e3718a620d5fdfefe24edb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439461"
---
# <a name="exit"></a>exit

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Beenden das Cmd.exe-Programm (den Befehlsinterpreter) oder das aktuelle Batchskript.  
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).  
## <a name="syntax"></a>Syntax  
```  
exit [/b] [<exitCode>]  
```  
## <a name="parameters"></a>Parameter  

| Parameter  |                                                                                         Beschreibung                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      beendet das aktuelle Batchskript anstelle von Cmd.exe beendet wird. Wenn Sie von außerhalb einer Batchdatei ausgeführt wird, wird die Cmd.exe beendet.                                      |
| <exitCode> | Gibt einen numerischen Wert an. Wenn **/b** angegeben wird, um die Anzahl der Umgebungsvariablen ERRORLEVEL festgelegt ist. Wenn Sie beenden werden **Cmd.exe**, Exitcode des Prozesses mit dieser Zahl festgelegt ist. |
|     /?     |                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                             |

## <a name="BKMK_examples"></a>Beispiele für  
Geben Sie Folgendes ein, um den Befehlsinterpreter, Cmd.exe zu schließen:  
```  
exit  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  

