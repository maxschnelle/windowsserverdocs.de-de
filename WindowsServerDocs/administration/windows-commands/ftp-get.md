---
title: FTP-get
description: Abrufen des Windows-Befehle Themas für ftp
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 798317f3921cd0e5ff12b69b972e2ea423fa6b3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816731"
---
# <a name="ftp-get"></a>FTP: Abrufen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert eine Remotedatei auf dem lokalen Computer, die mit den aktuellen Dateiübertragungstyp an.   
## <a name="syntax"></a>Syntax  
```  
get <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<remoteFile>|Gibt an, der remote-Datei zu kopieren.|  
|[<LocalFile>]|Gibt den Namen der Datei, die auf dem lokalen Computer verwenden. Wenn *LocalFile* nicht angegeben ist, wird die Datei erhält den *Remotedatei* Name.|  
## <a name="remarks"></a>Hinweise  
Die **erhalten** Befehl ist identisch mit der **empfangener** Befehl.  
## <a name="BKMK_Examples"></a>Beispiele für  
Kopie **"Test.txt"** auf dem lokalen Computer, die den aktuellen Dateityp für die Übertragung verwenden.  
```  
get test.txt  
```  
Kopie **"Test.txt"** auf dem lokalen Computer als **test1.txt** mithilfe der aktuellen Datei Übertragungstyp auswählen.  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [ftp: ascii](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
