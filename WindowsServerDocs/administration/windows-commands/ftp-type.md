---
title: FTP-Typ
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 36a80fd251794d9bec993d0366551cdc71a4cdf0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842863"
---
# <a name="ftp-type"></a>FTP: Typ

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp fest oder zeigt ihn an.   
## <a name="syntax"></a>Syntax  
```  
type [<typeName>]  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter   |            Beschreibung            |
|--------------|-----------------------------------|
| [<typeName>] | Gibt den Datei Übertragungstyp an. |

## <a name="remarks"></a>Hinweise  
- Wenn *tykame* nicht angegeben ist, wird der aktuelle Typ angezeigt.  
- **FTP** unterstützt zwei Datei Übertragungs Typen, ASCII und Binary.  
  Der standardmäßige Datei Übertragungstyp ist ASCII.  Der **ASCII** -Befehl sollte beim Übertragen von Textdateien verwendet werden. Im ASCII-Modus werden Zeichen Konvertierungen in und aus dem Netzwerkstandard-Zeichensatz ausgeführt. Beispielsweise werden zeitzeiendezeichen nach Bedarf auf Grundlage des Betriebssystems am Ziel konvertiert.  
  Der **binäre** Befehl sollte verwendet werden, wenn ausführbare Dateien übertragen werden. Im Binärmodus wird die Datei in 1-Byte-Einheiten verschoben.  
  ## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
  Legen Sie den Datei Übertragungstyp auf ASCII fest.  
  ```  
  type ascii  
  ```  
  Legen Sie den Dateityp übertragen auf Binär fest.  
  ```  
  type binary  
  ```  
  ## <a name="additional-references"></a>Weitere Verweise  
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
