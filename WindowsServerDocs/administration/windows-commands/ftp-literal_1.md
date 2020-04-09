---
title: FTP-literal_1
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f502bb56c94734870962f56cfb85dcc17ddc3f93
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843393"
---
# <a name="ftp-literal_1"></a>FTP: literal_1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 sendet wörtliche Argumente an den Remote-FTP-Server. Ein einzelner FTP-Antwort Code wird zurückgegeben.   

## <a name="syntax"></a>Syntax  
```  
literal <Argument> [ ]  
```  
#### <a name="parameters"></a>Parameter  

| Parameter  |                    Beschreibung                    |
|------------|---------------------------------------------------|
| <Argument> | Gibt das Argument an, das an den FTP-Server gesendet werden soll. |

## <a name="remarks"></a>Hinweise  
Der **literalbefehl** ist identisch mit dem **Anführungs** Zeichen Befehl.  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Senden Sie einen Befehl zum **Beenden** an den FTP-Remote Server.  
```  
literal quit  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: Anführungszeichen](ftp-quote.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
