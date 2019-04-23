---
title: Dynamischer Arbeitsspeicher ist aktiviert, aber für einige virtuelle Maschinen reagiert nicht
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 91b7f50f-a071-4ab6-beb1-1b29f92f52b6
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 95fd426929f3e2f6f01bc10b207a21a57f1d8370
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887781"
---
# <a name="dynamic-memory-is-enabled-but-not-responding-on-some-virtual-machines"></a>Dynamischer Arbeitsspeicher ist aktiviert, aber für einige virtuelle Maschinen reagiert nicht

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Eine oder mehrere virtuelle Computer treten Probleme mit dem Treiber für dynamischen Arbeitsspeicher in Gast-Betriebssystems erforderlich.*  
  
## <a name="impact"></a>Auswirkungen  
*Das Gastbetriebssystem in die folgenden virtuellen Computer möglicherweise nicht ausgeführt oder kann die ausführungsgeschwindigkeit unberechenbar Verhalten da Hyper-V nicht den Arbeitsspeicher dynamisch, um die Reaktion auf Änderungen in den Arbeitsspeicher bei Bedarf anpassen kann. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Dies ist Erwartetes Verhalten, wenn der virtuelle Computer gestartet wird. Wenn die virtuelle Maschine nicht startet, stellen Sie sicher, dass Integrationsservices auf die neueste Version aktualisiert werden und das Gastbetriebssystem dynamischen Arbeitsspeicher unterstützt.*  
  
Ab Windows Server 2016 werden die Integrationsdienste über Windows Update bereitgestellt. Stellen Sie sicher, dass die virtuellen Computer konfiguriert sind, um Updates, um die neueste Version von Integrationsservices zu erhalten.  
  
Dynamischer Arbeitsspeicher funktioniert mit bestimmten Versionen der unterstützten Gäste. Finden Sie unter [Hyper-V dynamischer Arbeitsspeicher – Übersicht](https://technet.microsoft.com/library/hh831766.aspx) für Versionen vor Windows Server 2016 und Windows 10.  
  


