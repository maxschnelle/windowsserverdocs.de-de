---
title: Komprimierung wird für den Replikationsdatenverkehr empfohlen.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cf8be6e9-2909-4e4a-bb63-d1e1ebbc6930
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 802f11355bec8903e7f6ab81bf337d38e64513f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833511"
---
# <a name="compression-is-recommended-for-replication-traffic"></a>Komprimierung wird für den Replikationsdatenverkehr empfohlen.

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
*Der Replikationsdatenverkehr vom primären Server zum Replikatserver über das Netzwerk gesendet werden nicht komprimiert.*  
  
## <a name="impact"></a>Auswirkungen  
*Replikationsdatenverkehr verwendet mehr Bandbreite als nötig. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Konfigurieren Sie Hyper-V-Replikat so, die in den Einstellungen für den virtuellen Computer im Hyper-V-Manager über das Netzwerk übertragenen Daten zu komprimieren. Sie können auch Tools außerhalb von Hyper-V verwenden, Komprimierung ausführen.*  
  


