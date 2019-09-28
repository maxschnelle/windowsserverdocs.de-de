---
title: FTP-literal_1
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 393dea27e8567a72a5bd25c927282ade93e317c9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376273"
---
# <a name="ftp-literal_1"></a>FTP: literal_1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 sendet wörtliche Argumente an den Remote-FTP-Server. Ein einzelner FTP-Antwort Code wird zurückgegeben.   

## <a name="syntax"></a>Syntax  
```  
literal <Argument> [ ]  
```  
### <a name="parameters"></a>Parameter  

| Parameter  |                    Beschreibung                    |
|------------|---------------------------------------------------|
| <Argument> | Gibt das Argument an, das an den FTP-Server gesendet werden soll. |

## <a name="remarks"></a>Hinweise  
Der **literalbefehl** ist identisch mit dem **Anführungs** Zeichen Befehl.  
## <a name="BKMK_Examples"></a>Beispiele  
Senden Sie einen Befehl zum **Beenden** an den FTP-Remote Server.  
```  
literal quit  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: Anführungszeichen](ftp-quote.md)  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
