---
title: Telnet geöffnet
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4528b728c89bbdfc99de94c7fefebb18c8e1ad97
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383653"
---
# <a name="telnet-open"></a>Telnet: offen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit einem Telnet-Server her.    
## <a name="syntax"></a>Syntax  
```  
o[pen] <hostname> [<Port>]  
```  
### <a name="parameters"></a>Parameter  

| Parameter  |                                        Beschreibung                                         |
|------------|--------------------------------------------------------------------------------------------|
| <hostname> |                         Gibt den Computernamen oder die IP-Adresse an.                         |
|  [<Port>]  | Gibt den TCP-Port an, an dem der Telnet-Server lauscht. Der Standardwert ist TCP-Port 23. |

## <a name="BKMK_Examples"></a>Beispiele  
Herstellen einer Verbindung mit einem Telnet-Server unter Telnet.Microsoft.com.  
```  
o telnet.microsoft.com  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
