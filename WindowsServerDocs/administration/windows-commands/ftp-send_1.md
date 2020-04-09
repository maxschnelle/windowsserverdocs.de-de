---
title: FTP-send_1
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: df6ea9eda6fced91babca37639cd6efe981ba7de
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843003"
---
# <a name="ftp-send_1"></a>FTP: send_1

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine lokale Datei mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.   
## <a name="syntax"></a>Syntax  
```  
send <LocalFile> [<remoteFile>]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                    Beschreibung                    |
|--------------|---------------------------------------------------|
| <LocalFile>  |         Gibt die zu Kopier lokale Datei an.         |
| <remoteFile> | Gibt den Namen an, der auf dem Remote Computer verwendet werden soll. |

## <a name="remarks"></a>Hinweise  
- Der **Send** -Befehl ist mit dem **Put** -Befehl identisch.  
- Wenn *remotefile* nicht angegeben wird, erhält die Datei den Namen *LocalFile* .  
  ## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
  Kopieren Sie die lokale Datei " **Test. txt** ", und nennen Sie Sie " **test1. txt** " auf dem Remote Computer.  
  ```  
  send test.txt test1.txt  
  ```  
  Kopieren Sie die lokale Datei **Programm. exe** auf den Remote Computer.  
  ```  
  send program.exe  
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
