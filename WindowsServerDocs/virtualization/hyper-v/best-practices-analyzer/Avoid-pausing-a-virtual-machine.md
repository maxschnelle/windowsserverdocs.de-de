---
title: Vermeiden Sie eine virtuelle Maschine anhalten
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 930f927c-e414-4a36-9786-028941e886e4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4492ac385a289d075ebcd48b1c7c1c78c1af2f8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814351"
---
# <a name="avoid-pausing-a-virtual-machine"></a>Vermeiden Sie eine virtuelle Maschine anhalten

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
  
*Dieser Server weist eine oder mehrere virtuelle Computer im angehaltenen Zustand.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Abhängig von der Menge des verfügbaren Arbeitsspeichers möglicherweise Sie nicht zusätzliche virtuelle Computer ausführen können.*  
  
Angehaltenen virtuellen Maschinen nicht ihre zugeordneten Arbeitsspeicher freigeben, d.h., dass der Speicher ist nicht verfügbar, um andere virtuelle Computer zu starten.  
  
## <a name="resolution"></a>Auflösung  
  
*Wenn dies beabsichtigt ist, ist keine weitere Aktion erforderlich. Andernfalls sollten Sie diese virtuellen Computer fortgesetzt oder beendet werden.*  
  
#### <a name="use-hyper-v-manager-to-resume-the-virtual-machine"></a>Verwenden Sie Hyper-V-Manager, um die virtuelle Maschine fortsetzen  
  
1.  Öffnen Sie den Hyper-V-Manager. (Aus der **Tools** von Server-Manager, klicken Sie anschließend auf **Hyper-V-Manager**.)  
  
2.  Von der **VMs** auflisten, suchen Sie die virtuellen Computer mit dem Status **angehalten**.  
  
    > [!IMPORTANT]  
    > Status der **angehalten-kritisch** tritt auf, wenn es nur sehr wenig freier Speicherplatz auf dem physischen Speicher für den virtuellen Computer. Bevor Sie versuchen, einen virtuellen Computer in diesem Zustand fortsetzen, frei verfügbaren Speicherplatz auf den physischen Speicher ab.  
  
3.  Mit der rechten Maustaste jeder Name des virtuellen Computers, und klicken Sie dann **fortsetzen**. Dadurch wird der virtuelle Computer in einem ausgeführten Zustand zurückgegeben. Wenn Sie den virtuellen Computer herunterfahren möchten, sie erneut einen Rechtsklick, und wählen Sie **Herunterfahren**.  
  
#### <a name="use-windows-powershell-to-resume-the-virtual-machine"></a>Verwenden Sie Windows PowerShell, um die virtuelle Maschine fortsetzen  
  
Sie können dazu in einem Befehl Filtern, und die Pipeline nach dem Abrufen aller virtuellen Maschinen auf dem Host. Typ:  
  
```  
get-vm | where state -eq 'paused' | resume-vm  
```  
  


