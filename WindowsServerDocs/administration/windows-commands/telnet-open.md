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
ms.openlocfilehash: a87c4bac000a63af806705e9371a79d7370a34c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838241"
---
# <a name="telnet-open"></a>Telnet: Öffnen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Eine Verbindung mit einem Telnet-Server.    
## <a name="syntax"></a>Syntax  
```  
o[pen] <hostname> [<Port>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<hostname>|Gibt den Computernamen oder IP-Adresse.|  
|[<Port>]|Gibt den TCP-Port, dem der Telnet-Server überwacht. Der Standardwert ist die TCP-Port 23.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Verbinden Sie mit einem Telnetserver telnet.microsoft.com.  
```  
o telnet.microsoft.com  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
