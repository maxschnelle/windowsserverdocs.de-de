---
title: FTP-Typ
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a261382da47501b416fa83c6d2497deae5711bb1
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438354"
---
# <a name="ftp-type"></a>FTP: Typ

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt den Dateityp für die Übertragung an ab oder legt ihn fest.   
## <a name="syntax"></a>Syntax  
```  
type [<typeName>]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |            Beschreibung            |
|--------------|-----------------------------------|
| [<typeName>] | Gibt den Dateiübertragungstyp an. |

## <a name="remarks"></a>Hinweise  
- Wenn *TypeName* nicht angegeben ist, wird der aktuelle Typ angezeigt wird.  
- **FTP** unterstützt zwei Datei Übertragungstypen ASCII und binär.  
  Der Standardtyp ist ASCII.  Die **Ascii** Befehl sollte verwendet werden, bei der Übertragung von Textdateien. Im ASCII-Modus werden zeichenkonvertierungen in und aus dem Netzwerk-standard-Zeichensatz ausgeführt. Beispielsweise werden End-of-Line-Zeichen konvertiert, wenn erforderlich, auf der Grundlage des Betriebssystems am Ziel.  
  Die **binäre** Befehl sollte verwendet werden, wenn die Übertragung von ausführbaren Dateien. In diesem Modus wird die Datei im byteweise verschoben.  
  ## <a name="BKMK_Examples"></a>Beispiele für  
  Den Dateityp für die Übertragung auf ASCII festgelegt.  
  ```  
  type ascii  
  ```  
  Legen Sie die Übertragung Dateityp in einen Binärwert.  
  ```  
  type binary  
  ```  
  ## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
