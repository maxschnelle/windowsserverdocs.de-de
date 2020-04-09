---
title: Komprimierung wird für Replikations Datenverkehr empfohlen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cf8be6e9-2909-4e4a-bb63-d1e1ebbc6930
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: aca66991eae57d702f38e2282eeb4253bc1cd244
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857663"
---
# <a name="compression-is-recommended-for-replication-traffic"></a>Komprimierung wird für Replikations Datenverkehr empfohlen

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
*Der Replikations Datenverkehr, der vom primären Server zum Replikat Server über das Netzwerk gesendet wird, ist nicht komprimiert.*  
  
## <a name="impact"></a>Auswirkungen  
*Der Replikations Datenverkehr verwendet mehr Bandbreite als notwendig. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Konfigurieren Sie das Hyper-v-Replikat, um die über das Netzwerk übertragenen Daten in den Einstellungen für den virtuellen Computer im Hyper-v-Manager zu komprimieren. Sie können auch Tools außerhalb von Hyper-V verwenden, um die Komprimierung auszuführen.*  
  


