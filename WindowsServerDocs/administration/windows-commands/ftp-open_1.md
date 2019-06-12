---
title: FTP-open_1
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 45de8b3c210fe0925ac3cc43c41d3e092d5dfe16
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438504"
---
# <a name="ftp-open1"></a>FTP: open_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Eine Verbindung mit dem angegebenen ftp-Server.   
## <a name="syntax"></a>Syntax  
```  
open <computer> [<Port>]  
```  
### <a name="parameters"></a>Parameter  

| Parameter  |                                           Beschreibung                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                Gibt an, den Remotecomputer, den Sie eine Verbindung herstellen möchten.                 |
|  [<Port>]  | Gibt eine TCP-Portnummer zu verwenden, um die Verbindung mit eines ftp-Servers an. Standardmäßig wird TCP-Port 21 verwendet. |

## <a name="remarks"></a>Hinweise  
Sie können ein IP-Adresse oder einen Computer an (in diesem Fall eine DNS-Server oder die Datei "Hosts" muss verfügbar sein) an **Computer**.  
## <a name="BKMK_Examples"></a>Beispiele für  
Verbinden mit dem ftp-Server am **ftp.microsoft.com**.  
```  
Open ftp.microsoft.com  
```  
Verbinden mit dem ftp-Server am **ftp.microsoft.com** , TCP-Port 755 überwacht.  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
