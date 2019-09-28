---
title: FTP-empfangener
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f249ce61-247d-421b-9b93-48bce5108800 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ec35a2044945e3d39a2a78d39923de3a56eb18d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376130"
---
# <a name="ftp-recv"></a>FTP: empfangener

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine Remote Datei mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer.   
## <a name="syntax"></a>Syntax  
```  
recv <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>Parameter  

|   Parameter   |                   Beschreibung                    |
|---------------|--------------------------------------------------|
| <remoteFile>  |        Gibt die zu Kopier-Remote Datei an.        |
| [<LocalFile>] | Gibt den Namen an, der auf dem lokalen Computer verwendet werden soll. |

## <a name="remarks"></a>Hinweise  
- Der **empfangener** -Befehl ist mit dem **Get** -Befehl identisch.  
- Wenn " *LocalFile* " nicht angegeben wird, erhält die Datei den Namen " *remotefile* ".  
  ## <a name="BKMK_Examples"></a>Beispiele  
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
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
