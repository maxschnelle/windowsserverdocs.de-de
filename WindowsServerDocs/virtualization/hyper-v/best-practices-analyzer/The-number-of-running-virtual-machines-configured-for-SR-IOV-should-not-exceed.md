---
title: Die Anzahl der für SR-IOV konfigurierten virtuellen Computer sollte nicht die Anzahl der virtuellen Funktionen überschreiten, die für die virtuellen Maschinen verfügbar sind.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 3c58e980471284c950f41551b02b92bf74aca7cc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854613"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>Die Anzahl der für SR-IOV konfigurierten virtuellen Computer sollte nicht die Anzahl der virtuellen Funktionen überschreiten, die für die virtuellen Maschinen verfügbar sind.

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
*Für die Anzahl der für die e/a-Virtualisierung mit Einzel Stamm (Single-root I/O Virtualization, SR-IOV) konfigurierten virtuellen Maschinen sind nicht genügend virtuelle Funktionen verfügbar.*  
  
## <a name="impact"></a>Auswirkungen  
*Die Netzwerkleistung ist auf den folgenden virtuellen Computern möglicherweise nicht optimal:*  
   
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Deaktivieren Sie ggf. SR-IOV auf einem oder mehreren virtuellen Computern, für die keine virtuelle SR-IOV-Funktion erforderlich ist.*  
  


