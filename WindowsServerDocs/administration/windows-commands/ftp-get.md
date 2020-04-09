---
title: FTP-Get
description: Windows-Befehls Thema für FTP Get
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0b4dc41ec29edfb94661176a5ccaf651584fc43
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843483"
---
# <a name="ftp-get"></a>FTP: Get

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine Remote Datei mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer.   
## <a name="syntax"></a>Syntax  
```  
get <remoteFile> [<LocalFile>]  
```  
#### <a name="parameters"></a>Parameter  

|   Parameter   |                                                              Beschreibung                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|
| <remoteFile>  |                                                   Gibt die zu Kopier-Remote Datei an.                                                   |
| [<LocalFile>] | Gibt den Namen der Datei an, die auf dem lokalen Computer verwendet werden soll. Wenn " *LocalFile* " nicht angegeben wird, erhält die Datei den Namen " *remotefile* ". |

## <a name="remarks"></a>Hinweise  
Der **Get** -Befehl ist mit dem **empfangener** -Befehl identisch.  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Kopieren Sie die Datei " **Test. txt** " mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer.  
```  
get test.txt  
```  
Kopieren Sie die Datei " **Test. txt** " mit dem aktuellen Datei Übertragungstyp als **test1. txt** auf den lokalen Computer.  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: ASCII](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
