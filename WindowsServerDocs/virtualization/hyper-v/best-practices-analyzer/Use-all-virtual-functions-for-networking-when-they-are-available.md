---
title: Alle virtuellen Funktionen für das Netzwerk verwenden, wenn diese verfügbar sind
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8798a7021b3df0113b8d957340d6d688acead5c7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393348"
---
# <a name="use-all-virtual-functions-for-networking-when-they-are-available"></a>Alle virtuellen Funktionen für das Netzwerk verwenden, wenn diese verfügbar sind

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
*Einige Hardware Beschleunigungsfunktionen werden nicht verwendet.*  
  
## <a name="impact"></a>Auswirkungen  
*diese Konfiguration kann dazu führen, dass die CPU-Gesamtauslastung höher als notwendig ist. Die Netzwerkleistung ist auf den folgenden virtuellen Computern möglicherweise nicht optimal:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*Sie sollten den virtuellen Netzwerkadapter für SR-IOV konfigurieren, wenn die physische Hardware SR-IOV unterstützt und wenn diese Konfiguration nicht mit den Netzwerk Features in Konflikt steht, die für die virtuelle Maschine erforderlich sind.*  
  


