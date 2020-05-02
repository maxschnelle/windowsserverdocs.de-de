---
title: FTP-mls_1
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 27f74d4c1d03cb4d9f665566f69485e80f8eccdc
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725204"
---
# <a name="ftp-mls_1"></a>FTP: mls_1

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis an.   
## <a name="syntax"></a>Syntax  
```  
mls <remoteFile>[ ] <LocalFile>  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |                       BESCHREIBUNG                       |
|--------------|---------------------------------------------------------|
| <remoteFile> | Gibt die Datei an, für die eine Auflistung angezeigt werden soll. |
| <LocalFile>  |  Gibt eine lokale Datei an, in der die Auflistung gespeichert werden soll.  |

## <a name="remarks"></a>Bemerkungen  
- Angeben von *remotefiles*  
  Geben Sie einen Bindestrich**-**() ein, um das aktuelle Arbeitsverzeichnis auf dem Remote Computer zu verwenden.  
- Angeben von *LocalFile*  
  Geben Sie einen Bindestrich**-**() ein, um die Auflistung auf dem Bildschirm anzuzeigen.  
  ## <a name="examples"></a>Beispiele  
  Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen für **dir1** und **dir2**an.  
  ```  
  mls dir1 dir2 -  
  ```  
  Speichert eine abgekürzte Liste von Dateien und Unterverzeichnissen für **dir1** und **dir2** in der lokalen Datei " **dirlist. txt".**  
  ```  
  mls dir1 dir2 dirlist.txt   
  ```  
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
