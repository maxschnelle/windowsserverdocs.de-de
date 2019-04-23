---
title: FTP-löschen
description: Windows-Befehle-Thema zum Löschen von ftp
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1365373097cf7280c4475514107a940f46e65893
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840071"
---
# <a name="ftp-delete"></a>FTP: Löschen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Löscht Dateien auf Remotecomputern.   
## <a name="syntax"></a>Syntax  
```  
delete <remoteFile>  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<remoteFile>|Gibt die zu löschende Datei an.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Löschen Sie die Datei "Test.txt" auf dem Remotecomputer.  
```  
delete test.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
