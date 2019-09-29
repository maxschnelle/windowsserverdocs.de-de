---
title: expand
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a88222ffe9ff374626a6406c330a6660d992f96
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377321"
---
# <a name="expand"></a>expand

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erweitert eine oder mehrere komprimierte Dateien. Mit diesem Befehl können Sie komprimierte Dateien von Verteilungs Datenträgern abrufen.  
## <a name="syntax"></a>Syntax  
```  
expand [/r] <source> <destination>  
expand /r <source> [<destination>]  
expand /i <source> [<destination>]  
expand /d <source>.cab [/f:<files>]  
expand <source>.cab /f:<files> <destination>  
```  
### <a name="parameters"></a>Parameter  

|  Parameter  |                                                                                                                                                                   Beschreibung                                                                                                                                                                    |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /r      |                                                                                                                                                             benennt Erweiterte Dateien um.                                                                                                                                                              |
|   Quelle    |                                                                              Gibt die Dateien an, die erweitert werden sollen. Die *Quelle* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen. Sie können Platzhalter ( **\\** \* oder **?** ) verwenden.                                                                               |
| Entwickelt | Gibt an, wo Dateien erweitert werden sollen.<br /><br />Wenn die *Quelle* aus mehreren Dateien besteht und Sie **/r**nicht angeben, muss *Destination* ein Verzeichnis sein.<br /><br />Das *Ziel* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen.<br /><br />Ziel Datei &#124; Pfad-Spezifikation. |
|     /i      |                                                                                                   benennt Erweiterte Dateien um, ignoriert jedoch die Verzeichnisstruktur.<br /><br />Dieser Parameter gilt für:  Windows Server 2008 R2 und Windows 7.                                                                                                    |
|     /d      |                                                                                                                              Zeigt eine Liste der Dateien am Quell Speicherort an. Die Dateien werden nicht erweitert oder extrahiert.                                                                                                                              |
|     /f:     |                                                                                                                 Gibt die Dateien in einer CAB-Datei an, die Sie erweitern möchten. Sie können Platzhalter ( **\\** \* oder **?** ) verwenden.                                                                                                                 |
|     /?      |                                                                                                                                                       Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                       |

## <a name="remarks"></a>Hinweise  
- Verwenden von **Expand** in der Wiederherstellungskonsole  
  Der **Erweiterungs Befehl mit** unterschiedlichen Parametern ist über die Wiederherstellungskonsole verfügbar. Weitere Informationen zur Wiederherstellungskonsole finden Sie im [Artikel 314058](https://support.microsoft.com/kb/314058) in der Microsoft Knowledge Base.  
  ## <a name="additional-references"></a>Weitere Verweise  
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
