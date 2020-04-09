---
title: Konfigurieren von Gastbetriebssystemen für VSS-basierte Sicherungen zum Aktivieren von Anwendungs konsistenten Momentaufnahmen für Hyper-V-Replikate
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7638e996-d42d-47b8-a670-1e09e7183850
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: f7a77b2cb743f478525f839e1c64ecc892b3fb04
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862063"
---
# <a name="configure-guest-operating-systems-for-vss-based-backups-to-enable-application-consistent-snapshots-for-hyper-v-replica"></a>Konfigurieren von Gastbetriebssystemen für VSS-basierte Sicherungen zum Aktivieren von Anwendungs konsistenten Momentaufnahmen für Hyper-V-Replikate

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Anwendungs konsistente Momentaufnahmen erfordert, dass die Volumeschattenkopie-Dienste (VSS) in den Gastbetriebssystemen der an der Replikation beteiligten virtuellen Computer aktiviert und konfiguriert werden.*  
  
## <a name="impact"></a>Auswirkungen  
*Auch wenn Anwendungs konsistente Momentaufnahmen in der Replikationskonfiguration angegeben werden, werden diese von Hyper-V nur verwendet, wenn VSS konfiguriert ist. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie die Verbindung mit dem virtuellen Computer, um Integration Services auf dem virtuellen Computer zu installieren.*  
  


