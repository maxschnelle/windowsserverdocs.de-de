---
title: Serielle Ports dürfen nicht auf virtuellen Maschinen der Generation 2 konfiguriert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 87061193-dd3f-4398-aa5d-4cee83cadfa3
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8a8c15076921efa0e1e791a18c6a45ea1bf27b0e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364727"
---
# <a name="serial-ports-should-not-be-configured-on-generation-2-virtual-machines"></a>Serielle Ports dürfen nicht auf virtuellen Maschinen der Generation 2 konfiguriert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Für mindestens einen virtuellen Computer der Generation 2 ist ein serieller Port konfiguriert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Die Leistung kann für die folgenden virtuellen Computer beeinträchtigt werden:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>**Auflösung**  
*wenn dies beabsichtigt ist, ist keine weitere Aktion erforderlich. Andernfalls sollten Sie den Hyper-V-Manager oder Windows PowerShell verwenden, um die Verbindungs Zeichenfolge aus den seriellen Anschlüssen auf dem virtuellen Computer zu entfernen.*  
  


