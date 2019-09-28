---
title: FTP-remotehelp_1
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: bac6fbe4a55c3fed4caab4e30ba848ec9ea68e21
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376026"
---
# <a name="ftp-remotehelp_1"></a>FTP: remotehelp_1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Hilfe für Remote Befehle an.   
## <a name="syntax"></a>Syntax  
```  
remotehelp [<Command>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|[<Command>]|Gibt den Namen des Befehls an, zu dem Sie Hilfe benötigen. Wenn der *Befehl* nicht angegeben wird, zeigt **FTP** eine Liste aller Remote Befehle an.|  
## <a name="remarks"></a>Hinweise  
Sie können Remote Befehle mithilfe von **Anführungs** Zeichen oder **literalen**ausführen.  
## <a name="BKMK_Examples"></a>Beispiele  
Zeigt eine Liste der Remote Befehle an.  
```  
remotehelp  
```  
Zeigt die Syntax für den Befehl " **feat** Remote" an.  
```  
remotehelp feat  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: Anführungszeichen](ftp-quote.md)  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
