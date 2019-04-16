---
title: Grundlegendes zur Verwendung von virtuellen Netzwerken und VLANs
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
manager: brianlic
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
ms.openlocfilehash: fcf84c5c1f0be2fa1c7524592f8d02e4b11d3a2b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="understanding-usage-of-virtual-networks-and-vlans"></a>Grundlegendes zur Verwendung von virtuellen Netzwerken und VLANs

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zu Hyper-V Network Virtualization virtuelle Netzwerke und wie unterscheiden sich von virtuelle lokale Netzwerke (VLANs).  
  
Software Defined Networking (SDN) in Windows Server2016 basiert auf die Richtlinie für die Überlagerung von virtuellen Netzwerken in einem virtuellen Hyper-V-Switch programmieren. Sie können die Überlagerung virtuelle Netzwerke, auch als virtuelle Netzwerke, mit Hyper-V-Netzwerkvirtualisierung bezeichnet erstellen.   
  
Bei der Bereitstellung von Hyper-V-Netzwerkvirtualisierung werden überlagerungsnetzwerke erstellt, durch die Kapselung von der ursprünglichen Mandanten des virtuellen Computers Schicht-2-Ethernet-Frame mit einem Overlay- oder Tunnel - Headers (z.B. VXLAN oder NVGRE) und Layer-3-IP-Adresse und Layer-2-Ethernet-Header vom dabei (oder physische) Netzwerk. Die Überlagerung virtuellen Netzwerke werden durch ein 24-Bit-virtuellen Netzwerk Bezeichner (VNI7D) mandantenisolation Datenverkehr verwalten und überlappende IP-Adressen identifiziert werden. Die VNI7D besteht aus einem virtuellen Subnetz VSID (ID), logischen Switch-ID und Tunnel-ID.  
  
Darüber hinaus wird jeder Mandant eine Routingdomäne (ähnlich wie virtuelle Routing und Weiterleitung - VRF) zugewiesen, sodass mehrere virtuelle Subnetzpräfixe (jede dargestellt durch einen VNI7D) direkt miteinander weitergeleitet werden können. Cross-Mandanten (oder domänenübergreifendes Routing) Routing wird ohne den Umweg über ein Gateway nicht unterstützt.   
  
Im physische Netzwerk, auf dem jeder Mandant gekapselten Datenverkehr getunnelt wird, wird durch ein logisches Netzwerk bezeichnet das logische Netzwerk von Anbieter dargestellt. Dieser Anbieter logisches Netzwerk besteht aus einem oder mehreren Subnetzen, die durch eine IP-Präfix und optional ein VLAN 802. 1Q dargestellt Tag.  
  
Sie können zusätzliche logische Netzwerke erstellen und Subnetze für Infrastrukturzwecke zum Ausführen von Verwaltungsdatenverkehr, Speicherdatenverkehr, live migrationsdatenverkehr usw.  
  
Microsoft-SDN unterstützt nicht die Isolierung der mandantennetzwerke Verwendung von VLANs. Mandanten erfolgt ausschließlich mithilfe von Hyper-V-Netzwerkvirtualisierung Overlay virtuelle Netzwerke und Kapselung. 


