---
title: FTP löschen
description: Referenz Thema zum Löschen von FTP
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 14e4e870bb7f0f384e3803d75021298d04a8ca4d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725321"
---
# <a name="ftp-delete"></a>FTP: Löschen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf Remote Computern.   
## <a name="syntax"></a>Syntax  
```  
delete <remoteFile>  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |          BESCHREIBUNG          |
|--------------|-------------------------------|
| <remoteFile> | Gibt die Datei an, die gelöscht werden soll. |

## <a name="examples"></a>Beispiele  
Löschen Sie die Datei "Test. txt" auf dem Remote Computer.  
```  
delete test.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
