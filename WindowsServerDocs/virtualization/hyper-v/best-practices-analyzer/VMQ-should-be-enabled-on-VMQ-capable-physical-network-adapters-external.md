---
title: VMQ muss auf VMQ-fähig physischen Netzwerkadaptern, die an einen externen virtuellen Switch gebunden aktiviert werden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 93d1b155-bf44-46b0-bb69-d34d5b30e574
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9a552c15675e6ca7a7310c8c9eaec883653987be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889471"
---
# <a name="vmq-should-be-enabled-on-vmq-capable-physical-network-adapters-bound-to-an-external-virtual-switch"></a>VMQ muss auf VMQ-fähig physischen Netzwerkadaptern, die an einen externen virtuellen Switch gebunden aktiviert werden

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
*Die folgenden Netzwerkadapter werden der Warteschlange für virtuelle Computer (VMQ) kann die Funktion ist jedoch deaktiviert.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Windows kann nicht der verfügbaren Hardware abladungen optimal auf die folgenden Netzwerkadapter nutzen:*  
  
\<Liste der Netzwerkadapter >  
  
## <a name="resolution"></a>**Lösung**  
*Aktivieren Sie VMQ, mithilfe des Enable-NetAdapterVmq Windows PowerShell-Cmdlets oder die Benutzeroberfläche für erweiterte Eigenschaften für den Netzwerkadapter an.*  
  


