---
ms.assetid: de054ac2-a386-43ec-a537-c0de21549741
title: Festlegen von Standortverknüpfungseigenschaften
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4fa9a1fa8d2a463fe5f361a5a27ee2b9e3edc0f6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870361"
---
# <a name="setting-site-link-properties"></a>Festlegen von Standortverknüpfungseigenschaften

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gemäß den Eigenschaften der Verbindungsobjekte erfolgt die standortübergreifende Replikation. Wenn die Konsistenzprüfung (KCC) Verbindungsobjekte erstellt wird, wird den Replikationszeitplan von Eigenschaften der Standortverknüpfungsobjekte abgeleitet. Jede Standortverknüpfungsobjekt stellt die Verbindung die wide Area Network (WAN) zwischen zwei oder mehr Standorten dar.  
  
Standortverknüpfungsobjekt-Eigenschaften festlegen, enthält die folgenden Schritte aus:  
  
-   Bestimmen der Kosten, die diesen Replikationspfad zugeordnet ist. Die konsistenzprüfung (KCC) verwendet Kosten, um die kostengünstigste Route für die Replikation zwischen zwei Standorten zu ermitteln, die derselben Verzeichnispartition replizieren.  
  
-   Bestimmen den Zeitplan, der definiert, die Zeiten, in denen die standortübergreifende Replikation auftreten kann.  
  
-   Das Intervall der Replikation wird ermittelt, die definiert, wie häufig Replikation während der Zeiten, die bei der Replikation zulässig ist, erfolgen soll, gemäß dem Zeitplan.  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung  
  
-   [Bestimmen der Kosten](../../ad-ds/plan/Determining-the-Cost.md)  
  
-   [Bestimmen des Zeitplans](../../ad-ds/plan/Determining-the-Schedule.md)  
  
-   [Bestimmen des Intervalls](../../ad-ds/plan/Determining-the-Interval.md)  
  


