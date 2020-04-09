---
title: Erweitern
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ab4b9bcb5c9da2aeace71a8e535fa762d6d6e95
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844873"
---
# <a name="expand"></a>Erweitern

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erweitert eine oder mehrere komprimierte Dateien. Mit diesem Befehl können Sie komprimierte Dateien von Verteilungs Datenträgern abrufen.  
## <a name="syntax"></a>Syntax  
```  
expand [/r] <source> <destination>  
expand /r <source> [<destination>]  
expand /i <source> [<destination>]  
expand /d <source>.cab [/f:<files>]  
expand <source>.cab /f:<files> <destination>  
```  
#### <a name="parameters"></a>Parameter  

|  Parameter  |                                                                                                                                                                   Beschreibung                                                                                                                                                                    |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /r      |                                                                                                                                                             benennt Erweiterte Dateien um.                                                                                                                                                              |
|   source    |                                                                              Gibt die Dateien an, die erweitert werden sollen. Die *Quelle* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen. Sie können Platzhalter verwenden ( **\\** \* oder **?** ).                                                                               |
| Ziel | Gibt an, wo Dateien erweitert werden sollen.<p>Wenn die *Quelle* aus mehreren Dateien besteht und Sie **/r**nicht angeben, muss *Destination* ein Verzeichnis sein.<p>Das *Ziel* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen.<p>Ziel Datei &#124; Pfad-Spezifikation. |
|     /i      |                                                                                                   benennt Erweiterte Dateien um, ignoriert jedoch die Verzeichnisstruktur.<p>Dieser Parameter gilt für: Windows Server 2008 R2 und Windows 7.                                                                                                    |
|     /d      |                                                                                                                              Zeigt eine Liste der Dateien am Quell Speicherort an. Die Dateien werden nicht erweitert oder extrahiert.                                                                                                                              |
|     /f:     |                                                                                                                 Gibt die Dateien in einer CAB-Datei an, die Sie erweitern möchten. Sie können Platzhalter verwenden ( **\\** \* oder **?** ).                                                                                                                 |
|     /?      |                                                                                                                                                       Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                       |

## <a name="remarks"></a>Hinweise  
- Verwenden von **Expand** in der Wiederherstellungskonsole  
  Der **Erweiterungs Befehl mit** unterschiedlichen Parametern ist über die Wiederherstellungskonsole verfügbar. Weitere Informationen zur Wiederherstellungskonsole finden Sie im [Artikel 314058](https://support.microsoft.com/kb/314058) in der Microsoft Knowledge Base.  
  ## <a name="additional-references"></a>Weitere Verweise  
  - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
