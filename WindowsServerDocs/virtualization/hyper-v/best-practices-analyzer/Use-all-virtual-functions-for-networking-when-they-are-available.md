---
title: Verwenden Sie alle virtuelle Funktionen für Netzwerke, sobald diese verfügbar sind
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3ad120ffa689f1f7dcae832432e216ebda57e62f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877791"
---
# <a name="use-all-virtual-functions-for-networking-when-they-are-available"></a>Verwenden Sie alle virtuelle Funktionen für Netzwerke, sobald diese verfügbar sind

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
*Einige Funktionen der Hardware-Beschleunigung werden nicht verwendet wird*  
  
## <a name="impact"></a>Auswirkungen  
*Diese Konfiguration kann dazu führen, dass CPU-Gesamtauslastung höher als nötig sein. Netzwerkleistung möglicherweise nicht optimal auf die folgenden virtuellen Computer:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Erwägen Sie den virtuellen Netzwerkadapter für SR-IOV konfigurieren, wenn physische Hardware unterstützt, SR-IOV und diese Konfiguration nicht zu Konflikten mit der Netzwerkfunktionen, die von der virtuellen Maschine erforderlich.*  
  


