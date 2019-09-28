---
title: Stellen Sie sicher, dass genügend physischer Speicherplatz verfügbar ist, wenn virtuelle Computer dynamisch erweiterbare virtuelle Festplatten verwenden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9e3e3e64-4b3a-4b9d-acf1-e4df61a04f1e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c38d7c11a05eef9d29097e625fec2830000cf550
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393640"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-dynamically-expanding-virtual-hard-disks"></a>Stellen Sie sicher, dass genügend physischer Speicherplatz verfügbar ist, wenn virtuelle Computer dynamisch erweiterbare virtuelle Festplatten verwenden.

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
*Mindestens eine virtuelle Maschine verwendet dynamisch erweiterbare virtuelle Festplatten.*  
  
## <a name="impact"></a>Auswirkungen  
für dynamisch erweiterbare virtuelle Festplatten, die @no__t werden, ist der verfügbare Speicherplatz auf dem hostingvolume erforderlich, damit Speicherplatz bei Schreibvorgängen auf den virtuellen Festplatten zugeordnet werden kann Wenn der verfügbare Speicherplatz erschöpft ist, kann der virtuelle Computer, der auf dem physischen Speicher basiert, beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus: *  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*monitor verfügbaren Speicherplatz, um sicherzustellen, dass ausreichend Speicherplatz für die Erweiterung verfügbar ist. Sie sollten den virtuellen Computer Herunterfahren und mit dem Assistenten zum Bearbeiten von Datenträgern im Hyper-V-Manager jede dynamisch erweiterbare virtuelle Festplatte für diese virtuelle Maschine in eine virtuelle Festplatte mit fester Größe konvertieren.*  
  


