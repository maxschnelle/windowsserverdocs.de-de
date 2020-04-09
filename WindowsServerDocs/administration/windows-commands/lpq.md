---
title: lpq
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bb6abcc4-310a-4fa4-927b-4084b62ca02e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 051b1983fcc0fddd7b69e561c0a27a120f78d998
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840393"
---
# <a name="lpq"></a>lpq

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt den Status einer Druck Warteschlange auf einem Computer an, auf dem der Line Printer Daemon (LPD) ausgeführt wird.  

## <a name="syntax"></a>Syntax  
```  
lpq -S <ServerName> -P <printerName> [-l]  
```  
### <a name="parameters"></a>Parameter  

|    Parameter     |                                                                        Beschreibung                                                                        |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| -S <ServerName>  | Gibt (anhand des Namens oder der IP-Adresse) das Computer-oder Druckerfreigabe Gerät an, das die LPD-Drucker Warteschlange mit einem Status hostet, den Sie anzeigen möchten. Erforderlich |
| -P <printerName> |                           Gibt (nach Name) den Drucker für die Druck Warteschlange mit einem Status an, den Sie anzeigen möchten. Erforderlich                           |
|        -l        |                                      Gibt an, dass Details zum Status der Druck Warteschlange angezeigt werden sollen.                                      |
|        /?        |                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                            |

## <a name="remarks"></a>Hinweise  
Bei den Parametern **-S** und **-P** muss die Groß-/Kleinschreibung beachtet werden, und Sie müssen in Großbuchstaben eingegeben werden.  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Dieses Beispiel zeigt, wie Sie den Status der Laserprinter1-Drucker Warteschlange auf einem LPD-Host unter 10.0.0.45 anzeigen:  
```  
lpq -S 10.0.0.45 -P Laserprinter1  
```  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Befehls Verweis drucken](print-command-reference.md)  
