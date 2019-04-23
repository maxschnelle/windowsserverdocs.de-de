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
ms.openlocfilehash: 3307ba71e7b3c8b4113f9ed29ab06660dafa5f6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868741"
---
# <a name="ftp-put"></a>FTP: put

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert eine Remotedatei auf dem Remotecomputer über den aktuellen Dateityp für die Übertragung.   
## <a name="syntax"></a>Syntax  
```  
put <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<LocalFile>|Gibt an, die lokale Datei zu kopieren.|  
|[<remoteFile>]|Gibt den Namen für die Verwendung auf dem Remotecomputer.|  
## <a name="remarks"></a>Hinweise  
-   Die **put** Befehl ist identisch mit der **senden** Befehl.  
-   Wenn *Remotedatei* nicht angegeben ist, wird die Datei erhält den *LocalFile* Name.  
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
-   [ftp: ascii](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
