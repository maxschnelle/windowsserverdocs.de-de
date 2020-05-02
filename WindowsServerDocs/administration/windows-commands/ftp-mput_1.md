---
title: FTP-mput_1
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3fb654d5a2f44b9b63238abdbaee8d6a0294861
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725220"
---
# <a name="ftp-mput_1"></a>FTP: mput_1

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Lokale Dateien werden mithilfe des aktuellen Datei Übertragungs Typs auf den Remote Computer kopiert.   
## <a name="syntax"></a>Syntax  
```  
mput <LocalFile>[ ]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter  |                       BESCHREIBUNG                        |
|-------------|----------------------------------------------------------|
| <LocalFile> | Gibt die lokale Datei an, die auf den Remote Computer kopiert werden soll. |

## <a name="examples"></a>Beispiele  
Kopieren Sie **Program1. exe** und **Program2. exe** mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [FTP: ASCII](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
