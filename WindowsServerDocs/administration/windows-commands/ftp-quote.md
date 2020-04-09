---
title: FTP-Anführungszeichen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1bf13704150d602fbfa4e3b1a3fb1774d3bf7363
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843033"
---
# <a name="ftp-quote"></a>FTP: Anführungszeichen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet wörtliche Argumente an den Remote-FTP-Server. Ein einzelner FTP-Antwort Code wird zurückgegeben.   
## <a name="syntax"></a>Syntax  
```  
quote <Argument>[ ]  
```  
#### <a name="parameters"></a>Parameter  

| Parameter  |                    Beschreibung                    |
|------------|---------------------------------------------------|
| <Argument> | Gibt das Argument an, das an den FTP-Server gesendet werden soll. |

## <a name="remarks"></a>Hinweise  
Der **Anführungs** Zeichen Wert ist mit dem **literalbefehl** identisch.  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Senden Sie einen Befehl zum **Beenden** an den FTP-Remote Server.  
```  
quote quit  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: literal_1](ftp-literal_1.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
