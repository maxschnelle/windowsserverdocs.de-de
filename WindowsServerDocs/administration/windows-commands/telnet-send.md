---
title: Telnet-senden
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 36dc7f861e88cf991af57dda2f150107c6870f0f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441042"
---
# <a name="telnet-send"></a>Telnet: gesendet

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Telnetbefehle an den Telnet-Server gesendet.   
## <a name="syntax"></a>Syntax  
```  
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]  
```  
### <a name="parameters"></a>Parameter  

| Parameter |                     Beschreibung                      |
|-----------|------------------------------------------------------|
|    AO     |       Sendet den Telnetbefehl Ausgabe abzubrechen.        |
|    ayt    |       Sendet den Telnetbefehl werden Sie es.       |
|    brk    |            Sendet die Brk der Telnet-Befehl.            |
|    esc    |      Sendet das aktuelle Telnet-Escape-Zeichen.      |
|    ip     |     Sendet den Telnetbefehl Prozess unterbrechen.     |
|   Synch   |           Sendet die Synchronisierung der Telnet-Befehl.           |
| <string>  | Die Zeichenfolge ein, Sie geben, an den Telnet-Server gesendet. |
|     ?     |     Zeigt die Hilfe im Zusammenhang mit dem folgenden Befehl.      |

## <a name="BKMK_Examples"></a>Beispiele für  
Senden, sind Sie es an den Telnetserver.  
```  
sen ayt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
