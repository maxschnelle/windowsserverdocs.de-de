---
title: FTP-mget
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 666025c92b6fb1a612cbe7b83833557a8a7d5017
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376297"
---
# <a name="ftp-mget"></a>FTP: mget

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert Remote Dateien mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer.   
## <a name="syntax"></a>Syntax  
```  
mget <remoteFile>[ ]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                        Beschreibung                        |
|--------------|-----------------------------------------------------------|
| <remoteFile> | Gibt die Remote Dateien an, die auf den lokalen Computer kopiert werden sollen. |

## <a name="BKMK_Examples"></a>Beispiele  
Kopieren Sie die Remote Dateien " **exe** " und " **b. exe** " auf den lokalen Computer, indem Sie den aktuellen Datei Übertragungstyp verwenden.  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: ASCII](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
