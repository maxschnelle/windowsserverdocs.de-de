---
title: FTP-Anfüge Ende
description: Referenz Thema für FTP-anfügen
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b53228473b8ea16a0955c244d60fae77cf4f7d7f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725405"
---
# <a name="ftp-append"></a>FTP: Anfügen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt eine lokale Datei mithilfe der aktuellen Dateityp Einstellung an eine Datei auf dem Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
append <LocalFile> [remoteFile]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                               BESCHREIBUNG                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     Gibt die hinzu zufügende lokale Datei an.                     |
| [remotefile] | Gibt die Datei auf dem Remote Computer an, <LocalFile> der hinzugefügt wird. |

## <a name="remarks"></a>Bemerkungen  
Wenn *remotefile* weggelassen wird, wird der Name der *LocalFile* anstelle des Remote Dateinamens verwendet.  
## <a name="examples"></a>Beispiele  
Fügen Sie file1. txt an file2. txt auf dem Remote Computer an.  
```  
append file1.txt file2.txt  
```  
Fügen Sie die lokale Datei "file1. txt" an eine Datei mit dem Namen "file1. txt" auf dem Remote Computer an.  
```  
append file1.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
