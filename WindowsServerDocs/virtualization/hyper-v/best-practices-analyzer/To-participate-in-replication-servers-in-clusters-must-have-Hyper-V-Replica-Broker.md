---
title: Für Server in Failoverclustern muss ein Hyper-V-Replikat Broker konfiguriert sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2e15d2c4a467807397ef4712d2df1730b40d8024
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364599"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>Für Server in Failoverclustern muss ein Hyper-V-Replikat Broker konfiguriert sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Für Failovercluster erfordert das Hyper-v-Replikat die Verwendung eines Hyper-v-Replikat Broker-namens anstelle eines einzelnen Server namens.*  
  
## <a name="impact"></a>Auswirkungen  
*Wenn die virtuelle Maschine auf einen anderen Failoverclusterknoten verschoben wird, kann die Replikation nicht fortgesetzt werden.*  
  
## <a name="resolution"></a>Auflösung  
*verwenden Sie Failovercluster-Manager, um den Hyper-V-Replikat Broker zu konfigurieren. Stellen Sie im Hyper-v-Manager sicher, dass die Replikationskonfiguration den Namen des Hyper-v-Replikat Brokers als Servernamen verwendet.*  
  


