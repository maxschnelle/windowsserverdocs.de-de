---
title: Serielle Anschlüsse sollte auf virtuelle Maschinen der Generation 2 nicht konfiguriert werden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 87061193-dd3f-4398-aa5d-4cee83cadfa3
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 58c3fc5f975b85ce17ac5f7cca4930ec9e851e07
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877381"
---
# <a name="serial-ports-should-not-be-configured-on-generation-2-virtual-machines"></a>Serielle Anschlüsse sollte auf virtuelle Maschinen der Generation 2 nicht konfiguriert werden

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Eine oder mehrere Generation müssen 2 virtuellen Computern einen seriellen Anschluss konfiguriert.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Für die folgenden virtuellen Computer kann die Leistung beeinträchtigen:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Wenn dies beabsichtigt ist, ist keine weitere Aktion erforderlich. Erwägen Sie andernfalls, Hyper-V-Manager oder Windows PowerShell verwenden, um die Verbindungszeichenfolge aus der seriellen Anschlüsse auf dem virtuellen Computer zu entfernen.*  
  


