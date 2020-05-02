---
title: FTP-Binärdatei
description: Referenz Thema für FTP-Binärdatei
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ee925b4d-85d2-47b1-b7d6-3832b7ec5505 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60a3e84bf9256dd5c71dd4444b5939980eecc512
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725373"
---
# <a name="ftp-binary"></a>FTP: binär

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp auf Binary fest.   
## <a name="syntax"></a>Syntax  
```  
binary  
```  
#### <a name="parameters"></a>Parameter  
none  
## <a name="remarks-optional-section"></a>Rede<optional section>  
**FTP** unterstützt sowohl ASCII-als auch binäre Bilddatei-Übertragungs Typen. Verwenden Sie Binärdateien beim Übertragen von ausführbaren Dateien. Im Binärmodus werden Dateien in 1-Byte-Einheiten übertragen. Weitere Informationen zum Übertragen von ASCII-Dateien finden Sie unter **FTP: ASCII** in additional References.  
## <a name="examples"></a>Beispiele  
Legen Sie den Datei Übertragungstyp auf Binär fest.  
```  
binary  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [FTP: ASCII](ftp-ascii.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
