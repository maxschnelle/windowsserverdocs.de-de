---
title: Alle virtuellen Netzwerkadapter müssen aktiviert sein
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b17d647d-a34a-44de-ada6-01a2bf5eeb48
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0a769c3203f6c6946f01cd91b66fbec38af83bbd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837131"
---
# <a name="all-virtual-network-adapters-should-be-enabled"></a>Alle virtuellen Netzwerkadapter müssen aktiviert sein

>Gilt für: Windows Server 2016


  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Eine oder mehrere virtuelle Netzwerkadapter einen physischen Netzwerkadapter zugeordnet werden im Verwaltungsbetriebssystem deaktiviert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Die Konfiguration des Servers ist nicht optimal.*  
  
Das Verwaltungsbetriebssystem kann keine Verbindung herstellen, mit einem physischen (extern) Netzwerk einem physischen Netzwerkadapter auf diesem Computer verwenden, da er einen deaktivierten virtuellen Netzwerkadapter zugeordnet ist.  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Netzwerk- und Interneteinstellungen, um den virtuellen Netzwerkadapter zu aktivieren. Oder Manager für virtuelle Switches verwenden, um den externen virtuellen Switch neu zu konfigurieren, damit sie das Verwaltungsbetriebssystem nicht freigegeben werden.*  
  


