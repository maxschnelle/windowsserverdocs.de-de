---
title: Komprimierung wird für Replikations Datenverkehr empfohlen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cf8be6e9-2909-4e4a-bb63-d1e1ebbc6930
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 77a314e816c36f626ea3edb10b80f65e3897e7c5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365097"
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
*replikations Datenverkehr verwendet mehr Bandbreite als notwendig. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*konfigurieren Sie das Hyper-v-Replikat, um die über das Netzwerk übertragenen Daten in den Einstellungen für den virtuellen Computer im Hyper-v-Manager zu komprimieren. Sie können auch Tools außerhalb von Hyper-V verwenden, um die Komprimierung auszuführen.*  
  


