---
title: FTP-mdir
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54adcd1d28079487c5e238c72413d8269447944e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725027"
---
# <a name="ftp-mdir"></a>FTP: mdir

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Verzeichnisliste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis an.   
## <a name="syntax"></a>Syntax  
```  
mdir <remoteFile>[ ] <LocalFile>  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                               BESCHREIBUNG                                |
|--------------|--------------------------------------------------------------------------|
| <remoteFile> |   Gibt das Verzeichnis oder die Datei an, für das eine Auflistung angezeigt werden soll.   |
| <LocalFile>  | Gibt eine lokale Datei zum Speichern der Auflistung an. Dieser Parameter ist erforderlich. |

## <a name="remarks"></a>Bemerkungen  
- Sie können **mdir** verwenden, um mehrere Dateien anzugeben.  
- Angeben von *remotefile*  
  Geben Sie einen Bindestrich**-**() ein, um das aktuelle Arbeitsverzeichnis auf dem Remote Computer zu verwenden.  
- Angeben einer *LocalFile*  
  Geben Sie einen Bindestrich**-**() ein, um die Auflistung auf dem Bildschirm anzuzeigen.  
  ## <a name="examples"></a>Beispiele  
  Anzeigen einer Verzeichnisliste von **dir1** und **dir2** auf dem Bildschirm  
  ```  
  mdir dir1 dir2 -  
  ```  
  Speichern Sie die kombinierte Verzeichnis Auflistung von **dir1** und **dir2** in einer lokalen Datei namens **dirlist. txt.**  
  ```  
  mdir dir1 dir2 dirlist.txt  
  ```  
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
