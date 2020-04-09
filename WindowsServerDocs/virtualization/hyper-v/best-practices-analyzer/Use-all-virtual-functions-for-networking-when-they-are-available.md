---
title: Alle virtuellen Funktionen für das Netzwerk verwenden, wenn diese verfügbar sind
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 0fab06ae21a4632df73b7a4d8b17b12665ffed98
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854213"
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
*Diese Konfiguration kann dazu führen, dass die CPU-Gesamtauslastung höher als notwendig ist. Die Netzwerkleistung ist auf den folgenden virtuellen Computern möglicherweise nicht optimal:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Sie sollten den virtuellen Netzwerkadapter für SR-IOV konfigurieren, wenn die physische Hardware SR-IOV unterstützt und wenn diese Konfiguration nicht mit den Netzwerk Features in Konflikt steht, die für die virtuelle Maschine erforderlich sind.*  
  


