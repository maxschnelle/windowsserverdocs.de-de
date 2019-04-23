---
title: verifier
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 782173d6-f196-4bc4-a547-76109829453c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ab0833d4fdb11c4962d4916ec2e32097e08ca04
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865871"
---
# <a name="verifier"></a>verifier

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Treiberüberprüfungs-Manager.  

## <a name="syntax"></a>Syntax  
```  
verifier /standard /driver <name> [<name> ...]  
verifier /standard /all  
verifier [/flags <flags>] [/faults [<probability> [<tags> [<applications> [<minutes>]]]] /driver <name> [<name>...]  
verifier [/flags FLAGS] [/faults [<probability> [<tags> [<applications> [<minutes>]]]] /all  
verifier /querysettings  
verifier /volatile /flags <flags>  
verifier /volatile /adddriver <name> [<name>...]  
verifier /volatile /removedriver <name> [<name>...]  
verifier /volatile /faults [<probability> [<tags> [<applications>]]  
verifier /reset  
verifier /query  
verifier /log <LogFileName> [/interval <seconds>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|\<flags>|Eine Zahl in Dezimal oder Hexadezimal, eine Kombination von Bits muss sein:<br /><br />-   **Wert: Beschreibung**<br />-   **Bit 0:** spezieller Pool überprüfen<br />-   **Um Bit 1:** Irql-Überprüfung zu erzwingen<br />-   **Bit 2:** wenig Ressourcen Simulation<br />-   **Bit 3:** Pool nachverfolgen<br />-   **bit 4:** E/a-Überprüfung<br />-   **Bit-5:** deadlock Erkennung<br />-   **6 Bit:** nicht verwendet<br />-   **bit 7:** DMA-Überprüfung<br />-   **8-Bit:** sicherheitsüberprüfungen<br />-   **9-Bit:** ausstehende e/a-Anforderungen erzwingen<br />-   **bit 10:** IRP-Protokollierung<br />-   **Bit-11:** verschiedene Überprüfungen<br /><br />z. B. **/27 flags** ist gleichbedeutend mit   **/flags 0x1B**|  
|/volatile|Verwendet, um die Einstellungen für die Verifier dynamisch zu ändern, ohne einen Neustart des Systems. Wenn das System neu gestartet wird, werden alle neuen Einstellungen verloren gehen.|  
|\<probability>|Zahl zwischen 1 und 10.000 angeben der Wahrscheinlichkeit der Fault Injection. Angeben von 100 bedeutet beispielsweise, eine Fault Injection-Wahrscheinlichkeit von 1 % (100/10.000).<br /><br />Wenn dieser Parameter nicht angegeben ist, wird der standardwahrscheinlichkeit 6 % verwendet werden.|  
|\<tags>|Gibt die Pooltags, die eingefügt werden mit Fehlern, die durch Leerzeichen getrennt an. Wenn dieser Parameter nicht angegeben ist, kann auf die Pool-Zuweisung mit Fehlern eingefügt werden.|  
|\<applications>|Gibt den Namen der Bilddatei der Anwendungen, die eingefügt werden mit Fehlern, die durch Leerzeichen getrennt an. Wenn dieser Parameter nicht angegeben ist kann dann Simulation unzureichender Ressourcen in jeder Anwendung stattfinden.|  
|\<minutes>|Eine positive Zahl, die die Länge des Zeitraums nach dem Neustart werden in Minuten an, während ohne die Fault Injection angelaufen wird. Wenn dieser Parameter nicht angegeben ist, wird die standardmäßige Länge 8 Minuten verwendet werden.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="additional-references"></a>Weitere Verweise  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  