---
title: FTP-literal_1
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fc4f8aff5a22da93330a12a75e5f368285366216
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725256"
---
# <a name="ftp-literal_1"></a>FTP: literal_1

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 sendet ausführliche Argumente an den Remote-FTP-Server. Ein einzelner FTP-Antwort Code wird zurückgegeben.   

## <a name="syntax"></a>Syntax  
```  
literal <Argument> [ ]  
```  
#### <a name="parameters"></a>Parameter  

| Parameter  |                    BESCHREIBUNG                    |
|------------|---------------------------------------------------|
| <Argument> | Gibt das Argument an, das an den FTP-Server gesendet werden soll. |

## <a name="remarks"></a>Bemerkungen  
Der **literalbefehl** ist identisch mit dem **Anführungs** Zeichen Befehl.  
## <a name="examples"></a>Beispiele  
Senden Sie einen Befehl zum **Beenden** an den FTP-Remote Server.  
```  
literal quit  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [FTP: Anführungszeichen](ftp-quote.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
