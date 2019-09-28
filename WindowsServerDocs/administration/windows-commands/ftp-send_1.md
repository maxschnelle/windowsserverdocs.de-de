---
title: FTP-send_1
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd9f658b4fbfa5f6c9fa9a58fb0c524ad53627bc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376000"
---
# <a name="ftp-send_1"></a>FTP: send_1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine lokale Datei mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.   
## <a name="syntax"></a>Syntax  
```  
send <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                    Beschreibung                    |
|--------------|---------------------------------------------------|
| <LocalFile>  |         Gibt die zu Kopier lokale Datei an.         |
| <remoteFile> | Gibt den Namen an, der auf dem Remote Computer verwendet werden soll. |

## <a name="remarks"></a>Hinweise  
- Der **Send** -Befehl ist mit dem **Put** -Befehl identisch.  
- Wenn *remotefile* nicht angegeben wird, erhält die Datei den Namen *LocalFile* .  
  ## <a name="BKMK_Examples"></a>Beispiele  
  Kopieren Sie die lokale Datei " **Test. txt** ", und nennen Sie Sie " **test1. txt** " auf dem Remote Computer.  
  ```  
  send test.txt test1.txt  
  ```  
  Kopieren Sie die lokale Datei **Programm. exe** auf den Remote Computer.  
  ```  
  send program.exe  
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
