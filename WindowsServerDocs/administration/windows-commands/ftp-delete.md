---
title: FTP löschen
description: Windows-Befehls Thema zum Löschen von FTP
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4683e63700a22d8ac8016fb118475a341221e7f6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843563"
---
# <a name="ftp-delete"></a>FTP: Löschen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf Remote Computern.   
## <a name="syntax"></a>Syntax  
```  
delete <remoteFile>  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |          Beschreibung          |
|--------------|-------------------------------|
| <remoteFile> | Gibt die Datei an, die gelöscht werden soll. |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Löschen Sie die Datei "Test. txt" auf dem Remote Computer.  
```  
delete test.txt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
