---
title: Bei der Replikation beteiligt sein soll, müssen Server im Failovercluster eine Hyper-V-Replikatbroker konfiguriert haben.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: d4966396af955f9c8bad34b5b2892115e93c3b85
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887971"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>Bei der Replikation beteiligt sein soll, müssen Server im Failovercluster eine Hyper-V-Replikatbroker konfiguriert haben.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Bei Failoverclustern erfordert Hyper-V-Replikat für die Verwendung eines Hyper-V-Replikatbroker-Namens anstelle eines einzelnen Server an.*  
  
## <a name="impact"></a>Auswirkungen  
*Wenn der virtuelle Computer in einem anderen Failoverclusterknoten verschoben wird, kann nicht die Replikation fortgesetzt.*  
  
## <a name="resolution"></a>Auflösung  
*Mit Failovercluster-Manager die Hyper-V-Replikatbroker konfigurieren. In Hyper-V-Manager stellen Sie sicher, dass die Replikationskonfiguration den Hyper-V-Replikatbroker-Namen als den Namen des Servers verwendet.*  
  


