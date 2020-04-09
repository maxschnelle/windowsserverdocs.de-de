---
title: FTP-mput_1
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 489e18da937e12a1fc69e0ee84d9dda00309ccd6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843233"
---
# <a name="ftp-mput_1"></a>FTP: mput_1

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Lokale Dateien werden mithilfe des aktuellen Datei Übertragungs Typs auf den Remote Computer kopiert.   
## <a name="syntax"></a>Syntax  
```  
mput <LocalFile>[ ]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter  |                       Beschreibung                        |
|-------------|----------------------------------------------------------|
| <LocalFile> | Gibt die lokale Datei an, die auf den Remote Computer kopiert werden soll. |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Kopieren Sie **Program1. exe** und **Program2. exe** mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: ASCII](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
