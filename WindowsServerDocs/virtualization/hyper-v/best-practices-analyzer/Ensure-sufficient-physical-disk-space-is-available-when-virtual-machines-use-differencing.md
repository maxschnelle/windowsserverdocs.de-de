---
title: Stellen Sie sicher, dass genügend physischer Speicherplatz verfügbar ist, wenn virtuelle Computer differenzierende virtuelle Festplatten verwenden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 71f99aab-f994-4022-9da0-d661965b95ac
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 52e09cfb8695389d2c37def2c39ff43b4091fb76
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861953"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-differencing-virtual-hard-disks"></a>Stellen Sie sicher, dass genügend physischer Speicherplatz verfügbar ist, wenn virtuelle Computer differenzierende virtuelle Festplatten verwenden.

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
*Mindestens eine virtuelle Maschine verwendet differenzierende virtuelle Festplatten.*  
  
## <a name="impact"></a>Auswirkungen  
*Bei differenzierenden virtuellen Festplatten ist verfügbarer Speicherplatz auf dem hostingvolume erforderlich, damit Speicherplatz zugewiesen werden kann, wenn Schreibvorgänge auf den virtuellen Festplatten stattfinden. Wenn der verfügbare Speicherplatz erschöpft ist, kann der virtuelle Computer, der auf dem physischen Speicher basiert, beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Überwachen Sie den verfügbaren Speicherplatz, um sicherzustellen, dass ausreichend Speicherplatz für die Erweiterung virtueller Festplatten Sie sollten differenzierende virtuelle Festplatten mit ihrem übergeordneten Element zusammenführen. Überprüfen Sie im Hyper-V-Manager den differenzierenden Datenträger, um die übergeordnete virtuelle Festplatte zu ermitteln. Wenn Sie einen differenzierenden Datenträger mit einem übergeordneten Datenträger zusammenführen, der von anderen differenzierenden Datenträgern gemeinsam verwendet wird, wird durch diese Aktion die Beziehung zwischen den anderen differenzierenden Datenträgern und dem übergeordneten Datenträger beschädigt, sodass Sie unbrauchbar werden. Nachdem Sie überprüft haben, dass die übergeordnete virtuelle Festplatte nicht freigegeben ist, können Sie mit dem Assistenten zum Bearbeiten von Datenträgern den differenzierenden Datenträger mit der übergeordneten virtuellen Festplatte zusammenführen.*  
  


