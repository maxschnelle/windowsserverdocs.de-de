---
title: lpq
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb6abcc4-310a-4fa4-927b-4084b62ca02e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a3755c010c9bb4549deed08f26b5a0670fe7318
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374205"
---
# <a name="lpq"></a>lpq

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt den Status einer Druck Warteschlange auf einem Computer an, auf dem der Line Printer Daemon (LPD) ausgeführt wird.  

## <a name="syntax"></a>Syntax  
```  
lpq -S <ServerName> -P <printerName> [-l]  
```  
## <a name="parameters"></a>Parameter  

|    Parameter     |                                                                        Beschreibung                                                                        |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| -S <ServerName>  | Gibt (anhand des Namens oder der IP-Adresse) das Computer-oder Druckerfreigabe Gerät an, das die LPD-Drucker Warteschlange mit einem Status hostet, den Sie anzeigen möchten. Erforderlich. |
| -P <printerName> |                           Gibt (nach Name) den Drucker für die Druck Warteschlange mit einem Status an, den Sie anzeigen möchten. Erforderlich.                           |
|        -l        |                                      Gibt an, dass Details zum Status der Druck Warteschlange angezeigt werden sollen.                                      |
|        /?        |                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                            |

## <a name="remarks"></a>Hinweise  
Bei den Parametern **-S** und **-P** muss die Groß-/Kleinschreibung beachtet werden, und Sie müssen in Großbuchstaben eingegeben werden.  
## <a name="BKMK_examples"></a>Beispiele  
Dieses Beispiel zeigt, wie Sie den Status der Laserprinter1-Drucker Warteschlange auf einem LPD-Host unter 10.0.0.45 anzeigen:  
```  
lpq -S 10.0.0.45 -P Laserprinter1  
```  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Befehls Verweis drucken](print-command-reference.md)  
