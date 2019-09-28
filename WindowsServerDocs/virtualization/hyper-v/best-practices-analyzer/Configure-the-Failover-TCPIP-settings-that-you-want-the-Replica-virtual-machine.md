---
title: Konfigurieren Sie die TCP/IP-Failover-Einstellungen, die der virtuelle Replikat Computer im Falle eines Failovers verwenden soll.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3f2681694d87b34369b29be6216ebec9210c6024
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366288"
---
# <a name="configure-the-failover-tcpip-settings-that-you-want-the-replica-virtual-machine-to-use-in-the-event-of-a-failover"></a>Konfigurieren Sie die TCP/IP-Failover-Einstellungen, die der virtuelle Replikat Computer im Falle eines Failovers verwenden soll.

>Gilt für: Windows Server 2016
 
Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>Problem  
*Virtuelle Replikat Computer, die mit einer statischen IP-Adresse konfiguriert sind, müssen so konfiguriert werden, dass Sie im Fall eines Failovers eine andere IP-Adresse von Ihrem primären virtuellen Computer verwenden.*  
  
## <a name="impact"></a>Auswirkungen  
*clients, die die Arbeitsauslastung verwenden, die vom primären virtuellen Computer unterstützt wird, können nach einem Failover möglicherweise keine Verbindung mit dem virtuellen Replikat Computer herstellen. Außerdem ist die ursprüngliche IP-Adresse des primären virtuellen Computers in der Netzwerktopologie des virtuellen Replikat Computers nicht gültig. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Hyper-V-Manager, um die IP-Adresse zu konfigurieren, die vom virtuellen Replikat Computer bei einem Failover verwendet werden soll.*  
  


