---
title: Die erneute Synchronisierung der Replikation sollte außerhalb der Spitzenzeiten geplant werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: ae630f93ef50ebc977de2bffcefa3b27b03622ee
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861793"
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
*Je länger sich ein virtueller Computer in einem Zustand befindet, der eine erneute Synchronisierung erfordert, desto länger werden die Replikations Protokolldateien vergrößert, und die nicht replizierten Änderungen erfolgen auf den primären virtuellen Computern. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Hyper-V-Manager, um die Replikationseinstellungen für die virtuelle Maschine zu ändern und die erneute Synchronisierung außerhalb der Spitzenzeiten automatisch auszuführen.*  
  


