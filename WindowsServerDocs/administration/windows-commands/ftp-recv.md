---
title: FTP-recv
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f249ce61-247d-421b-9b93-48bce5108800 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4979010c13d78c89c9a3e4965b567f7eef1f2ede
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841101"
---
# <a name="ftp-recv"></a>FTP: Durchschn.

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert eine Remotedatei auf dem lokalen Computer, die mit den aktuellen Dateiübertragungstyp an.   
## <a name="syntax"></a>Syntax  
```  
recv <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<remoteFile>|Gibt an, der remote-Datei zu kopieren.|  
|[<LocalFile>]|Gibt den Namen für die Verwendung auf dem lokalen Computer.|  
## <a name="remarks"></a>Hinweise  
-   Die **empfangener** Befehl ist identisch mit der **erhalten** Befehl.  
-   Wenn *LocalFile* nicht angegeben ist, wird die Datei erhält den *Remotedatei* Name.  
## <a name="BKMK_Examples"></a>Beispiele für  
Kopie **"Test.txt"** auf dem lokalen Computer, die den aktuellen Dateityp für die Übertragung verwenden.  
```  
recv test.txt  
```  
Kopie **"Test.txt"** auf dem lokalen Computer als **test1.txt** mithilfe der aktuellen Datei Übertragungstyp auswählen.  
```  
recv test.txt test1.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [ftp: ascii](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   [ftp: get](ftp-get.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
