---
title: FTP-Typ
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eb254d1c9b17ac6baadf6b84702d2812f1117a93
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375896"
---
# <a name="ftp-type"></a>FTP: Typ

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp fest oder zeigt ihn an.   
## <a name="syntax"></a>Syntax  
```  
type [<typeName>]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |            Beschreibung            |
|--------------|-----------------------------------|
| [<typeName>] | Gibt den Datei Übertragungstyp an. |

## <a name="remarks"></a>Hinweise  
- Wenn *tykame* nicht angegeben ist, wird der aktuelle Typ angezeigt.  
- **FTP** unterstützt zwei Datei Übertragungs Typen, ASCII und Binary.  
  Der standardmäßige Datei Übertragungstyp ist ASCII.  Der **ASCII** -Befehl sollte beim Übertragen von Textdateien verwendet werden. Im ASCII-Modus werden Zeichen Konvertierungen in und aus dem Netzwerkstandard-Zeichensatz ausgeführt. Beispielsweise werden zeitzeiendezeichen nach Bedarf auf Grundlage des Betriebssystems am Ziel konvertiert.  
  Der **binäre** Befehl sollte verwendet werden, wenn ausführbare Dateien übertragen werden. Im Binärmodus wird die Datei in 1-Byte-Einheiten verschoben.  
  ## <a name="BKMK_Examples"></a>Beispiele  
  Legen Sie den Datei Übertragungstyp auf ASCII fest.  
  ```  
  type ascii  
  ```  
  Legen Sie den Dateityp übertragen auf Binär fest.  
  ```  
  type binary  
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
