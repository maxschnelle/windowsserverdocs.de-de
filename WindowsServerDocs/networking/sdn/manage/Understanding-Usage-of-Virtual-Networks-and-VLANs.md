---
title: Grundlegendes zur Verwendung von virtuellen Netzwerken und VLANs
description: In diesem Thema erfahren Sie mehr über virtuelle Netzwerke für die Hyper-V-Netzwerkvirtualisierung und deren Unterschiede zu virtuellen lokalen Netzwerken (Virtual Local Area Networks, VLANs). Mit der Hyper-V-Netzwerkvirtualisierung erstellen Sie über Lagerungs-VMS, auch als virtuelle Netzwerke bezeichnet.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 84ac2458-3fcf-4c4f-acfe-6105443dd83f
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/26/2018
ms.openlocfilehash: 56e90966d38b8a138dd8781863a4eaad1db639fb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854483"
---
# <a name="understand-the-usage-of-virtual-networks-and-vlans"></a>Grundlegendes zur Verwendung von virtuellen Netzwerken und VLANs

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über virtuelle Netzwerke für die Hyper-V-Netzwerkvirtualisierung und deren Unterschiede zu virtuellen lokalen Netzwerken (Virtual Local Area Networks, VLANs). Mit der Hyper-V-Netzwerkvirtualisierung erstellen Sie über Lagerungs-VMS, auch als virtuelle Netzwerke bezeichnet.



  
Software-Defined Networking (SDN) in Windows Server 2016 basiert auf der Programmier Richtlinie für virtuelle Überlagerungs Netzwerke in einem virtuellen Hyper-V-Switch. Mithilfe der Hyper-V-Netzwerkvirtualisierung können Sie virtuelle Überlagerungs Netzwerke erstellen, die auch als virtuelle Netzwerke bezeichnet werden. 
  
Wenn Sie die Hyper-V-Netzwerkvirtualisierung bereitstellen, werden Überlagerungs Netzwerke erstellt, indem der Layer-2-Ethernet-Frame des ursprünglichen virtuellen Computers mit einem Overlay-oder Tunnel Header (z. b. vxlan oder nvgre) und Layer-3-IP und Layer-2-Ethernet gekapselt wird. Header aus dem zugrunde liegenden (oder physischen) Netzwerk. Die virtuellen über Lagerungs Netzwerke werden durch eine 24-Bit-Virtual Network Kennung (vni) identifiziert, um die Isolation von Mandanten Datenverkehr aufrechtzuerhalten und überlappende IP-Adressen zuzulassen. Die vni besteht aus einer vsid (Virtual Subnetz ID), einer logischen Switch-ID und einer Tunnel-ID.  
  
Außerdem wird jedem Mandanten eine Routing Domäne (ähnlich dem virtuellen Routing und der Weiterleitungs-VRF) zugewiesen, sodass mehrere virtuelle Subnetzpräfixe (die jeweils durch ein vni dargestellt werden) direkt miteinander geroutet werden können. Ein Mandanten übergreifendes Routing (oder Routing übergreifende Domänen) wird nicht unterstützt, ohne dass ein Gateway durchlaufen wird.   
  
Das physische Netzwerk, in dem der gekapselte Datenverkehr jedes Mandanten getunniert wird, wird durch ein logisches Netzwerk dargestellt, das als logisches Netzwerk bezeichnet wird. Dieses logische anbieternetzwerk besteht aus einem oder mehreren Subnetzen, die jeweils durch ein IP-Präfix und optional ein VLAN 802.1 q-Tag dargestellt werden.  
  
Sie können zusätzliche logische Netzwerke und Subnetze zu Infrastruktur Zwecken für den Verwaltungs Datenverkehr, den Speicher Datenverkehr, den Datenverkehr für die Live Migration usw. erstellen.  
  
Die Isolation von Mandanten Netzwerken mithilfe von VLANs wird von Microsoft Sdn nicht unterstützt. Die Mandanten Isolation erfolgt ausschließlich durch die Verwendung von Hyper-V-netzwerkvirtualisierungsüberlagerung virtuelle Netzwerke und Kapselung. 


