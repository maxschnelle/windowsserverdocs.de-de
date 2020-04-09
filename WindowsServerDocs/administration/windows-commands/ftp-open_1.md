---
title: FTP-open_1
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8bd3063a52908d65f336afcda6b6982d5bc9bf94
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843183"
---
# <a name="ftp-open_1"></a>FTP: open_1

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit dem angegebenen FTP-Server her.   
## <a name="syntax"></a>Syntax  
```  
open <computer> [<Port>]  
```  
#### <a name="parameters"></a>Parameter  

| Parameter  |                                           Beschreibung                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                Gibt den Remote Computer an, mit dem Sie eine Verbindung herstellen möchten.                 |
|  [<Port>]  | Gibt eine TCP-Portnummer an, die für die Verbindung mit einem FTP-Server verwendet wird. Standardmäßig wird TCP-Port 21 verwendet. |

## <a name="remarks"></a>Hinweise  
Sie können eine IP-Adresse oder einen Computernamen verwenden (in diesem Fall muss ein DNS-Server oder eine Host Datei verfügbar sein), um den **Computer**anzugeben.  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Stellen Sie unter **FTP.Microsoft.com**eine Verbindung zum FTP-Server her.  
```  
Open ftp.microsoft.com  
```  
Stellen Sie eine Verbindung mit dem FTP-Server unter **FTP.Microsoft.com** her, der an TCP-Port 755 lauscht.  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
