---
title: FTP-mdir
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c4ec445c3e367a46dc40d10a37c0b3b8e53a10e3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438332"
---
# <a name="ftp-mdir"></a>ftp: mdir

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt eine Verzeichnisliste von Dateien und Unterverzeichnisse in einem Remoteverzeichnis.   
## <a name="syntax"></a>Syntax  
```  
mdir <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                               Beschreibung                                |
|--------------|--------------------------------------------------------------------------|
| <remoteFile> |   Gibt an, das Verzeichnis oder die Datei aus, für das eine Liste angezeigt werden sollen.   |
| <LocalFile>  | Gibt eine lokale Datei zum Speichern der Liste an. Dieser Parameter ist erforderlich. |

## <a name="remarks"></a>Hinweise  
- Sie können **Mdir** um mehrere Dateien anzugeben.  
- Angeben von *Remotedatei*  
  Geben Sie einen Bindestrich ( **-** ) auf das aktuelle Arbeitsverzeichnis auf dem Remotecomputer zu verwenden.  
- Angeben einer *LocalFile*  
  Geben Sie einen Bindestrich ( **-** ) um die Auflistung auf dem Bildschirm anzuzeigen.  
  ## <a name="BKMK_Examples"></a>Beispiele für  
  Zeigt eine Liste des **dir1** und **dir2** auf dem Bildschirm  
  ```  
  mdir dir1 dir2 -  
  ```  
  Speichern Sie kombinierte verzeichnisauflistung des **dir1** und **dir2** in einer lokalen Datei namens **Verliste.txt**  
  ```  
  mdir dir1 dir2 dirlist.txt  
  ```  
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
