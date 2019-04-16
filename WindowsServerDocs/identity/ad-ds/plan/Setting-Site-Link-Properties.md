---
ms.assetid: de054ac2-a386-43ec-a537-c0de21549741
title: "Festlegen von Standortverknüpfungseigenschaften"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 495ed006ecac5458877191a14060c5fd4b746d96
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="setting-site-link-properties"></a>Festlegen von Standortverknüpfungseigenschaften

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Erfolgt die standortübergreifende Replikation gemäß den Eigenschaften der Verbindungsobjekte. Wenn Verbindungsobjekte (Knowledge Consistency Checker, KCC) erstellt wird, wird von den Eigenschaften der Standortverknüpfungsobjekte Zeitplans für die Replikation abgeleitet. Jedes Standortverknüpfungsobjekt stellt die Verbindung der wide Area Network (WAN) zwischen zwei oder mehr Standorten dar.  
  
Festlegen von Standortverknüpfungseigenschaften Objekt enthält die folgenden Schritteaus:  
  
-   Bestimmen der Kosten, die die Replikationspfad zugeordnet ist. Die Konsistenzprüfung (KCC) verwendet Kosten zum Bestimmen der kostengünstigsten Route für die Replikation zwischen zwei Standorten, die derselben Verzeichnispartition replizieren.  
  
-   Bestimmen des Zeitplans, die definiert, die Zeiten, in denen die standortübergreifende Replikation auftreten kann.  
  
-   Bestimmen das Intervall der Replikation, die definiert, wie häufig Replikation während der Zeiten, wenn der Replikation zugelassen wird, erfolgen soll, wie in den Zeitplan definiert.  
  
## <a name="in-this-guide"></a>In diesem Handbuch  
  
-   [Bestimmen der Kosten](../../ad-ds/plan/Determining-the-Cost.md)  
  
-   [Bestimmen des Zeitplans](../../ad-ds/plan/Determining-the-Schedule.md)  
  
-   [Bestimmen des Intervalls](../../ad-ds/plan/Determining-the-Interval.md)  
  


