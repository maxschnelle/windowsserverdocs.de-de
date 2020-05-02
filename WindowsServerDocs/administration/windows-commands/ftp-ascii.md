---
title: FTP-ASCII
description: Referenz Thema für FTP-ASCII
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aa33637f43ef8d26635f36b40dbd21cfe2bff42e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725394"
---
# <a name="ftp-ascii"></a>FTP: ASCII

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp auf ASCII fest.   
## <a name="syntax"></a>Syntax  
```  
ascii  
```  
#### <a name="parameters"></a>Parameter  
none  
## <a name="remarks"></a>Bemerkungen  
- Der standardmäßige Datei Übertragungstyp ist ASCII.  
- Im ASCII-Modus werden Zeichen Konvertierungen in und aus dem Netzwerkstandard-Zeichensatz ausgeführt. Beispielsweise werden zeitzeiendezeichen nach Bedarf auf Grundlage des Ziel Betriebssystems konvertiert.  
- **FTP** unterstützt sowohl ASCII-als auch binäre Bilddatei-Übertragungs Typen. Verwenden Sie ASCII beim Übertragen von Textdateien. Weitere Informationen zum Übertragen von Binärdateien finden Sie unter **FTP: Binary** in additional References.  
  ## <a name="examples"></a>Beispiele  
  Legen Sie den Datei Übertragungstyp auf ASCII fest.  
  ```  
  ascii  
  ```  
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
- [FTP: binär](ftp-binary.md)  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
