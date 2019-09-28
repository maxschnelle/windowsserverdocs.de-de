---
title: Die erneute Synchronisierung der Replikation sollte außerhalb der Spitzenzeiten geplant werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 379f8c8cd6744fe5db176efb55a84f231ce45857
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393512"
---
# <a name="resynchronization-of-replication-should-be-scheduled-for-off-peak-hours"></a>Die erneute Synchronisierung der Replikation sollte außerhalb der Spitzenzeiten geplant werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Die erneute Synchronisierung der Replikation für die primären virtuellen Computer ist außerhalb der Spitzenzeiten nicht geplant.*  
  
## <a name="impact"></a>Auswirkungen  
*je länger sich ein virtueller Computer in einem Zustand befindet, der eine erneute Synchronisierung erfordert, desto länger werden die Replikations Protokolldateien vergrößert, und die nicht replizierten Änderungen erfolgen auf den primären virtuellen Computern. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Hyper-V-Manager, um die Replikationseinstellungen für die virtuelle Maschine zu ändern und die erneute Synchronisierung außerhalb der Spitzenzeiten automatisch auszuführen.*  
  


