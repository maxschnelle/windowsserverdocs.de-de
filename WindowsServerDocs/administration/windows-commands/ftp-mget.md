---
title: FTP-mget
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a71fbfb60ae012b5e65af04e6f3e21ec796996a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725235"
---
# <a name="ftp-mget"></a>FTP: mget

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert Remote Dateien mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer.   
## <a name="syntax"></a>Syntax  
```  
mget <remoteFile>[ ]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                        BESCHREIBUNG                        |
|--------------|-----------------------------------------------------------|
| <remoteFile> | Gibt die Remote Dateien an, die auf den lokalen Computer kopiert werden sollen. |

## <a name="examples"></a>Beispiele  
Kopieren Sie die Remote Dateien " **exe** " und " **b. exe** " auf den lokalen Computer, indem Sie den aktuellen Datei Übertragungstyp verwenden.  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [FTP: ASCII](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
