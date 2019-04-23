---
title: Wiederherstellung von Momentaufnahmen müssen nach dem Failover entfernt werden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 922115fa-e8dd-4055-aaf1-4a4437c5cf28
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4663320df91019fc7dc1d8ca7ffdb2fcc3e0de42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837681"
---
# <a name="recovery-snapshots-should-be-removed-after-failover"></a>Wiederherstellung von Momentaufnahmen müssen nach dem Failover entfernt werden

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016| 
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Ein Failover der virtuellen Computer verfügt über eine oder mehrere Recovery Momentaufnahmen.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Speicherplatz kann auf dem physischen Datenträger erschöpft, in dem die momentaufnahmedateien gespeichert. In diesem Fall können keine zusätzlichen Datenträger-Operationen auf dem physischen Speicher ausgeführt werden. Eine virtuelle Maschine, die auf den physischen Speicher basieren, kann beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie für jeden virtuellen Computer ein Failover das Complete-VMFailover-Cmdlet in Windows PowerShell, entfernen Sie die Momentaufnahmen für die Wiederherstellung und Failover-Abschluss anzugeben.*  
  


