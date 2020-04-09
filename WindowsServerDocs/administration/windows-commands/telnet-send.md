---
title: Telnet-Sendevorgang
description: Windows-Befehls Thema für Telnet Send, das Telnet-Befehle an den Telnet-Server sendet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fef48ca04a3817f58d063bc8b23f5c11c4ea197
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833283"
---
# <a name="telnet-send"></a>Telnet: senden

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Telnet-Befehle an den Telnet-Server.   

## <a name="syntax"></a>Syntax  
```  
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]  
```  
#### <a name="parameters"></a>Parameter  

| Parameter |                     Beschreibung                      |
|-----------|------------------------------------------------------|
|    OS     |       Sendet die Ausgabe des Telnet-Befehls abgebrochen.        |
|    AYT    |       Sendet den Telnet-Befehl.       |
|    BRK    |            Sendet den Telnet-Befehl BRK.            |
|    Dor    |      Sendet das aktuelle Telnet-Escapezeichen.      |
|    -     |     Sendet den Telnet-Befehls Unterbrechungs Prozess.     |
|   synch   |           Sendet den Telnet-Befehl "Synch".           |
| <string>  | Sendet jede Zeichenfolge, die Sie an den Telnet-Server eingeben. |
|     ?     |     Zeigt die diesem Befehl zugeordnete Hilfe an.      |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Senden Sie an den Telnet-Server.  
```  
sen ayt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
