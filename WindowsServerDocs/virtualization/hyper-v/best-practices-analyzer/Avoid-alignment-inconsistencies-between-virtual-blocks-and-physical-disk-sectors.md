---
title: Vermeiden von Ausrichtungs Inkonsistenzen zwischen virtuellen und physischen Datenträger Sektoren auf dynamischen virtuellen Festplatten oder differenzierenden Datenträgern
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: f77d80db1e2454eb460043cacef632e979fc16de
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366492"
---
# <a name="avoid-alignment-inconsistencies-between-virtual-blocks-and-physical-disk-sectors-on-dynamic-virtual-hard-disks-or-differencing-disks"></a>Vermeiden von Ausrichtungs Inkonsistenzen zwischen virtuellen und physischen Datenträger Sektoren auf dynamischen virtuellen Festplatten oder differenzierenden Datenträgern

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
*Für mindestens eine virtuelle Festplatte wurden Ausrichtungs Inkonsistenzen erkannt.*  
  
### <a name="impact"></a>Auswirkungen  
*wenn die virtuellen Festplatten auf einem physischen Datenträger mit einer Sektorgröße von 4 KB gespeichert werden, können die virtuellen Computer oder Anwendungen, die die virtuelle Festplatte verwenden, Leistungsprobleme verursachen. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
*verwenden Sie den Assistenten zum Erstellen virtueller Festplatten, um ein neues VHD-Format oder eine virtuelle Festplatte im vhdx-Format zu erstellen, und geben Sie die vorhandene virtuelle Festplatte als Quell Datenträger an. Die neue virtuelle Festplatte wird mit Ausrichtung zwischen den virtuellen Blöcken und dem physischen Datenträger erstellt.*  
  


