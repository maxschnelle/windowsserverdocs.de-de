---
title: Für Server in Failoverclustern muss ein Hyper-V-Replikat Broker konfiguriert sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 921d31aa63bcaaf0946c487d327144f5e29bcfe0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854583"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>Für Server in Failoverclustern muss ein Hyper-V-Replikat Broker konfiguriert sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Für Failovercluster erfordert das Hyper-v-Replikat die Verwendung eines Hyper-v-Replikat Broker-namens anstelle eines einzelnen Server namens.*  
  
## <a name="impact"></a>Auswirkungen  
*Wenn die virtuelle Maschine auf einen anderen Failoverclusterknoten verschoben wird, kann die Replikation nicht fortgesetzt werden.*  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie Failovercluster-Manager zum Konfigurieren des Hyper-V-Replikat Brokers. Stellen Sie im Hyper-v-Manager sicher, dass die Replikationskonfiguration den Namen des Hyper-v-Replikat Brokers als Servernamen verwendet.*  
  


