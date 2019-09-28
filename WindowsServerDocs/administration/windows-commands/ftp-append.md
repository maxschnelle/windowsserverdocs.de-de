---
title: FTP-Anfüge Ende
description: 'Windows-Befehls Thema für FTP-anfügen '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52d16b878ff5fb165fd851b227dcc361c9da3a80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376644"
---
# <a name="ftp-append"></a>FTP: Anfügen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt eine lokale Datei mithilfe der aktuellen Dateityp Einstellung an eine Datei auf dem Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
append <LocalFile> [remoteFile]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                               Beschreibung                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     Gibt die hinzu zufügende lokale Datei an.                     |
| [remotefile] | Gibt die Datei auf dem Remote Computer an, der <LocalFile> hinzugefügt wird. |

## <a name="remarks"></a>Hinweise  
Wenn *remotefile* weggelassen wird, wird der Name der *LocalFile* anstelle des Remote Dateinamens verwendet.  
## <a name="BKMK_Examples"></a>Beispiele  
Fügen Sie file1. txt an file2. txt auf dem Remote Computer an.  
```  
append file1.txt file2.txt  
```  
Fügen Sie die lokale Datei "file1. txt" an eine Datei mit dem Namen "file1. txt" auf dem Remote Computer an.  
```  
append file1.txt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
