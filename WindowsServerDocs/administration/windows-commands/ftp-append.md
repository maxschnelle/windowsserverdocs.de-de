---
title: FTP-Anfüge Ende
description: Windows-Befehls Thema für FTP-anfügen
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44ce1d6e7259dc8745da35ed462e6378f0fce8ba
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843823"
---
# <a name="ftp-append"></a>FTP: Anfügen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt eine lokale Datei mithilfe der aktuellen Dateityp Einstellung an eine Datei auf dem Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
append <LocalFile> [remoteFile]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                               Beschreibung                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     Gibt die hinzu zufügende lokale Datei an.                     |
| [remotefile] | Gibt die Datei auf dem Remote Computer an, der <LocalFile> hinzugefügt wird. |

## <a name="remarks"></a>Hinweise  
Wenn *remotefile* weggelassen wird, wird der Name der *LocalFile* anstelle des Remote Dateinamens verwendet.  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Fügen Sie file1. txt an file2. txt auf dem Remote Computer an.  
```  
append file1.txt file2.txt  
```  
Fügen Sie die lokale Datei "file1. txt" an eine Datei mit dem Namen "file1. txt" auf dem Remote Computer an.  
```  
append file1.txt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
