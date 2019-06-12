---
title: lpr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ddc64f958dcb38129d81becfc8950059e055d8e5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437482"
---
# <a name="lpr"></a>lpr

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sendet eine Datei auf einem Computer oder Geräte, die der Zeile LPD (Printer Daemon)-Dienst ausgeführt wird, als Vorbereitung für das Drucken der Druckerfreigabe.  

## <a name="syntax"></a>Syntax  
```  
lpr [-S <ServerName>] -P <printerName> [-C <BannerContent>] [-J <JobName>] [-o | "-o l"] [-x] [-d] <filename>  
```  
## <a name="parameters"></a>Parameter  

|     Parameter      |                                                                                                           Beschreibung                                                                                                           |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  -S <ServerName>   |                                    Gibt (nach Name oder IP-Adresse) ein, den Computer oder die Druckerfreigabe Gerät, das die LPD-Druckwarteschlange mit dem Status gehostet wird, die Sie anzeigen möchten. Erforderlich.                                    |
|  -P <printerName>  |                                                              Gibt an, (nach Namen) der Drucker für die Druckwarteschlange mit dem Status, den Sie anzeigen möchten. Erforderlich.                                                              |
| -C <BannerContent> |                Gibt den Inhalt auf der Seite "Banner" des Druckauftrags gedruckt. Wenn Sie diesen Parameter nicht einschließen, wird der Name des Computers, von dem der Druckauftrag gesendet wurde, auf der Seite "Banner" angezeigt.                 |
|    -J <JobName>    |                           Gibt den Druckauftrag-Namen, der auf der Seite "Banner" gedruckt werden. Wenn Sie diesen Parameter nicht einschließen, wird der Name der auszugebenden Datei auf der Seite "Banner" angezeigt.                            |
| [-o&#124; "-o l"]  | Gibt den Typ der Datei, die Sie drucken möchten. Der Parameter **- e/a** gibt an, dass Sie eine Textdatei drucken möchten. Der Parameter **"-o-l"** gibt an, dass Sie eine binäre Datei (z. B. PostScript-Datei) drucken möchten. |
|         -d         |              Gibt an, dass die Datendatei muss, bevor die Benutzersteuerelement-Datei gesendet werden. Verwenden Sie diesen Parameter aus, wenn Ihr Drucker das Datendatei, die zuerst gesendet werden muss. Weitere Informationen finden Sie in der Druckerdokumentation.               |
|         -x         |                               Gibt an, dass die **Lpr** Befehl muss mit der Sun Microsystems (bezeichnet als SunOS) Versionen bis zu und einschließlich 4.1.4_u1 kompatibel sein.                                |
|     <FileName>     |                                                                                      Gibt an (nach Namen) der Datei gedruckt werden sollen. Erforderlich.                                                                                      |
|         /?         |                                                                                              Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                               |

## <a name="remarks"></a>Hinweise  
- Um den Namen des Druckers zu suchen, öffnen Sie den Druckerordner.  
- Die **' -s'** , **-P**, **- C**, und **+ J** Parameter wird die Groß-/Kleinschreibung beachtet, und müssen in Großbuchstaben eingegeben werden.  
  ## <a name="BKMK_examples"></a>Beispiele für  
  Dieses Beispiel zeigt, wie die "Dokument.txt." Text-Datei in die Warteschlange des Laserprinter1 Drucker auf einem Host LPD am 10.0.0.45 zu drucken:  
  ```  
  lpr -S 10.0.0.45 -P Laserprinter1 -o Document.txt  
  ```  
  Dieses Beispiel zeigt, wie "PostScript_file.ps" Adobe PostScript-Datei, die Druckerwarteschlange Laserprinter1 auf einem Host LPD am 10.0.0.45 gedruckt:  
  ```  
  lpr -S 10.0.0.45 -P Laserprinter1 "-o l" PostScript_file.ps  
  ```  

#### <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
-   [Druckbefehlsreferenz](print-command-reference.md)  
