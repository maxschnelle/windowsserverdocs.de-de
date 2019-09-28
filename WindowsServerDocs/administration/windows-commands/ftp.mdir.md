---
title: FTP-mdir
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08aa5bb216a3d0155c100c761e476bb963e59311
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375849"
---
# <a name="ftp-mdir"></a>FTP: mdir

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Verzeichnisliste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis an.   
## <a name="syntax"></a>Syntax  
```  
mdir <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                               Beschreibung                                |
|--------------|--------------------------------------------------------------------------|
| <remoteFile> |   Gibt das Verzeichnis oder die Datei an, für das eine Auflistung angezeigt werden soll.   |
| <LocalFile>  | Gibt eine lokale Datei zum Speichern der Auflistung an. Dieser Parameter ist erforderlich. |

## <a name="remarks"></a>Hinweise  
- Sie können **mdir** verwenden, um mehrere Dateien anzugeben.  
- Angeben von *remotefile*  
  Geben Sie einen Bindestrich ( **-** ) ein, um das aktuelle Arbeitsverzeichnis auf dem Remote Computer zu verwenden.  
- Angeben einer *LocalFile*  
  Geben Sie einen Bindestrich ( **-** ) ein, um die Auflistung auf dem Bildschirm anzuzeigen.  
  ## <a name="BKMK_Examples"></a>Beispiele  
  Anzeigen einer Verzeichnisliste von **dir1** und **dir2** auf dem Bildschirm  
  ```  
  mdir dir1 dir2 -  
  ```  
  Speichern Sie die kombinierte Verzeichnis Auflistung von **dir1** und **dir2** in einer lokalen Datei namens **dirlist. txt.**  
  ```  
  mdir dir1 dir2 dirlist.txt  
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
