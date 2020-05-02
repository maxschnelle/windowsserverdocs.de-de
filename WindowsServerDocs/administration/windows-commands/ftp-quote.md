---
title: FTP-Anführungszeichen
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1101dd6a5fa163df8d43d182e9d0dfe66e340b60
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725142"
---
# <a name="ftp-quote"></a>FTP: Anführungszeichen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet wörtliche Argumente an den Remote-FTP-Server. Ein einzelner FTP-Antwort Code wird zurückgegeben.   
## <a name="syntax"></a>Syntax  
```  
quote <Argument>[ ]  
```  
#### <a name="parameters"></a>Parameter  

| Parameter  |                    BESCHREIBUNG                    |
|------------|---------------------------------------------------|
| <Argument> | Gibt das Argument an, das an den FTP-Server gesendet werden soll. |

## <a name="remarks"></a>Bemerkungen  
Der **Anführungs** Zeichen Wert ist mit dem **literalbefehl** identisch.  
## <a name="examples"></a>Beispiele  
Senden Sie einen Befehl zum **Beenden** an den FTP-Remote Server.  
```  
quote quit  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [FTP: literal_1](ftp-literal_1.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
