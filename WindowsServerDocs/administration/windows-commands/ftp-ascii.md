---
title: FTP-ASCII
description: 'Windows-Befehls Thema für FTP-ASCII '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5ae0064f9c1679bb8b386271f042d589b158c73
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376620"
---
# <a name="ftp-ascii"></a>FTP: ASCII

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp auf ASCII fest.   
## <a name="syntax"></a>Syntax  
```  
ascii  
```  
### <a name="parameters"></a>Parameter  
none  
## <a name="remarks"></a>Hinweise  
- Der standardmäßige Datei Übertragungstyp ist ASCII.  
- Im ASCII-Modus werden Zeichen Konvertierungen in und aus dem Netzwerkstandard-Zeichensatz ausgeführt. Beispielsweise werden zeitzeiendezeichen nach Bedarf auf Grundlage des Ziel Betriebssystems konvertiert.  
- **FTP** unterstützt sowohl ASCII-als auch binäre Bilddatei-Übertragungs Typen. Verwenden Sie ASCII beim Übertragen von Textdateien. Weitere Informationen zum Übertragen von Binärdateien finden Sie unter **FTP: Binary** in additional References.  
  ## <a name="BKMK_Examples"></a>Beispiele  
  Legen Sie den Datei Übertragungstyp auf ASCII fest.  
  ```  
  ascii  
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- [FTP: binär](ftp-binary.md)  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
