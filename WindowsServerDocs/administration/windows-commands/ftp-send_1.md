---
title: FTP-send_1
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3dca11f0d534eb875a71fa2c39cdd4dc674ad788
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862121"
---
# <a name="ftp-send1"></a>FTP: send_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert eine Remotedatei auf dem Remotecomputer über den aktuellen Dateityp für die Übertragung.   
## <a name="syntax"></a>Syntax  
```  
send <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<LocalFile>|Gibt an, die lokale Datei zu kopieren.|  
|<remoteFile>|Gibt den Namen für die Verwendung auf dem Remotecomputer.|  
## <a name="remarks"></a>Hinweise  
-   Die **senden** Befehl ist identisch mit der **put** Befehl.  
-   Wenn *Remotedatei* nicht angegeben ist, wird die Datei erhält den *LocalFile* Name.  
## <a name="BKMK_Examples"></a>Beispiele für  
Kopieren Sie die lokale Datei **"Test.txt"** und nennen Sie sie **test1.txt** auf dem Remotecomputer.  
```  
send test.txt test1.txt  
```  
Kopieren Sie die lokale Datei **program.exe** an den Remotecomputer.  
```  
send program.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
