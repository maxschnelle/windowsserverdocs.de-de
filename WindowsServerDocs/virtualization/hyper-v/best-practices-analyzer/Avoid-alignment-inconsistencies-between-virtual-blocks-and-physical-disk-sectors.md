---
title: Vermeiden von Ausrichtungs Inkonsistenzen zwischen virtuellen und physischen Datenträger Sektoren auf dynamischen virtuellen Festplatten oder differenzierenden Datenträgern
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
ms.date: 8/16/2016
ms.openlocfilehash: aa165dad38ae455f7c4a5a0d73cdd005c01a60ef
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747095"
---
# <a name="avoid-alignment-inconsistencies-between-virtual-blocks-and-physical-disk-sectors-on-dynamic-virtual-hard-disks-or-differencing-disks"></a>Vermeiden von Ausrichtungs Inkonsistenzen zwischen virtuellen und physischen Datenträger Sektoren auf dynamischen virtuellen Festplatten oder differenzierenden Datenträgern

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Für mindestens eine virtuelle Festplatte wurden Ausrichtungs Inkonsistenzen erkannt.*

### <a name="impact"></a>Auswirkung
*Wenn die virtuellen Festplatten auf einem physischen Datenträger mit einer Sektorgröße von 4 KB gespeichert sind, treten bei der virtuellen Maschine oder Anwendungen, die die virtuelle Festplatte verwenden, möglicherweise Leistungsprobleme auf. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Verwenden Sie den Assistenten zum Erstellen virtueller Festplatten, um eine neue virtuelle Festplatte im VHD-oder vhdx-Format zu erstellen, und geben Sie die vorhandene virtuelle Festplatte als Quell Datenträger an. Die neue virtuelle Festplatte wird mit Ausrichtung zwischen den virtuellen Blöcken und dem physischen Datenträger erstellt.*



