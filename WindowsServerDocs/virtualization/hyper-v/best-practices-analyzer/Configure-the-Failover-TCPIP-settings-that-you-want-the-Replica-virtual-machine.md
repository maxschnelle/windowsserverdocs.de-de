---
title: Konfigurieren Sie die TCP/IP-Failover-Einstellungen, die der virtuelle Replikat Computer im Falle eines Failovers verwenden soll.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: d2db5fdedbe2f19c01b7dd172f18b6fec969e828
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862053"
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
*Clients, die die Arbeitsauslastung verwenden, die vom primären virtuellen Computer unterstützt wird, können nach einem Failover möglicherweise keine Verbindung mit dem virtuellen Replikat Computer herstellen. Außerdem ist die ursprüngliche IP-Adresse des primären virtuellen Computers in der Netzwerktopologie des virtuellen Replikat Computers nicht gültig. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Hyper-V-Manager, um die IP-Adresse zu konfigurieren, die vom virtuellen Replikat Computer bei einem Failover verwendet werden soll.*  
  


