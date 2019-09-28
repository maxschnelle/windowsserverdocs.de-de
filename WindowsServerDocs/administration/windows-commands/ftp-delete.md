---
title: FTP löschen
description: Windows-Befehls Thema zum Löschen von FTP
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 1b566da14751921e2f38acd922ececbbc972daa6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376453"
---
# <a name="ftp-delete"></a>FTP: Löschen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf Remote Computern.   
## <a name="syntax"></a>Syntax  
```  
delete <remoteFile>  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |          Beschreibung          |
|--------------|-------------------------------|
| <remoteFile> | Gibt die Datei an, die gelöscht werden soll. |

## <a name="BKMK_Examples"></a>Beispiele  
Löschen Sie die Datei "Test. txt" auf dem Remote Computer.  
```  
delete test.txt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
