---
title: FTP-Get
description: Referenz Thema für FTP Get
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 37423f81fd72e79cebcdf169160ad3e8033b69b2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725294"
---
# <a name="ftp-get"></a>FTP: Get

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine Remote Datei mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer.   
## <a name="syntax"></a>Syntax  
```  
get <remoteFile> [<LocalFile>]  
```  
#### <a name="parameters"></a>Parameter  

|   Parameter   |                                                              BESCHREIBUNG                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|
| <remoteFile>  |                                                   Gibt die zu Kopier-Remote Datei an.                                                   |
| [<LocalFile>] | Gibt den Namen der Datei an, die auf dem lokalen Computer verwendet werden soll. Wenn " *LocalFile* " nicht angegeben wird, erhält die Datei den Namen " *remotefile* ". |

## <a name="remarks"></a>Bemerkungen  
Der **Get** -Befehl ist mit dem **empfangener** -Befehl identisch.  
## <a name="examples"></a>Beispiele  
Kopieren Sie die Datei " **Test. txt** " mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer.  
```  
get test.txt  
```  
Kopieren Sie die Datei " **Test. txt** " mit dem aktuellen Datei Übertragungstyp als **test1. txt** auf den lokalen Computer.  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [FTP: ASCII](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
