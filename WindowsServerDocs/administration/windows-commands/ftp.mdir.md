---
title: FTP-mdir
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: afb024d063761f1e817f02fdd7301376dd167846
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842713"
---
# <a name="ftp-mdir"></a>FTP: mdir

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Verzeichnisliste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis an.   
## <a name="syntax"></a>Syntax  
```  
mdir <remoteFile>[ ] <LocalFile>  
```  
#### <a name="parameters"></a>Parameter  

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
  ## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
  Anzeigen einer Verzeichnisliste von **dir1** und **dir2** auf dem Bildschirm  
  ```  
  mdir dir1 dir2 -  
  ```  
  Speichern Sie die kombinierte Verzeichnis Auflistung von **dir1** und **dir2** in einer lokalen Datei namens **dirlist. txt.**  
  ```  
  mdir dir1 dir2 dirlist.txt  
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
