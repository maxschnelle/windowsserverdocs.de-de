---
title: FTP-mdelete_1
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ffbb06cff9e177316ea60e281c25d7640a7f981
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375925"
---
# <a name="ftp-mdelete_1"></a>FTP: mdelete_1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf dem Remote Computer.   
## <a name="syntax"></a>Syntax  
```  
mdelete <remoteFile>[ ]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |             Beschreibung              |
|--------------|--------------------------------------|
| <remoteFile> | Gibt die zu löschende Remote Datei an. |

## <a name="BKMK_Examples"></a>Beispiele  
Löschen Sie Remote Dateien " **exe** " und " **b. exe**".  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
