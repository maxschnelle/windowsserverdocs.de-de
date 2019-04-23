---
title: Stellen Sie sicher, dass ausreichend physischer Speicherplatz verfügbar ist, wenn der virtuelle Computer verwenden, dynamisch erweiterbare virtuelle Festplatten
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9e3e3e64-4b3a-4b9d-acf1-e4df61a04f1e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 09e481b99594ac543dadab2b60bf9b3f4c29e54b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883291"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-dynamically-expanding-virtual-hard-disks"></a>Stellen Sie sicher, dass ausreichend physischer Speicherplatz verfügbar ist, wenn der virtuelle Computer verwenden, dynamisch erweiterbare virtuelle Festplatten

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
*Dynamisch erweiterbare virtuelle Festplatten verwenden einen oder mehrere virtuelle Computer.*  
  
## <a name="impact"></a>Auswirkungen  
*Dynamisch erweiterbare virtueller Festplatten erfordert verfügbaren Speicherplatz auf dem Host verwendete Volume, sodass Speicherplatz zugewiesen werden kann, wenn Schreibvorgänge in die virtuellen Festplatten auftreten. Wenn der verfügbare Speicherplatz aufgebraucht ist, kann eine virtuelle Maschine, die abhängig von den physischen Speicher beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verfügbaren Speicherplatz überwachen, um sicherzustellen, dass ausreichend Speicherplatz ist für eine Erweiterung verfügbar. Betrachten Sie den virtuellen Computer wird heruntergefahren, und verwenden Sie den Assistenten zum Bearbeiten von Datenträger in Hyper-V-Manager, um jede dynamisch erweiterbare virtuelle Festplatte für diese virtuelle Maschine in eine feste Größe virtuelle Festplatte konvertieren.*  
  


