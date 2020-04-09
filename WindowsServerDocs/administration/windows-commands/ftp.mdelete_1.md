---
title: FTP-mdelete_1
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b64fa691a9ac890aad0e8d8dc93bd73e53478fc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842723"
---
# <a name="ftp-mdelete_1"></a>FTP: mdelete_1

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf dem Remote Computer.   
## <a name="syntax"></a>Syntax  
```  
mdelete <remoteFile>[ ]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |             Beschreibung              |
|--------------|--------------------------------------|
| <remoteFile> | Gibt die zu löschende Remote Datei an. |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Löschen Sie Remote Dateien " **exe** " und " **b. exe**".  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
