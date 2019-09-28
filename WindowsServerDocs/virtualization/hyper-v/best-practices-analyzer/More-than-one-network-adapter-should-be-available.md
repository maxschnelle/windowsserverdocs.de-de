---
title: Es sollten mehrere Netzwerkadapter verfügbar sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6b043900c6fde4522e5805a1f0c1a635de335e31
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364797"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>Es sollten mehrere Netzwerkadapter verfügbar sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Fehler|  
|**Kategorie**|Konfiguration|  

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem  
  
*Dieser Server ist mit einem Netzwerkadapter konfiguriert, der vom Verwaltungs Betriebssystem und allen virtuellen Computern gemeinsam genutzt werden muss, die Zugriff auf ein physisches Netzwerk benötigen.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Die Netzwerkleistung kann im Verwaltungs Betriebssystem beeinträchtigt werden.*  
  
## <a name="resolution"></a>Auflösung  
  
*fügen Sie diesem Computer weitere Netzwerkadapter hinzu. Um einen Netzwerkadapter für die ausschließliche Verwendung durch das Verwaltungs Betriebssystem zu reservieren, konfigurieren Sie ihn nicht für die Verwendung mit einem externen virtuellen Netzwerk.*  
  
Weitere Informationen zum Hinzufügen eines Netzwerkadapters zum Computer finden Sie in der Dokumentation für den Computer oder den Netzwerkadapter. Um es dann ausschließlich für das Verwaltungs Betriebssystem zu reservieren, verbinden Sie es nicht mit einem virtuellen Switch.   
  


