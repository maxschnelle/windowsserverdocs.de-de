---
title: FTP-send_1
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 04617246c05edde127db01ce1a0fe692eb0aceb1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725116"
---
# <a name="ftp-send_1"></a>FTP: send_1

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine lokale Datei mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.   
## <a name="syntax"></a>Syntax  
```  
send <LocalFile> [<remoteFile>]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                    BESCHREIBUNG                    |
|--------------|---------------------------------------------------|
| <LocalFile>  |         Gibt die zu Kopier lokale Datei an.         |
| <remoteFile> | Gibt den Namen an, der auf dem Remote Computer verwendet werden soll. |

## <a name="remarks"></a>Bemerkungen  
- Der **Send** -Befehl ist mit dem **Put** -Befehl identisch.  
- Wenn *remotefile* nicht angegeben wird, erhält die Datei den Namen *LocalFile* .  
  ## <a name="examples"></a>Beispiele  
  Kopieren Sie die lokale Datei " **Test. txt** ", und nennen Sie Sie " **test1. txt** " auf dem Remote Computer.  
  ```  
  send test.txt test1.txt  
  ```  
  Kopieren Sie die lokale Datei **Programm. exe** auf den Remote Computer.  
  ```  
  send program.exe  
  ```  
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
