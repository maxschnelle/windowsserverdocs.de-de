---
title: Es sollten mehrere Netzwerkadapter verfügbar sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 56cb747ac44d48b115dbf105ea96e4623d458b28
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861893"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>Es sollten mehrere Netzwerkadapter verfügbar sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Konfiguration|  

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem  
  
*Dieser Server ist mit einem Netzwerkadapter konfiguriert, der vom Verwaltungs Betriebssystem und allen virtuellen Computern gemeinsam genutzt werden muss, die Zugriff auf ein physisches Netzwerk benötigen.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Die Netzwerkleistung kann im Verwaltungs Betriebssystem beeinträchtigt werden.*  
  
## <a name="resolution"></a>Auflösung  
  
*Fügen Sie diesem Computer weitere Netzwerkadapter hinzu. Um einen Netzwerkadapter für die ausschließliche Verwendung durch das Verwaltungs Betriebssystem zu reservieren, sollten Sie ihn nicht für die Verwendung mit einem externen virtuellen Netzwerk konfigurieren.*  
  
Weitere Informationen zum Hinzufügen eines Netzwerkadapters zum Computer finden Sie in der Dokumentation für den Computer oder den Netzwerkadapter. Um es dann ausschließlich für das Verwaltungs Betriebssystem zu reservieren, verbinden Sie es nicht mit einem virtuellen Switch.   
  


