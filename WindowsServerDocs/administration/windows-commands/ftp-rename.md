---
title: FTP-umbenennen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 977baa042a6b0d9c23db7cb398bee997c2049227
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376024"
---
# <a name="ftp-rename"></a>FTP: Umbenennen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

benennt Remote Dateien um.   
## <a name="syntax"></a>Syntax  
```  
rename <FileName> <NewFileName>  
```  
### <a name="parameters"></a>Parameter  

|   Parameter   |                 Beschreibung                 |
|---------------|---------------------------------------------|
|  <FileName>   | Gibt die Datei an, die Sie umbenennen möchten. |
| <NewFileName> |        Gibt den neuen Dateinamen an.         |

## <a name="BKMK_Examples"></a>Beispiele  
Benennen Sie die Remote Datei **example. txt** in **"example1". txt um.**  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
