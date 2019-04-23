---
title: Verstehen Sie die Verwendung von virtuellen Netzwerken und VLANs
description: In diesem Thema enthält Informationen zu virtuellen Netzwerken für Hyper-V Network Virtualization und deren Unterschiede zu virtuelle lokale Netzwerke (VLANs). Mit Hyper-V-Netzwerkvirtualisierung erstellen Sie die Überlagerung virtuellen Netzwerken, die auch als virtuelle Netzwerke bezeichnet.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84ac2458-3fcf-4c4f-acfe-6105443dd83f
ms.author: pashort
author: shortpatti
ms.date: 08/26/2018
ms.openlocfilehash: d126e97a91e4c61ecff00cc2b5a527618b2d4d0f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875531"
---
# <a name="understand-the-usage-of-virtual-networks-and-vlans"></a>Verstehen Sie die Verwendung von virtuellen Netzwerken und VLANs

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema enthält Informationen zu virtuellen Netzwerken für Hyper-V Network Virtualization und deren Unterschiede zu virtuelle lokale Netzwerke (VLANs). Mit Hyper-V-Netzwerkvirtualisierung erstellen Sie die Überlagerung virtuellen Netzwerken, die auch als virtuelle Netzwerke bezeichnet.



  
Software-Defined Networking (SDN) in Windows Server 2016 basiert auf die Richtlinie für die Überlagerung von virtuellen Netzwerken in einem virtuellen Hyper-V-Switch-Programmierung. Sie können die Overlay virtuelle Netzwerke, virtuelle Netzwerke, mit Hyper-V-Netzwerkvirtualisierung so genannte erstellen. 
  
Wenn Sie Hyper-V-Netzwerkvirtualisierung bereitstellen, werden Overlay-Netzwerke erstellt, indem Kapseln der ursprünglichen Mandanten-VM Schicht-2-Ethernet-Frame mit einem Overlay - oder -Tunnel - Headers (z. B. VXLAN oder NVGRE) und Layer-3-IP und Layer-2-Ethernet- Header aus der dabei (oder physisch) Netzwerk. Die Überlagerung virtuellen Netzwerke werden durch ein 24-Bit-virtuelles Netzwerk Bezeichner (VNI) mandantenisolation-Datenverkehr zu verwalten und können überlappende IP-Adressen identifiziert. Die VNI besteht aus einem virtuellen Subnetz VSID (ID), die ID der logischen Switch und Tunnel-ID.  
  
Darüber hinaus ist jeder Mandant eine Routingdomäne (ähnlich wie virtuelle routing und Weiterleitung - VRF) zugewiesen, sodass mehrere virtuelle Subnetz-Präfixe (jede dargestellt durch eine VNI) direkt miteinander weitergeleitet werden können. Mandantenübergreifende (oder die übergreifende Routingdomäne) routing wird ohne Umweg über ein Gateway nicht unterstützt.   
  
Im physische Netzwerk, auf dem jedes Mandanten-gekapselten Datenverkehr getunnelt wird, wird durch ein logisches Netzwerk Namens im Anbieter logischen Netzwerk dargestellt. Dieses logische Netzwerk des Anbieters besteht aus einem oder mehreren Subnetzen, dargestellt durch eine IP-Präfix und optional ein VLAN 802. 1Q Tag.  
  
Sie können zusätzliche logische Netzwerke erstellen und Subnetze für Infrastrukturzwecke zum Ausführen von Verwaltungsdatenverkehr, Speicherdatenverkehr, live Migration-Traffic usw.  
  
Microsoft SDN unterstützt nicht die Isolation von mandantennetzwerke mit VLANs. Mandantenisolation erfolgt ausschließlich mithilfe von Hyper-V-Netzwerkvirtualisierung Overlay virtuelle Netzwerke und Kapselung. 


