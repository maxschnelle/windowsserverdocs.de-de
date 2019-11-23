---
title: Konfigurieren von virtuellen lokalen Netzwerken für Hyper-V
description: Enthält Anweisungen zum Konfigurieren eines virtuellen lokalen Netzwerks (VLAN) für die Verwendung durch virtuelle Maschinen auf einem Hyper-V-Host.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8510a709-001c-4eee-b6d6-c451e8a8a836
author: KBDAzure
ms.author: kathydav
ms.date: 10/11/2016
ms.openlocfilehash: f2c240a3ad9f9783e509efb288cc6c6410339685
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364277"
---
# <a name="configure-virtual-local-area-networks-for-hyper-v"></a>Konfigurieren von virtuellen lokalen Netzwerken für Hyper-V
Virtuelle lokale Netzwerke \(VLANs\) eine Möglichkeit bieten, den Netzwerk Datenverkehr zu isolieren. VLANs werden in Switches und Routern konfiguriert, die 802.1 q unterstützen. Wenn Sie mehrere VLANs konfigurieren und die Kommunikation zwischen Ihnen stattfinden soll, müssen Sie die Netzwerkgeräte so konfigurieren, dass Sie dies zulassen. 

Zum Konfigurieren von VLANs benötigen Sie Folgendes:  
  
-   Ein physischer Netzwerkadapter und-Treiber, der 802.1 q-VLAN-Kennzeichnung unterstützt.  
-   Ein physischer Netzwerk Switch, der 802.1 q-VLAN-Tagging unterstützt.  
  
Auf dem Host konfigurieren Sie den virtuellen Switch so, dass Netzwerk Datenverkehr auf dem physischen Switchport zugelassen wird. Dies gilt für die VLAN-IDs, die Sie intern mit virtuellen Computern verwenden möchten. Als Nächstes konfigurieren Sie den virtuellen Computer, um das VLAN anzugeben, das von der virtuellen Maschine für die gesamte Netzwerkkommunikation verwendet wird.  
  
#### <a name="to-allow-a-virtual-switch-to-use-a-vlan"></a>So ermöglichen Sie einem virtuellen Switch die Verwendung eines VLANs  
  
1.  Öffnen Sie den Hyper\-V-Manager.  
  
2.  Klicken Sie im Menü Aktionen auf **Manager für virtuelle**Switches.  
  
3.  Wählen Sie unter **virtuelle Switches**einen virtuellen Switch aus, der mit einem physischen Netzwerkadapter verbunden ist, der VLANs unterstützt. 

4. Wählen Sie im rechten Bereich unter VLAN-ID die Option **virtuelle LAN-Identifikation aktivieren** aus, und geben Sie dann eine Nummer für die VLAN-ID ein.  
  
    Der gesamte Datenverkehr über den physischen Netzwerkadapter, der mit dem virtuellen Switch verbunden ist, wird mit der von Ihnen festgelegten VLAN-ID gekennzeichnet.  
  
#### <a name="to-allow-a-virtual-machine-to-use-a-vlan"></a>So lassen Sie zu, dass ein virtueller Computer ein VLAN verwendet  
  
1.  Öffnen Sie den Hyper\-V-Manager.  
  
2.  Wählen Sie im Ergebnisbereich unter **Virtual Machines**den entsprechenden virtuellen Computer aus, und klicken Sie dann mit der rechten Maustaste auf **Einstellungen**.  

3.  Wählen Sie unter **Hardware**einen virtuellen Switch aus, der mit einem VLAN eingerichtet ist.
  
4.  Wählen Sie im rechten Bereich die Option **virtuelle LAN-Identifikation aktivieren**aus, und geben Sie dann dieselbe VLAN-ID ein, die Sie für den virtuellen Switch angegeben haben. 

Wenn die virtuelle Maschine weitere VLANs verwenden muss, führen Sie einen der folgenden Schritte aus:  
  
-   Verbinden Sie weitere virtuelle Netzwerkadapter mit den entsprechenden virtuellen Switches, und weisen Sie die VLAN-IDs zu. Stellen Sie sicher, dass die IP-Adressen ordnungsgemäß konfiguriert sind und dass der Datenverkehr, den Sie über das VLAN weiterleiten möchten, auch die richtige IP-Adresse verwendet  
  
-   Konfigurieren Sie den Wort Adapter des virtuellen Netzwerks im trunk Modus mithilfe der [Set\-vmnetworkadaptervlan](https://technet.microsoft.com/library/hh848475.aspx) -cmdlt.
  
## <a name="see-also"></a>Weitere Informationen  
 
[Virtueller Hyper\-V-Switch](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/hyper-v-virtual-switch)