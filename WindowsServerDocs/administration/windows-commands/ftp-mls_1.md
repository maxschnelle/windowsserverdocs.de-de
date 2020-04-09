---
title: FTP-mls_1
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca3b8e04dd4a152b2d1bf8ce1ca8006d70186116
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843293"
---
# <a name="ftp-mls_1"></a>FTP: mls_1

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis an.   
## <a name="syntax"></a>Syntax  
```  
mls <remoteFile>[ ] <LocalFile>  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                       Beschreibung                       |
|--------------|---------------------------------------------------------|
| <remoteFile> | Gibt die Datei an, für die eine Auflistung angezeigt werden soll. |
| <LocalFile>  |  Gibt eine lokale Datei an, in der die Auflistung gespeichert werden soll.  |

## <a name="remarks"></a>Hinweise  
- Angeben von *remotefiles*  
  Geben Sie einen Bindestrich ( **-** ) ein, um das aktuelle Arbeitsverzeichnis auf dem Remote Computer zu verwenden.  
- Angeben von *LocalFile*  
  Geben Sie einen Bindestrich ( **-** ) ein, um die Auflistung auf dem Bildschirm anzuzeigen.  
  ## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
  Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen für **dir1** und **dir2**an.  
  ```  
  mls dir1 dir2 -  
  ```  
  Speichert eine abgekürzte Liste von Dateien und Unterverzeichnissen für **dir1** und **dir2** in der lokalen Datei " **dirlist. txt".**  
  ```  
  mls dir1 dir2 dirlist.txt   
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
