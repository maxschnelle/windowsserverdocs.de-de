---
title: Mehr als einem Netzwerkadapter sollte verfügbar sein.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 678c0161e97b8dd022bbf0037d9add5de0281f77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884601"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>Mehr als einem Netzwerkadapter sollte verfügbar sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  

In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem  
  
*Dieser Server wird konfiguriert, mit einem Netzwerkadapter und vom Verwaltungsbetriebssystem freigegeben werden muss und alle virtuellen Computer, die Zugriff auf einem physischen Netzwerk erforderlich ist.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Netzwerkleistung kann im Verwaltungsbetriebssystem beeinträchtigt.*  
  
## <a name="resolution"></a>Auflösung  
  
*Fügen Sie für diesen Computer mehrere Netzwerkadapter hinzu. Um einen Netzwerkadapter für die ausschließliche Verwendung durch das Verwaltungsbetriebssystem reserviert werden muss, nicht konfigurieren Sie für die Verwendung mit einem externen virtuellen Netzwerk.*  
  
Informationen zum Hinzufügen von eines Netzwerkadapters auf dem Computer finden Sie in der Dokumentation für den Computer oder den Netzwerkadapter. Um es ausschließlich für das Verwaltungsbetriebssystem reserviert werden sollen, verbinden Sie nicht ihn mit einem virtuellen Switch.   
  


