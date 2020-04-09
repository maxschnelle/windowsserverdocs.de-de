---
title: Vermeiden von Ausrichtungs Inkonsistenzen zwischen virtuellen und physischen Datenträger Sektoren auf dynamischen virtuellen Festplatten oder differenzierenden Datenträgern
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 3f090f015f2179ba372e56d580477ef8d72d977f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857803"
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
*Wenn die virtuellen Festplatten auf einem physischen Datenträger mit einer Sektorgröße von 4 KB gespeichert sind, treten bei der virtuellen Maschine oder Anwendungen, die die virtuelle Festplatte verwenden, möglicherweise Leistungsprobleme auf. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Assistenten zum Erstellen virtueller Festplatten, um eine neue virtuelle Festplatte im VHD-oder vhdx-Format zu erstellen, und geben Sie die vorhandene virtuelle Festplatte als Quell Datenträger an. Die neue virtuelle Festplatte wird mit Ausrichtung zwischen den virtuellen Blöcken und dem physischen Datenträger erstellt.*  
  


