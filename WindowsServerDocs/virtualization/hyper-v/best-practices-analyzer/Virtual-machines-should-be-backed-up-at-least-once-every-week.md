---
title: Virtuelle Computer sollten mindestens einmal pro Woche gesichert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ec11b067de2c9f8cbb3a17731caa0dc526bf54a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393237"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>Virtuelle Computer sollten mindestens einmal pro Woche gesichert werden.

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
*Mindestens eine virtuelle Maschine wurde in der letzten Woche nicht gesichert.*  
  
## <a name="impact"></a>Auswirkungen  
ein signifikanter Datenverlust @no__t 0 kann auftreten, wenn auf dem virtuellen Computer ein Problem auftritt und keine aktuelle Sicherung vorhanden ist. Dies wirkt sich auf die folgenden virtuellen Computer aus: *  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*planen Sie eine Sicherung der virtuellen Computer so, dass Sie mindestens einmal pro Woche ausgeführt wird. Diese Regel kann ignoriert werden, wenn es sich bei dieser virtuellen Maschine um ein Replikat handelt und der primäre virtuelle Computer gesichert wird, oder wenn dies der primäre virtuelle Computer ist und das zugehörige Replikat gesichert wird.*  
  


