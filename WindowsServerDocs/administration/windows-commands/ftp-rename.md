---
title: FTP-umbenennen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bbe159f2833ce52921b46e46881a1d7aed8c5df8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843023"
---
# <a name="ftp-rename"></a>FTP: Umbenennen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

benennt Remote Dateien um.   
## <a name="syntax"></a>Syntax  
```  
rename <FileName> <NewFileName>  
```  
#### <a name="parameters"></a>Parameter  

|   Parameter   |                 Beschreibung                 |
|---------------|---------------------------------------------|
|  <FileName>   | Gibt die Datei an, die Sie umbenennen möchten. |
| <NewFileName> |        Gibt den neuen Dateinamen an.         |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Benennen Sie die Remote Datei **example. txt** in **"example1". txt um.**  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
