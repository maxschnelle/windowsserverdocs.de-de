---
ms.assetid: 96a6749c-6c9f-4f2f-ad0a-51272d282ace
title: Bestimmen des Intervalls
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d5eb824b3b15c8b0734b2df23b79649778b28e9d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="determining-the-interval"></a>Bestimmen des Intervalls

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie müssen angeben, wie häufig Sie während der Zeiten auftreten, wenn der Zeitplan Replikation ermöglicht die, Replikation soll die Website Link Replikation Intervall-Eigenschaft festlegen. Wenn beispielsweise Sie der Zeitplan ermöglicht die Replikation von 02:00 Uhr bis 04:00 Uhr und das Intervall der Replikation ist für 30Minuten festgelegt Replikation kann bis zu vier Mal während der geplanten Zeit erfolgen. Das Standardintervall für die Replikation beträgt 180Minuten oder 3 Stunden. Das Mindestintervall ist 15Minuten.  
  
Berücksichtigen Sie die folgenden Kriterien fest, wie oft erfolgt die Replikation innerhalb des Fensters planen:  
  
-   Ein kleines Intervall verringert die Latenz, erhöht aber die Menge des Datenverkehrs von wide Area Network (WAN).  
  
-   Um Domänenverzeichnispartitionen aktuell zu halten, wird mit geringer Latenz bevorzugt.  
  
Mit einer Store-and-Forward-Replikationsstrategie ist es schwierig zu bestimmen, wie lange ein Verzeichnisupdate dauern kann, auf alle Domänencontroller repliziert werden sollen. Um eine konservative Schätzung der maximale Wartezeit zu ermöglichen, müssen führen Sie diese Aufgaben aus:  
  
-   Erstellen Sie eine Tabelle mit allen Standorten in Ihrem Netzwerk, wie im folgenden Beispiel dargestellt:  
  
    |Standorte|Seattle|Boston|Los Angeles|New York|Washington, D.C.|  
    |---------|-----------|----------|---------------|------------|--------------------|  
    |Seattle|0.25|||||  
    |Boston||0.25||||  
    |Los Angeles|||0.25|||  
    |New York||||0.25||  
    |Washington, D.C.|||||0.25|  
  
    Eine maximale Wartezeit innerhalb eines Standorts schätzungsweise 15Minuten lang ausfallen.  
  
-   Der Replikationszeitplan ermitteln Sie die maximale Replikationswartezeit, die auf einen beliebigen Link Standort möglich ist, die zwei Hubstandorte verbindet.  
  
    Wenn die Replikation zwischen Seattle und New York alle drei Stunden erfolgt, ist die maximale Verzögerung für die Replikation zwischen diesen Standorten z.B. drei Stunden. Die replikationsverzögerung zwischen New York und Seattle ist die längste geplanten Verzögerung zwischen allen Hubstandorten, die maximale Wartezeit zwischen den Hubs alle drei Stunden.  
  
-   Erstellen Sie eine Tabelle der maximalen Latenzen zwischen dem Hubstandort und dessen Satelliten-Standorte, für jeden Hubstandort.  
  
    Wenn die Replikation zwischen New York und Washington, D.C., alle vier Stunden, und dies ist die längste replikationsverzögerung zwischen New York und dessen Satelliten-Standorte, ist die maximale Wartezeit zwischen New York und zugehörigen Satelliten vier Stunden.  
  
-   Kombinieren Sie diese maximalen Latenzzeiten, um die maximale Wartezeit für das gesamte Netzwerk zu ermitteln.  
  
    Beispielsweise ist die maximale Wartezeit zwischen Seattle und dem Satelliten-Standort in Los Angeles einen Tag, die maximale Replikationswartezeit für diesen Satz von Links (Washington, D.C.-New York-Seattle-Los Angeles) ist 31 Stunden, d.h. 4 (Washington, D.C.-New York) + 3 (New York Seattle) + 24 (Seattle-Los Angeles), wie in der folgenden Tabelle dargestellt.  
  
    |Standorte|Seattle|Boston|Los Angeles|New York|Washington, D.C.|  
    |---------|-----------|----------|---------------|------------|--------------------|  
    |Seattle|0.25|4+3|24.00|3.00|4+3|  
    |Boston||0.25|4+3+24|4.00|4.00|  
    |Los Angeles|||0.25|24 + 3|24+3+4|  
    |New York||||0.25|4.00|  
    |Washington, D.C.|||||0.25|  
  


