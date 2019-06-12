---
title: Telnet öffnen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 186664a75978f589a9a26047c72b9db74dd2dc4d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441126"
---
# <a name="telnet-open"></a>Telnet: Öffnen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Eine Verbindung mit einem Telnet-Server.    
## <a name="syntax"></a>Syntax  
```  
o[pen] <hostname> [<Port>]  
```  
### <a name="parameters"></a>Parameter  

| Parameter  |                                        Beschreibung                                         |
|------------|--------------------------------------------------------------------------------------------|
| <hostname> |                         Gibt den Computernamen oder IP-Adresse.                         |
|  [<Port>]  | Gibt den TCP-Port, dem der Telnet-Server überwacht. Der Standardwert ist die TCP-Port 23. |

## <a name="BKMK_Examples"></a>Beispiele für  
Verbinden Sie mit einem Telnetserver telnet.microsoft.com.  
```  
o telnet.microsoft.com  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
