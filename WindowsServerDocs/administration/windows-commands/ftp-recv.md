---
title: FTP-empfangener
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f249ce61-247d-421b-9b93-48bce5108800 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7fec409741e00bb3e6f61808630e5141ce4ec78f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842963"
---
# <a name="ftp-recv"></a>FTP: empfangener

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine Remote Datei mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer.   
## <a name="syntax"></a>Syntax  
```  
recv <remoteFile> [<LocalFile>]  
```  
#### <a name="parameters"></a>Parameter  

|   Parameter   |                   Beschreibung                    |
|---------------|--------------------------------------------------|
| <remoteFile>  |        Gibt die zu Kopier-Remote Datei an.        |
| [<LocalFile>] | Gibt den Namen an, der auf dem lokalen Computer verwendet werden soll. |

## <a name="remarks"></a>Hinweise  
- Der **empfangener** -Befehl ist mit dem **Get** -Befehl identisch.  
- Wenn " *LocalFile* " nicht angegeben wird, erhält die Datei den Namen " *remotefile* ".  
  ## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
  Kopieren Sie die Datei " **Test. txt** " mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer.  
  ```  
  recv test.txt  
  ```  
  Kopieren Sie die Datei " **Test. txt** " mit dem aktuellen Datei Übertragungstyp als **test1. txt** auf den lokalen Computer.  
  ```  
  recv test.txt test1.txt  
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- [FTP: ASCII](ftp-ascii.md)  
- [FTP: binär](ftp-binary.md)  
- [FTP: Get](ftp-get.md)  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
