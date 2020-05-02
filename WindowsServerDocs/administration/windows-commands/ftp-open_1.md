---
title: FTP-open_1
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 15a27d2f7512da352a0f4ddf02fa2511ffce7c1d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725196"
---
# <a name="ftp-open_1"></a>FTP: open_1

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit dem angegebenen FTP-Server her.   
## <a name="syntax"></a>Syntax  
```  
open <computer> [<Port>]  
```  
#### <a name="parameters"></a>Parameter  

| Parameter  |                                           BESCHREIBUNG                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                Gibt den Remote Computer an, mit dem Sie eine Verbindung herstellen möchten.                 |
|  [<Port>]  | Gibt eine TCP-Portnummer an, die für die Verbindung mit einem FTP-Server verwendet wird. Standardmäßig wird TCP-Port 21 verwendet. |

## <a name="remarks"></a>Bemerkungen  
Sie können eine IP-Adresse oder einen Computernamen verwenden (in diesem Fall muss ein DNS-Server oder eine Host Datei verfügbar sein), um den **Computer**anzugeben.  
## <a name="examples"></a>Beispiele  
Stellen Sie unter **FTP.Microsoft.com**eine Verbindung zum FTP-Server her.  
```  
Open ftp.microsoft.com  
```  
Stellen Sie eine Verbindung mit dem FTP-Server unter **FTP.Microsoft.com** her, der an TCP-Port 755 lauscht.  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
