---
title: Wiederherstellungs Momentaufnahmen sollten nach dem Failover entfernt werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 922115fa-e8dd-4055-aaf1-4a4437c5cf28
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4b8574956fb1b46ca0cf9678187fffcd68c2d261
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393527"
---
# <a name="recovery-snapshots-should-be-removed-after-failover"></a>Wiederherstellungs Momentaufnahmen sollten nach dem Failover entfernt werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016| 
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Für einen virtuellen Computer, für den ein Failover ausgeführt wurde, ist mindestens ein Wiederherstellungs*  
  
## <a name="impact"></a>**Auswirkt**  
auf dem physischen Datenträger, auf dem die Momentaufnahme Dateien gespeichert werden, kann *verfüg barer Speicherplatz auftreten. In diesem Fall können keine weiteren Datenträger Vorgänge für den physischen Speicher ausgeführt werden. Jeder virtuelle Computer, der auf dem physischen Speicher basiert, kann beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>**Auflösung**  
*Verwenden Sie für jeden virtuellen Computer, für den ein Failover ausgeführt wurde, das Complete-vmfailover-Cmdlet in Windows PowerShell, um die Wiederherstellungs Momentaufnahmen zu entfernen und die Failover*  
  


