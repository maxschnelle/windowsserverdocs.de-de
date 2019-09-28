---
title: FTP-open_1
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c5da1c73362c0396300f712b2e45b906d1652604
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376189"
---
# <a name="ftp-open_1"></a>FTP: open_1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit dem angegebenen FTP-Server her.   
## <a name="syntax"></a>Syntax  
```  
open <computer> [<Port>]  
```  
### <a name="parameters"></a>Parameter  

| Parameter  |                                           Beschreibung                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                Gibt den Remote Computer an, mit dem Sie eine Verbindung herstellen möchten.                 |
|  [<Port>]  | Gibt eine TCP-Portnummer an, die für die Verbindung mit einem FTP-Server verwendet wird. Standardmäßig wird TCP-Port 21 verwendet. |

## <a name="remarks"></a>Hinweise  
Sie können eine IP-Adresse oder einen Computernamen verwenden (in diesem Fall muss ein DNS-Server oder eine Host Datei verfügbar sein), um den **Computer**anzugeben.  
## <a name="BKMK_Examples"></a>Beispiele  
Stellen Sie unter **FTP.Microsoft.com**eine Verbindung zum FTP-Server her.  
```  
Open ftp.microsoft.com  
```  
Stellen Sie eine Verbindung mit dem FTP-Server unter **FTP.Microsoft.com** her, der an TCP-Port 755 lauscht.  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
