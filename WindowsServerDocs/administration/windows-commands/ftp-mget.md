---
title: FTP-mget
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72b45f84622fcd6abf7a743f606fb514def584cd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843353"
---
# <a name="ftp-mget"></a>FTP: mget

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert Remote Dateien mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer.   
## <a name="syntax"></a>Syntax  
```  
mget <remoteFile>[ ]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                        Beschreibung                        |
|--------------|-----------------------------------------------------------|
| <remoteFile> | Gibt die Remote Dateien an, die auf den lokalen Computer kopiert werden sollen. |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Kopieren Sie die Remote Dateien " **exe** " und " **b. exe** " auf den lokalen Computer, indem Sie den aktuellen Datei Übertragungstyp verwenden.  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: ASCII](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
