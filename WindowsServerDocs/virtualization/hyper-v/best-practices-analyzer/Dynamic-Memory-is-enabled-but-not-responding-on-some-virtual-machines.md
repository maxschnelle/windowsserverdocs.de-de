---
title: Dynamischer Arbeitsspeicher ist aktiviert, reagiert aber nicht auf einigen virtuellen Computern.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 91b7f50f-a071-4ab6-beb1-1b29f92f52b6
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9aa482d91c94a7a619bb65046cf152d6a5f8827a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393676"
---
# <a name="dynamic-memory-is-enabled-but-not-responding-on-some-virtual-machines"></a>Dynamischer Arbeitsspeicher ist aktiviert, reagiert aber nicht auf einigen virtuellen Computern.

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
*Bei mindestens einer virtuellen Maschine treten Probleme mit dem Treiber auf, der für dynamischer Arbeitsspeicher im Gast Betriebssystem erforderlich ist.*  
  
## <a name="impact"></a>Auswirkungen  
*Das Gast Betriebssystem auf den folgenden virtuellen Computern kann möglicherweise nicht ausgeführt werden oder nicht zuverlässig ausgeführt werden, da Hyper-V den Speicher nicht dynamisch anpassen kann, um auf Änderungen bei der Speichernachfrage zu reagieren. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*dies ist das erwartete Verhalten, wenn der virtuelle Computer gestartet wird. Wenn die virtuelle Maschine nicht gestartet wird, stellen Sie sicher, dass die Integrationsdienste auf die neueste Version aktualisiert werden und dass das Gast Betriebssystem dynamischer Arbeitsspeicher unterstützt.*  
  
Ab Windows Server 2016 werden Integrationsdienste über Windows Update bereitgestellt. Stellen Sie sicher, dass die virtuellen Computer für den Empfang von Updates zum Abrufen der neuesten Version von Integration Services konfiguriert sind.  
  
Dynamischer Arbeitsspeicher funktioniert mit bestimmten Versionen von unterstützten Gästen. Weitere Informationen finden Sie unter [Übersicht über Hyper-V-dynamischer Arbeitsspeicher](https://technet.microsoft.com/library/hh831766.aspx) für ältere Versionen als Windows Server 2016 und Windows 10.  
  


