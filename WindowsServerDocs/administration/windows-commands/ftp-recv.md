---
title: FTP-empfangener
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f249ce61-247d-421b-9b93-48bce5108800 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ece259f2d48e18f6a789d51b1df7089490f2fa1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725126"
---
# <a name="ftp-recv"></a>FTP: empfangener

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine Remote Datei mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer.   
## <a name="syntax"></a>Syntax  
```  
recv <remoteFile> [<LocalFile>]  
```  
#### <a name="parameters"></a>Parameter  

|   Parameter   |                   BESCHREIBUNG                    |
|---------------|--------------------------------------------------|
| <remoteFile>  |        Gibt die zu Kopier-Remote Datei an.        |
| [<LocalFile>] | Gibt den Namen an, der auf dem lokalen Computer verwendet werden soll. |

## <a name="remarks"></a>Bemerkungen  
- Der **empfangener** -Befehl ist mit dem **Get** -Befehl identisch.  
- Wenn " *LocalFile* " nicht angegeben wird, erhält die Datei den Namen " *remotefile* ".  
  ## <a name="examples"></a>Beispiele  
  Kopieren Sie die Datei " **Test. txt** " mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer.  
  ```  
  recv test.txt  
  ```  
  Kopieren Sie die Datei " **Test. txt** " mit dem aktuellen Datei Übertragungstyp als **test1. txt** auf den lokalen Computer.  
  ```  
  recv test.txt test1.txt  
  ```  
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
- [FTP: ASCII](ftp-ascii.md)  
- [FTP: binär](ftp-binary.md)  
- [FTP: Get](ftp-get.md)  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
