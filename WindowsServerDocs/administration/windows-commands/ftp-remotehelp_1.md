---
title: FTP-remotehelp_1
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc4affb3f04eadaa4e0005e5edce0f564156f64a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725135"
---
# <a name="ftp-remotehelp_1"></a>FTP: remotehelp_1

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Hilfe für Remote Befehle an.   
## <a name="syntax"></a>Syntax  
```  
remotehelp [<Command>]  
```  
#### <a name="parameters"></a>Parameter  
|Parameter|BESCHREIBUNG|  
|-------|--------|  
|[<Command>]|Gibt den Namen des Befehls an, zu dem Sie Hilfe benötigen. Wenn der *Befehl* nicht angegeben wird, zeigt **FTP** eine Liste aller Remote Befehle an.|  
## <a name="remarks"></a>Bemerkungen  
Sie können Remote Befehle mithilfe von **Anführungs** Zeichen oder **literalen**ausführen.  
## <a name="examples"></a>Beispiele  
Zeigt eine Liste der Remote Befehle an.  
```  
remotehelp  
```  
Zeigt die Syntax für den Befehl " **feat** Remote" an.  
```  
remotehelp feat  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [FTP: Anführungszeichen](ftp-quote.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
