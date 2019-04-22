---
ms.assetid: 96a6749c-6c9f-4f2f-ad0a-51272d282ace
title: Bestimmen des Intervalls
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 57b282102f10a595ce3842ac3a4eb1d289b86d22
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822161"
---
# <a name="determining-the-interval"></a>Bestimmen des Intervalls

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie müssen festlegen, dass die Site Link Replikation Interval-Eigenschaft, um anzugeben, wie oft die Replikation während der Zeiten auftreten, wenn der Zeitplan Replikation kann, soll. Z. B. wenn der Zeitplan ermöglicht die Replikation zwischen 04:00 Uhr, 02:00 Uhr und das Intervall der Replikation wird für 30 Minuten festgelegt Replikation kann bis zu vier Mal während der geplanten Zeit stattfinden. Das Standardintervall für die Replikation beträgt 180 Minuten oder 3 Stunden. Das minimale Intervall beträgt 15 Minuten.  
  
Berücksichtigen Sie die folgenden Kriterien fest, wie oft erfolgt Replikation innerhalb der Planungszeitraum:  
  
-   Einen kurzen Zeitraum verringert die Latenz erhöht jedoch die die Menge des Datenverkehrs für wide Area Network (WAN).  
  
-   Um Domänenverzeichnispartitionen auf dem neuesten Stand zu halten, wird mit geringer Latenz bevorzugt.  
  
Mit einer Strategie für die speichern-und-Weiterleiten-Replikation ist es schwierig zu bestimmen, wie lange ein Verzeichnisupdate dauern kann, auf jedem Domänencontroller repliziert werden sollen. Um eine konservative Schätzung der maximalen Latenz zu ermöglichen, müssen führen Sie diese Aufgaben aus:  
  
-   Erstellen Sie eine Tabelle mit allen Standorten in Ihrem Netzwerk an, wie im folgenden Beispiel gezeigt:  
  
    |Websites|Seattle|Boston|Los Angeles|New York|Washington, D.C.|  
    |---------|-----------|----------|---------------|------------|--------------------|  
    |Seattle|0.25|||||  
    |Boston||0.25||||  
    |Los Angeles|||0.25|||  
    |New York||||0.25||  
    |Washington, D.C.|||||0.25|  
  
    Eine Worst-Case Latenz innerhalb eines Standorts wird auf 15 Minuten werden geschätzt.  
  
-   Anhand der Replikationszeitplan ermitteln Sie die maximale Replikationswartezeit an, die auf einen beliebigen Link Standort möglich ist, die zwei nabenstandorten verbindet.  
  
    Wenn die Replikation zwischen Seattle und New York alle drei Stunden auftritt, ist die maximale Verzögerung für die Replikation zwischen diesen Standorten beispielsweise drei Stunden. Die replikationsverzögerung zwischen der New York "und" Seattle ist die längste geplante Verzögerung zwischen allen Hubstandorten, die maximale Latenz zwischen allen Hubs drei Stunden.  
  
-   Erstellen Sie eine Tabelle mit die maximale Latenz zwischen dem Hubstandort und dessen Satelliten-Standorte, für jeden Hubstandort.  
  
    Beispielsweise ist die maximale Latenz zwischen New York und dessen Satelliten Wenn wird die Replikation zwischen New York "und" Washington, D.C., alle vier Stunden, und dies die längste replikationsverzögerung zwischen der New York und dessen Satelliten-Standorte ist, vier Stunden.  
  
-   Kombinieren Sie diese maximale Latenz, um die maximale Latenzzeit für das gesamte Netzwerk zu ermitteln.  
  
    Die maximale Latenz zwischen Seattle und dessen Satellitenstandort in Los Angeles beispielsweise ein Tag, die maximale Replikationswartezeit für diesen Satz von Links (Washington, D.C.-in New York-Seattle-Berlin) ist 31 Stunden, d. h. 4 (Washington, D.C.-in New York) + (neu 3 York-Seattle) + 24 (Seattle-Berlin), wie in der folgenden Tabelle gezeigt.  
  
    |Websites|Seattle|Boston|Los Angeles|New York|Washington, D.C.|  
    |---------|-----------|----------|---------------|------------|--------------------|  
    |Seattle|0.25|4+3|24.00|3.00|4+3|  
    |Boston||0.25|4+3+24|4,00|4,00|  
    |Los Angeles|||0.25|24 + 3|24+3+4|  
    |New York||||0.25|4,00|  
    |Washington, D.C.|||||0.25|  
  


