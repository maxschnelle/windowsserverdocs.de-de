---
title: FTP-mls_1
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a84a0f8f3121ea19876744e9ef04bebf5f9fcb08
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376260"
---
# <a name="ftp-mls_1"></a>FTP: mls_1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis an.   
## <a name="syntax"></a>Syntax  
```  
mls <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                       Beschreibung                       |
|--------------|---------------------------------------------------------|
| <remoteFile> | Gibt die Datei an, für die eine Auflistung angezeigt werden soll. |
| <LocalFile>  |  Gibt eine lokale Datei an, in der die Auflistung gespeichert werden soll.  |

## <a name="remarks"></a>Hinweise  
- Angeben von *remotefiles*  
  Geben Sie einen Bindestrich ( **-** ) ein, um das aktuelle Arbeitsverzeichnis auf dem Remote Computer zu verwenden.  
- Angeben von *LocalFile*  
  Geben Sie einen Bindestrich ( **-** ) ein, um die Auflistung auf dem Bildschirm anzuzeigen.  
  ## <a name="BKMK_Examples"></a>Beispiele  
  Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen für **dir1** und **dir2**an.  
  ```  
  mls dir1 dir2 -  
  ```  
  Speichert eine abgekürzte Liste von Dateien und Unterverzeichnissen für **dir1** und **dir2** in der lokalen Datei " **dirlist. txt".**  
  ```  
  mls dir1 dir2 dirlist.txt   
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
