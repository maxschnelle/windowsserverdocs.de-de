---
title: FTP-umbenennen
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5dc5006c82df8417a8652a9c0ba20f7f1a002e7f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725117"
---
# <a name="ftp-rename"></a>FTP: Umbenennen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

benennt Remote Dateien um.   
## <a name="syntax"></a>Syntax  
```  
rename <FileName> <NewFileName>  
```  
#### <a name="parameters"></a>Parameter  

|   Parameter   |                 BESCHREIBUNG                 |
|---------------|---------------------------------------------|
|  <FileName>   | Gibt die Datei an, die Sie umbenennen möchten. |
| <NewFileName> |        Gibt den neuen Dateinamen an.         |

## <a name="examples"></a>Beispiele  
Benennen Sie die Remote Datei **example. txt** in **"example1". txt um.**  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
