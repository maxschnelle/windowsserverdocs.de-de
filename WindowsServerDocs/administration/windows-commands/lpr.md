---
title: lpr
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afc8790b-8b52-45c4-acdf-be0ffa9da534 jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e853933e368f181866963fdcbc1eca5b84bb8c09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374165"
---
# <a name="lpr"></a>lpr

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet eine Datei an einen Computer oder ein Druckerfreigabe Gerät, auf dem der LPD-Dienst (Line Printer Daemon) ausgeführt wird, um den Druck vorzubereiten.  

## <a name="syntax"></a>Syntax  
```  
lpr [-S <ServerName>] -P <printerName> [-C <BannerContent>] [-J <JobName>] [-o | "-o l"] [-x] [-d] <filename>  
```  
## <a name="parameters"></a>Parameter  

|     Parameter      |                                                                                                           Beschreibung                                                                                                           |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  -S <ServerName>   |                                    Gibt (anhand des Namens oder der IP-Adresse) das Computer-oder Druckerfreigabe Gerät an, das die LPD-Drucker Warteschlange mit einem Status hostet, den Sie anzeigen möchten. Erforderlich.                                    |
|  -P <printerName>  |                                                              Gibt (nach Name) den Drucker für die Druck Warteschlange mit einem Status an, den Sie anzeigen möchten. Erforderlich.                                                              |
| -C <BannerContent> |                Gibt den Inhalt an, der auf der Seite Banner des Druckauftrags gedruckt werden soll. Wenn Sie diesen Parameter nicht einschließen, wird der Name des Computers, von dem der Druckauftrag gesendet wurde, auf der Seite Banner angezeigt.                 |
|    -J <JobName>    |                           Gibt den Druckauftrags Namen an, der auf der Bannerseite gedruckt wird. Wenn Sie diesen Parameter nicht einschließen, wird der Name der zu druckenden Datei auf der Seite Banner angezeigt.                            |
| [-o&#124; "-o l"]  | Gibt den Dateityp an, den Sie drucken möchten. Der Parameter **-o** gibt an, dass Sie eine Textdatei drucken möchten. Der Parameter **"-o l"** gibt an, dass Sie eine Binärdatei (z. b. eine PostScript-Datei) drucken möchten. |
|         -d         |              Gibt an, dass die Datendatei vor der Steuerungs Datei gesendet werden muss. Verwenden Sie diesen Parameter, wenn für den Drucker die Datendatei zuerst gesendet werden muss. Weitere Informationen finden Sie in der Druckerdokumentation.               |
|         -x         |                               Gibt an, dass der **LPR** -Befehl mit dem Sun Microsystems-Betriebssystem (als SunOS bezeichnet) für Releases bis einschließlich 4.1.4 _u1 kompatibel sein muss.                                |
|     <FileName>     |                                                                                      Gibt (nach Name) die Datei an, die gedruckt werden soll. Erforderlich.                                                                                      |
|         /?         |                                                                                              Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                               |

## <a name="remarks"></a>Hinweise  
- Um den Namen des Druckers zu ermitteln, öffnen Sie den Ordner Drucker.  
- Bei den Parametern **-S**, **-P**, **-C**und **-J** wird die Groß-/Kleinschreibung beachtet, und Sie müssen in Großbuchstaben eingegeben werden.  
  ## <a name="BKMK_examples"></a>Beispiele  
  In diesem Beispiel wird gezeigt, wie Sie die Textdatei "Document. txt" in der Laserprinter1-Drucker Warteschlange auf einem LPD-Host unter 10.0.0.45 ausdrucken:  
  ```  
  lpr -S 10.0.0.45 -P Laserprinter1 -o Document.txt  
  ```  
  Dieses Beispiel zeigt, wie die Adobe PostScript-Datei "PostScript_file. PS" in der Laserprinter1-Drucker Warteschlange auf einem LPD-Host unter 10.0.0.45 gedruckt wird:  
  ```  
  lpr -S 10.0.0.45 -P Laserprinter1 "-o l" PostScript_file.ps  
  ```  

#### <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
-   [Befehls Verweis drucken](print-command-reference.md)  
