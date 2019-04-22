---
title: expand
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5df078af23c77f54ccb2da83b1057c5d7042593a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825961"
---
# <a name="expand"></a>expand

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Erweitert eine oder mehrere komprimierte Dateien an. Sie können diesen Befehl verwenden, um komprimierte Dateien von Originaldatenträgern abrufen.  
## <a name="syntax"></a>Syntax  
```  
expand [/r] <source> <destination>  
expand /r <source> [<destination>]  
expand /i <source> [<destination>]  
expand /d <source>.cab [/f:<files>]  
expand <source>.cab /f:<files> <destination>  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/r|Benennt erweiterte Dateien.|  
|Quelle|Gibt die Dateien zu erweitern. *Quelle* kann einen Laufwerkbuchstaben und Doppelpunkt, ein Verzeichnisname, einen Dateinamen oder eine Kombination aus diesen bestehen. Sie können Platzhalter verwenden (**\*** oder **?**).|  
|Ziel|Gibt an, in dem die Dateien erweitert werden.<br /><br />Wenn *Quelle* besteht aus mehreren Dateien, und Sie keinen **/r**, *Ziel* muss ein Verzeichnis sein.<br /><br />*Ziel* kann einen Laufwerkbuchstaben und Doppelpunkt, ein Verzeichnisname, einen Dateinamen oder eine Kombination aus diesen bestehen.<br /><br />Zieldatei &#124; Pfadangabe.|  
|/i|Benennt die erweiterte Dateien werden jedoch ignoriert die Verzeichnisstruktur.<br /><br />Dieser Parameter gilt für:  Windows Server 2008 R2 und Windows 7.|  
|/d|Zeigt eine Liste der Dateien am Quellspeicherort. Erweitern Sie oder Extrahieren Sie die Dateien nicht.|  
|/f:|Gibt die Dateien in einer CAB-Datei, die Sie erweitern möchten. Sie können Platzhalter verwenden (**\*** oder **?**).|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  
## <a name="remarks"></a>Hinweise  
-   Mithilfe von **erweitern** auf die Recovery-Konsole  
    Die **erweitern** ist der Befehl mit anderen Parametern, aus dem Recovery-Konsole verfügbar. Weitere Informationen über die Recovery-Konsole finden Sie unter [Artikel 314058](https://support.microsoft.com/kb/314058) in der Microsoft Knowledge Base.  
## <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
