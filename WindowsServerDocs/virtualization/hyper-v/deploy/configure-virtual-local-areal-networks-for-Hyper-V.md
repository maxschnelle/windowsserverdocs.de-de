---
title: Konfigurieren Sie virtuelle lokale Netzwerke für Hyper-V
description: Erhalten Anweisungen zum Konfigurieren einer virtuellen LAN (VLAN) für die Verwendung durch virtuelle Maschinen auf Hyper-V-Host.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8510a709-001c-4eee-b6d6-c451e8a8a836
author: KBDAzure
ms.author: kathydav
ms.date: 10/11/2016
ms.openlocfilehash: 5b5eaf175e7c09124aaa3f7a33523e8b87a9ae84
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848461"
---
# <a name="configure-virtual-local-area-networks-for-hyper-v"></a>Konfigurieren Sie virtuelle lokale Netzwerke für Hyper-V
Virtuelle lokale Netzwerke \(VLANs\) bieten eine Möglichkeit, um die Netzwerkdatenverkehr zu isolieren. VLANs sind so konfiguriert, in die Switches und Router, die 802. 1Q zu unterstützen. Wenn Sie mehrere VLANs konfigurieren und Kommunikation zwischen ihnen stattfindet, müssen Sie so konfigurieren, mit denen das Netzwerkgeräte. 

Sie benötigen Folgendes zum Konfigurieren von VLANs:  
  
-   Einen physischen Netzwerkadapter und Treiber, unterstützt der 802. 1Q, VLAN-Kennzeichnung.  
-   Einem physischen Netzwerkswitch, der unterstützt 802. 1Q VLAN-Kennzeichnung.  
  
Konfigurieren Sie den virtuellen Switch zum Zulassen von Netzwerkdatenverkehr am physischen Switchport auf dem Host. Dies ist für die VLAN-IDs, die Sie intern mit virtuellen Computern verwenden möchten. Als Nächstes konfigurieren Sie den virtuellen Computer, die das VLAN angeben, die dem virtuellen Computer für die gesamte Netzwerkkommunikation verwendet.  
  
#### <a name="to-allow-a-virtual-switch-to-use-a-vlan"></a>Um einen virtuellen Switch mit einem VLAN zu ermöglichen.  
  
1.  Öffnen Sie Hyper\-V-Manager.  
  
2.  Klicken Sie im Menü Aktionen auf **Manager für virtuelle Switches**.  
  
3.  Klicken Sie unter **virtuelle Switches**, wählen Sie ein virtueller Switch verbunden, um einen physischen Netzwerkadapter, die VLANs unterstützt. 

4. Wählen Sie im rechten Bereich unter der VLAN-ID, **Erkennung virtueller LANS aktivieren** und geben Sie eine Zahl für die VLAN-ID.  
  
    Gesamten Datenverkehr, der geht über den physischen Netzwerkadapter mit dem virtuellen Switch verbunden werden mit der VLAN-ID gekennzeichnet werden, die Sie festlegen.  
  
#### <a name="to-allow-a-virtual-machine-to-use-a-vlan"></a>Um einen virtuellen Computer mit einem VLAN zu ermöglichen.  
  
1.  Öffnen Sie Hyper\-V-Manager.  
  
2.  Klicken Sie im Ergebnisbereich unter **VMs**, wählen Sie den betreffenden virtuellen Computer aus, und klicken Sie dann mit der rechten Maustaste **Einstellungen**.  

3.  Klicken Sie unter **Hardware**, wählen Sie einen virtuellen Switch, der mit einem VLAN aktiviert ist.
  
4.  Wählen Sie im rechten Bereich **Erkennung virtueller LANS aktivieren**, und geben Sie dann die gleiche VLAN-ID, wie Sie für den virtuellen Switch angegeben. 

Wenn die virtuelle Maschine mehrere VLANs zu verwenden muss, führen Sie eine der folgenden:  
  
-   Verbinden Sie mehrere virtuelle Netzwerkadapter, um geeignete virtuelle Switches und Zuweisen von VLAN-IDs. Stellen Sie sicher, dass die IP-Adressen ordnungsgemäß konfiguriert und verwendet die richtige IP-Adresse der Datenverkehr auch über das VLAN weitergeleitet werden sollen.  
  
-   Konfigurieren Sie den virtuellen Netzwerkadapter für Word im "Trunk" mit der [festgelegt\-VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848475.aspx) Cmdlet.
  
## <a name="see-also"></a>Siehe auch  
 
[Hyper\-V-Switches](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/hyper-v-virtual-switch)