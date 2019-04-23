---
title: Stellen Sie sicher, dass ausreichend physischer Speicherplatz verfügbar ist, wenn differenzierenden virtuellen Festplatten, virtuelle Computer verwenden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 71f99aab-f994-4022-9da0-d661965b95ac
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6d4d219402cdc321a75cc27d75ea7749eb6127e0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855571"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-differencing-virtual-hard-disks"></a>Stellen Sie sicher, dass ausreichend physischer Speicherplatz verfügbar ist, wenn differenzierenden virtuellen Festplatten, virtuelle Computer verwenden

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
*Differenzierende virtuelle Festplatten verwenden einen oder mehrere virtuelle Computer.*  
  
## <a name="impact"></a>Auswirkungen  
*Differenzierender virtueller Festplatten erfordert verfügbaren Speicherplatz auf dem Host verwendete Volume, sodass Speicherplatz zugewiesen werden kann, wenn Schreibvorgänge in die virtuellen Festplatten auftreten. Wenn der verfügbare Speicherplatz aufgebraucht ist, kann eine virtuelle Maschine, die abhängig von den physischen Speicher beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Überwachen Sie die verfügbaren Speicherplatz, um sicherzustellen, dass ausreichend Speicherplatz für eine Erweiterung der virtuellen Festplatte verfügbar ist. Beachten Sie, zusammenführen, differenzierende virtuelle Festplatten in ihr übergeordnetes Element. Überprüfen Sie in Hyper-V-Manager des differenzierenden Datenträgers, um zu bestimmen, die übergeordnete virtuelle Festplatte ein. Wenn Sie einen differenzierenden Datenträger an einem übergeordneten Datenträger, die von anderen differenzierenden Datenträgern gemeinsam verwendet wird zusammenführen, wird diese Aktion die Beziehung zwischen den anderen differenzierenden Datenträgern und den übergeordneten Datenträger, sodass sie nicht verwendbar beschädigt. Nachdem Sie überprüft haben, dass die übergeordnete virtuelle Festplatte nicht gemeinsam genutzt wird, können Sie den Assistenten zum Bearbeiten von Datenträger Zusammenführen des differenzierenden Datenträgers, der übergeordneten virtuellen Festplatte.*  
  


