---
title: FTP-ASCII
description: Windows-Befehls Thema für FTP-ASCII
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4930d0d726acaa222f802d7aaef59578030db5f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843783"
---
# <a name="ftp-ascii"></a>FTP: ASCII

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp auf ASCII fest.   
## <a name="syntax"></a>Syntax  
```  
ascii  
```  
#### <a name="parameters"></a>Parameter  
none  
## <a name="remarks"></a>Hinweise  
- Der standardmäßige Datei Übertragungstyp ist ASCII.  
- Im ASCII-Modus werden Zeichen Konvertierungen in und aus dem Netzwerkstandard-Zeichensatz ausgeführt. Beispielsweise werden zeitzeiendezeichen nach Bedarf auf Grundlage des Ziel Betriebssystems konvertiert.  
- **FTP** unterstützt sowohl ASCII-als auch binäre Bilddatei-Übertragungs Typen. Verwenden Sie ASCII beim Übertragen von Textdateien. Weitere Informationen zum Übertragen von Binärdateien finden Sie unter **FTP: Binary** in additional References.  
  ## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
  Legen Sie den Datei Übertragungstyp auf ASCII fest.  
  ```  
  ascii  
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- [FTP: binär](ftp-binary.md)  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
