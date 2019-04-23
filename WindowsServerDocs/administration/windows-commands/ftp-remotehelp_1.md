---
title: FTP-remotehelp_1
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd64af157f7ce05330cdafe6e4db6787fa765859
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889591"
---
# <a name="ftp-remotehelp1"></a>FTP: remotehelp_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt die Hilfe für remote-Befehle.   
## <a name="syntax"></a>Syntax  
```  
remotehelp [<Command>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|[<Command>]|Gibt den Namen des Befehls dazu, welche Sie Hilfe benötigen. Wenn *Befehl* nicht angegeben ist, **ftp** zeigt eine Liste von allen Remotebefehlen.|  
## <a name="remarks"></a>Hinweise  
Ausführen von Remotebefehlen, die mit **Anführungszeichen** oder **literal**.  
## <a name="BKMK_Examples"></a>Beispiele für  
Eine Liste der Remotebefehle angezeigt.  
```  
remotehelp  
```  
Zeigt die Syntax für die **Feat** Remotebefehle ausführen.  
```  
remotehelp feat  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [ftp: quote](ftp-quote.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
