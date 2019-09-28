---
title: FTP-mput_1
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6308f7b47d58bc25d964944f96fbc83a26350962
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376213"
---
# <a name="ftp-mput_1"></a>FTP: mput_1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Lokale Dateien werden mithilfe des aktuellen Datei Übertragungs Typs auf den Remote Computer kopiert.   
## <a name="syntax"></a>Syntax  
```  
mput <LocalFile>[ ]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter  |                       Beschreibung                        |
|-------------|----------------------------------------------------------|
| <LocalFile> | Gibt die lokale Datei an, die auf den Remote Computer kopiert werden soll. |

## <a name="BKMK_Examples"></a>Beispiele  
Kopieren Sie **Program1. exe** und **Program2. exe** mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: ASCII](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
