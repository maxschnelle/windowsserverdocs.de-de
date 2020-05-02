---
title: FTP-mdelete_1
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f578a50207439f9bfb21c2607f0aa60a20fad292
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725035"
---
# <a name="ftp-mdelete_1"></a>FTP: mdelete_1

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf dem Remote Computer.   
## <a name="syntax"></a>Syntax  
```  
mdelete <remoteFile>[ ]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |             BESCHREIBUNG              |
|--------------|--------------------------------------|
| <remoteFile> | Gibt die zu löschende Remote Datei an. |

## <a name="examples"></a>Beispiele  
Löschen Sie Remote Dateien " **exe** " und " **b. exe**".  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
