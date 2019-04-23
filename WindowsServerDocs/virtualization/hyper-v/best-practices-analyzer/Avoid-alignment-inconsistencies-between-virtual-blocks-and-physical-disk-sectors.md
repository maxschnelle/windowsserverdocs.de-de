---
title: Vermeiden Sie die Ausrichtung auf Inkonsistenzen virtuellen Blöcke und physischen Datenträgersektoren auf dynamische virtuelle Festplatten oder differenzierende Datenträger
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4973c199a5507d00e15da8f621a09f0c602a29fa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833861"
---
# <a name="avoid-alignment-inconsistencies-between-virtual-blocks-and-physical-disk-sectors-on-dynamic-virtual-hard-disks-or-differencing-disks"></a>Vermeiden Sie die Ausrichtung auf Inkonsistenzen virtuellen Blöcke und physischen Datenträgersektoren auf dynamische virtuelle Festplatten oder differenzierende Datenträger

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
*Ausrichtung Inkonsistenzen wurden für eine oder mehrere virtuelle Festplatten erkannt.*  
  
### <a name="impact"></a>Auswirkungen  
*Wenn auf die virtuellen Festplatten gespeichert werden können möglicherweise die physischer Datenträger mit einer Sektorgröße von 4 K, den virtuellen Computer oder Anwendungen, die die virtuelle Festplatte verwenden Leistungsprobleme auftreten. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Assistenten zum Erstellen einer virtuellen Festplatte, erstellen eine neue VHD-Format oder im VHDX-Format virtuelle Festplatte aus, und geben die vorhandene virtuelle Festplatte als des Quelldatenträgers. Die neue virtuelle Festplatte wird mit der Ausrichtung zwischen den virtuellen Blöcke und die physischen Datenträger erstellt werden.*  
  


