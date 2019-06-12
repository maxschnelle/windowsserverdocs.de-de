---
title: Fügen Sie FTP
description: 'Fügen Sie die Windows-Befehle-Thema für ftp '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9580d725120bb32a9b915d37cdbc173bfb17b859
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438846"
---
# <a name="ftp-append"></a>FTP: Anfügen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fügt eine lokale Datei in eine Datei auf dem Remotecomputer über den aktuellen Dateityp festlegen.   
## <a name="syntax"></a>Syntax  
```  
append <LocalFile> [remoteFile]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                               Beschreibung                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     Gibt die lokale Datei hinzufügen.                     |
| [remoteFile] | Gibt die Datei auf dem Remotecomputer, <LocalFile> hinzugefügt wird. |

## <a name="remarks"></a>Hinweise  
Wenn *Remotedatei* weggelassen wird, die *LocalFile* Name anstelle des Namens der remote-Datei verwendet wird.  
## <a name="BKMK_Examples"></a>Beispiele für  
Fügen Sie file1.txt an file2.txt auf dem Remotecomputer ein.  
```  
append file1.txt file2.txt  
```  
Fügen Sie der lokalen file1.txt an eine Datei namens file1.txt auf dem Remotecomputer an.  
```  
append file1.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
