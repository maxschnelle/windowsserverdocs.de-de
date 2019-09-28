---
title: verifier
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: cc2482fa25d0236991889c3951cb522e27bf520d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362686"
---
# <a name="verifier"></a>verifier

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Treiberverifier-Manager.  

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
|\<flags >|Muss eine Zahl im Dezimal-oder Hexadezimal Format sein, eine Kombination aus Bits:<br /><br />-   -**Wert: Beschreibung**<br />-   **Bit 0:** Überprüfung des speziellen Pools<br />-   -**Bit 1:** erzwingen der Überprüfung von unql<br />-   **Bit 2:** Simulation mit geringer Ressourcen<br />-   **Bit 3:** Pool Überwachung<br />-   **Bit 4:** E/a-Überprüfung<br />-   **Bit 5:** Deadlockerkennung<br />-   **Bit 6:** nicht verwendet<br />-   **Bit 7:** DMA-Überprüfung<br />-   **Bit 8:** Sicherheitsüberprüfungen<br />-   **Bit 9:** ausstehende e/a-Anforderungen erzwingen<br />-   **Bit 10:** Unp-Protokollierung<br />-   **Bit 11:** sonstige Überprüfungen<br /><br />Beispielsweise entspricht **/Flags 27** **/Flags 0x1B** .|  
|/volatile|Wird verwendet, um die verifizierereinstellungen dynamisch zu ändern, ohne das System neu zu starten. Alle neuen Einstellungen gehen verloren, wenn das System neu gestartet wird.|  
|\<wahrscheinlichkeits >|Zahl zwischen 1 und 10.000, die die Wahrscheinlichkeit für die Fehler Injektion angibt. Wenn Sie z. b. 100 angeben, wird eine Fehler einschleusungs Wahrscheinlichkeit von 1% (100/10000) angegeben.<br /><br />Wenn dieser Parameter nicht angegeben wird, wird die Standard Wahrscheinlichkeit von 6% verwendet.|  
|\<tags >|Gibt die Pooltags an, die durch Leerzeichen getrennt eingefügt werden. Wenn dieser Parameter nicht angegeben wird, kann eine Pool Zuordnung mit Fehlern eingefügt werden.|  
|\<applications >|Gibt den Bilddateinamen der Anwendungen an, die durch Leerzeichen getrennt eingefügt werden. Wenn dieser Parameter nicht angegeben wird, kann es vorkommen, dass eine geringe Ressourcen Simulation in jeder Anwendung stattfindet.|  
|\<minutes >|Eine positive Zahl, die die Länge des Zeitraums nach dem Neustart (in Minuten) angibt, in dem keine Fehler Injektion stattfindet. Wenn dieser Parameter nicht angegeben wird, wird die Standardlänge von 8 Minuten verwendet.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  