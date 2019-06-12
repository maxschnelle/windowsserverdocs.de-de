---
title: Einfügen von FTP
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d602c685b7eac5d18c88bc0f6709b189cc61a77
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438465"
---
# <a name="ftp-put"></a>FTP: put

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert eine Remotedatei auf dem Remotecomputer über den aktuellen Dateityp für die Übertragung.   
## <a name="syntax"></a>Syntax  
```  
put <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>Parameter  

|   Parameter    |                    Beschreibung                    |
|----------------|---------------------------------------------------|
|  <LocalFile>   |         Gibt an, die lokale Datei zu kopieren.         |
| [<remoteFile>] | Gibt den Namen für die Verwendung auf dem Remotecomputer. |

## <a name="remarks"></a>Hinweise  
- Die **put** Befehl ist identisch mit der **senden** Befehl.  
- Wenn *Remotedatei* nicht angegeben ist, wird die Datei erhält den *LocalFile* Name.  
  ## <a name="BKMK_Examples"></a>Beispiele für  
  Kopieren Sie die lokale Datei **"Test.txt"** und nennen Sie sie **test1.txt** auf dem Remotecomputer.  
  ```  
  put test.txt test1.txt  
  ```  
  Kopieren Sie die lokale Datei **program.exe** an den Remotecomputer.  
  ```  
  put program.exe  
  ```  
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
- [ftp: ascii](ftp-ascii.md)  
- [FTP: binär](ftp-binary.md)  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
