---
title: Die Replikation für mindestens eine virtuelle Maschine auf diesem Server wurde angehalten.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: e1119a40-eda3-4058-8648-7df81cbc6c29
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 6974016dd564cf19d39a6d83b041020a4e327d2c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861813"
---
# <a name="replication-is-paused-for-one-or-more-virtual-machines-on-this-server"></a>Die Replikation für mindestens eine virtuelle Maschine auf diesem Server wurde angehalten.

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
*Die Replikation für mindestens einen virtuellen Computer wurde angehalten. Während der primäre virtuelle Computer angehalten wird, werden alle auftretenden Änderungen akkumuliert und an den virtuellen Replikat Computer gesendet, sobald die Replikation fortgesetzt wird.*  
  
## <a name="impact"></a>Auswirkungen  
*Solange die Replikation angehalten ist, verbrauchen akkumulierte Änderungen, die auf dem primären virtuellen Computer auftreten, den verfügbaren Speicherplatz auf dem primären Server. Nach dem Fortsetzen der Replikation kann es zu einem großen Anstieg des Netzwerk Datenverkehrs zum Replikat Server kommen. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Vergewissern Sie sich, dass das Anhalten der Replikation beabsichtigt war Wenn die Replikation angehalten wurde, um wenig Speicherplatz oder Netzwerk Konnektivität zu beheben, setzen Sie die Replikation fort, sobald diese Probleme behoben sind.*  
  


