---
title: Das Test Failover sollte nach Abschluss der ersten Replikation versucht werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cea7eeaa-c1a7-4f87-89be-d4e1208c546f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ec3ad3994227eb14d1d2e53842c755af76ac538d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364699"
---
# <a name="test-failover-should-be-attempted-after-initial-replication-is-complete"></a>Das Test Failover sollte nach Abschluss der ersten Replikation versucht werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="problem"></a>Problem  
*Es gab in mindestens einem Monat kein Test Failover.*  
  
## <a name="impact"></a>Auswirkungen  
*es gibt keine Bestätigung, dass ein geplantes oder ungeplantes Failover erfolgreich ist oder Arbeits Auslastungs Vorgänge nach einem Failover ordnungsgemäß fortgesetzt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Hyper-V-Manager, um ein Test Failover durchzuführen.*  
  


