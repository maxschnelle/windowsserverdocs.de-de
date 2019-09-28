---
title: Telnet-Sendevorgang
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 958e0e507e5a0ae836da98de8d677a116dbb38bd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383634"
---
# <a name="telnet-send"></a>Telnet: senden

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Telnet-Befehle an den Telnet-Server.   
## <a name="syntax"></a>Syntax  
```  
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]  
```  
### <a name="parameters"></a>Parameter  

| Parameter |                     Beschreibung                      |
|-----------|------------------------------------------------------|
|    OS     |       Sendet die Ausgabe des Telnet-Befehls abgebrochen.        |
|    AYT    |       Sendet den Telnet-Befehl.       |
|    BRK    |            Sendet den Telnet-Befehl BRK.            |
|    Dor    |      Sendet das aktuelle Telnet-Escapezeichen.      |
|    -     |     Sendet den Telnet-Befehls Unterbrechungs Prozess.     |
|   Synchronisierungs   |           Sendet den Telnet-Befehl "Synch".           |
| <string>  | Sendet jede Zeichenfolge, die Sie an den Telnet-Server eingeben. |
|     ?     |     Zeigt die diesem Befehl zugeordnete Hilfe an.      |

## <a name="BKMK_Examples"></a>Beispiele  
Senden Sie an den Telnet-Server.  
```  
sen ayt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
