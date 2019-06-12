---
title: FTP-send_1
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 39423aff3c64f41c4fc0f8998484e6dcc38f822e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438441"
---
# <a name="ftp-send1"></a>FTP: send_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert eine Remotedatei auf dem Remotecomputer über den aktuellen Dateityp für die Übertragung.   
## <a name="syntax"></a>Syntax  
```  
send <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                    Beschreibung                    |
|--------------|---------------------------------------------------|
| <LocalFile>  |         Gibt an, die lokale Datei zu kopieren.         |
| <remoteFile> | Gibt den Namen für die Verwendung auf dem Remotecomputer. |

## <a name="remarks"></a>Hinweise  
- Die **senden** Befehl ist identisch mit der **put** Befehl.  
- Wenn *Remotedatei* nicht angegeben ist, wird die Datei erhält den *LocalFile* Name.  
  ## <a name="BKMK_Examples"></a>Beispiele für  
  Kopieren Sie die lokale Datei **"Test.txt"** und nennen Sie sie **test1.txt** auf dem Remotecomputer.  
  ```  
  send test.txt test1.txt  
  ```  
  Kopieren Sie die lokale Datei **program.exe** an den Remotecomputer.  
  ```  
  send program.exe  
  ```  
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
