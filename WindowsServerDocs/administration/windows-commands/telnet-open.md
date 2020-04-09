---
title: Telnet geöffnet
description: Windows-Befehls Thema für Telnet Open, das eine Verbindung mit einem Telnet-Server herstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b100d2b53a340a083f22d4fd88c42363642d5da5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833333"
---
# <a name="telnet-open"></a>Telnet: offen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit einem Telnet-Server her.    

## <a name="syntax"></a>Syntax  
```  
o[pen] <hostname> [<Port>]  
```  
#### <a name="parameters"></a>Parameter  

| Parameter  |                                        Beschreibung                                         |
|------------|--------------------------------------------------------------------------------------------|
| <hostname> |                         Gibt den Computernamen oder die IP-Adresse an.                         |
|  [<Port>]  | Gibt den TCP-Port an, an dem der Telnet-Server lauscht. Der Standardwert ist TCP-Port 23. |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Herstellen einer Verbindung mit einem Telnet-Server unter Telnet.Microsoft.com.  
```  
o telnet.microsoft.com  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
