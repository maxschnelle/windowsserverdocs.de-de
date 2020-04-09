---
title: Serielle Ports dürfen nicht auf virtuellen Maschinen der Generation 2 konfiguriert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 87061193-dd3f-4398-aa5d-4cee83cadfa3
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: d9cfb8db2dc3fdff32544670d9443632c2d2264e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861783"
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
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Wenn dies beabsichtigt ist, ist keine weitere Aktion erforderlich. Andernfalls sollten Sie den Hyper-V-Manager oder Windows PowerShell verwenden, um die Verbindungs Zeichenfolge aus den seriellen Anschlüssen auf dem virtuellen Computer zu entfernen.*  
  


