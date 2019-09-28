---
title: Verhindern, dass ein virtueller Computer angehalten wird
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 930f927c-e414-4a36-9786-028941e886e4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 406b24edd4a7e87e32058006590ac7cd37206568
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366451"
---
# <a name="avoid-pausing-a-virtual-machine"></a>Verhindern, dass ein virtueller Computer angehalten wird

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
  
*Dieser Server verfügt über einen oder mehrere virtuelle Computer im angehaltenen Zustand.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Abhängig von der Menge des verfügbaren Arbeitsspeichers können Sie möglicherweise keine zusätzlichen virtuellen Maschinen ausführen.*  
  
Bei angehaltenen virtuellen Computern wird der zugewiesene Arbeitsspeicher nicht freigegeben, was bedeutet, dass der Arbeitsspeicher zum Starten anderer virtueller Maschinen nicht verfügbar ist  
  
## <a name="resolution"></a>Auflösung  
  
*wenn dies beabsichtigt ist, ist keine weitere Aktion erforderlich. Andernfalls sollten Sie diese virtuellen Computer fortsetzen oder Herunterfahren.*  
  
#### <a name="use-hyper-v-manager-to-resume-the-virtual-machine"></a>Fortsetzen des virtuellen Computers mit dem Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. (Klicken Sie **im Menü Extras** von Server-Manager auf **Hyper-V-Manager**.)  
  
2.  Suchen Sie in der Liste **Virtual Machines** die virtuellen Computer mit dem Status **angeh**alten.  
  
    > [!IMPORTANT]  
    > Der Status " **angehalten-kritisch** " tritt auf, wenn im physischen Speicher für diesen virtuellen Computer nur noch wenig freier Speicherplatz verbleiben. Bevor Sie versuchen, einen virtuellen Computer in diesem Zustand fortzusetzen, geben Sie verfügbaren Speicherplatz im physischen Speicher frei.  
  
3.  Klicken Sie mit der rechten Maustaste auf jeden virtuellen Computer, und klicken Sie **dann auf fort**setzen Dadurch wird die virtuelle Maschine in den Status "wird ausgeführt" zurückversetzt. Wenn Sie anschließend den virtuellen Computer herunterfahren möchten, klicken Sie erneut mit der rechten Maustaste darauf, und wählen Sie **herunter**fahren aus.  
  
#### <a name="use-windows-powershell-to-resume-the-virtual-machine"></a>Verwenden von Windows PowerShell zum Fortsetzen des virtuellen Computers  
  
Sie können dies in einem Befehl mithilfe von Filtern und der Pipeline tun, nachdem Sie alle virtuellen Maschinen auf dem Host erhalten haben. Typ:  
  
```  
get-vm | where state -eq 'paused' | resume-vm  
```  
  


