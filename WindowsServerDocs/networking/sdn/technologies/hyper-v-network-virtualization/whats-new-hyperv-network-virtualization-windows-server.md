---
title: Neuerungen in Hyper-V-Netzwerkvirtualisierung unter WindowsServer 2016
description: Dieses Thema enthält Informationen zu neuen Funktionen in Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0254275a-0a77-40a9-b68a-1029284c03fe
ms.author: pashort
author: shortpatti
ms.date: 03/19/2018
ms.openlocfilehash: 24ec9e52be3acdfced35eae4fb5f98f16d8e18f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837951"
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>Neuerungen in Hyper-V-Netzwerkvirtualisierung unter WindowsServer 2016

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird beschrieben, die Hyper-V-Netzwerkvirtualisierung (HNV) Funktionen, die neue oder geänderte in Windows Server 2016.  
  
## <a name="BKMK_IPAM2012R2"></a>Updates im HNV  
HNV bietet verbesserte Unterstützung in den folgenden Bereichen:  
  
|Feature/Funktionalität|Neu oder verbessert|Beschreibung|  
|--------------------------|-------------------|---------------|  
|[Programmierbare Hyper-V-switch](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|Neu|Hnv-Richtlinie ist über den Microsoft-Netzwerkcontroller programmierbar.|  
|[Unterstützung für VXLAN-Kapselung](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|Neu|HNV unterstützt jetzt VXLAN Kapselung.|  
|[Interoperabilität von Software Load Balancer (SLB)](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|Neu|HNV ist vollständig mit dem Microsoft-Software-Load Balancer integriert.|  
|[Kompatible IEEE-Ethernet-headers](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|Verbessert|Mit IEEE-Ethernet-Standards konform|  
  
### <a name="SDN"></a>Programmierbare Hyper-V-switch  
HNV ist ein wesentlicher Baustein der Lösung von Microsoft aktualisierte Software Defined Networking (SDN), und ist vollständig in den SDN-Stapel integriert.  
  
Neue Microsoft-Netzwerkcontroller überträgt-Richtlinien auf einem Host-Agent auf jedem Host mithilfe von Open-vSwitch-Datenbank-Management-Protokoll (OVSDB) als die SouthBound Schnittstelle (SBI) ausgeführt wird. Der Host-Agent speichert diese Richtlinie, die über eine Anpassung der [VTEP Schema](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema) und Programme von komplexen Flussregeln in eine leistungsstarke-Datenfluss-Engine in der Hyper-V-Switch.  
  
Die Datenfluss-Engine innerhalb der Hyper-V-Switch wird die gleiche Engine in Microsoft Azure verwendet&trade;, die im großen Maßstab in der öffentlichen Cloud von Microsoft Azure bewährt hat. Darüber hinaus ist die gesamte SDN-Stapel nach oben durch den Netzwerkcontroller und Anbieter von Netzwerkressourcen (Details, die in Kürze verfügbar) konsistent mit Microsoft Azure und daher bringt die Leistungsfähigkeit von der öffentlichen Cloud von Microsoft Azure für unser Unternehmen und hosting-Dienst Provider-Kunden.  
  
> [!NOTE]  
> Weitere Informationen zu OVSDB, finden Sie unter [RFC 7047](https://www.rfc-editor.org/info/rfc7047).  
  
Hyper-V-Switch unterstützt beide zustandslosen und zustandsbehafteten Flussregeln basierend auf einfachen "entsprechen der Aktion" innerhalb von Microsoft Flow-Engine.  
 
![Windows Server 2016 Hyper-V-switch](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)  
  
### <a name="VXLAN"></a>Unterstützung für VXLAN-Kapselung  
Die Virtual eXtensible Local Area Network (VXLAN - [RFC 7348](https://www.rfc-editor.org/info/rfc7348)) Protokoll auf dem Markt, mit Unterstützung von Herstellern wie Cisco, Brocade, Dell, HP und andere häufig übernommen wurde. HNV unterstützt jetzt auch dieses Kapselung-Schema mithilfe der MAC-Verteilungsmodus über den Microsoft-Netzwerkcontroller Programm Zuordnungen Mandanten Overlay-Netzwerk IP-Adressen (Customer Address, Kundenadresse oder CA) für die physischen dabei Netzwerk IP-Adressen (Anbieter Adresse oder PA). Sowohl NVGRE als auch VXLAN Aufgabe verlagert werden zur Verbesserung der Leistung durch Drittanbieter-Treiber unterstützt.  
  
### <a name="SLB"></a>Interoperabilität von Software Load Balancer (SLB)  
Windows Server 2016 bietet vollständige Unterstützung für virtuellen Netzwerkdatenverkehr und die nahtlose Interaktion mit HNV ein Software Load Balancer (SLB). Der SLB ist über die leistungsfähigen-Datenfluss-Engine in den Daten-Ebene-V-Switch implementiert und vom Netzwerkcontroller gesteuert wird, für die virtuelle IP-Adresse (VIP) / dynamische IP (DIP)-Zuordnungen.  
  
### <a name="L2"></a>Kompatible IEEE-Ethernet-headers  
HNV implementiert die richtige L2-Ethernet-Header, um die Interoperabilität mit virtuellen und physischen Geräten von Drittanbietern zu gewährleisten, die von branchenüblichen Protokollen abhängen. Microsoft wird sichergestellt, dass alle gesendeten Pakete kompatible Werte in allen Feldern, um diese Interoperabilität zu gewährleisten. Darüber hinaus unterstützen für Jumbo Frames (MTU 1780 >) im physischen Netzwerk L2-erforderlich, um das Konto für das Paket eingeführt Mehraufwand durch Kapselung-Protokolle (NVGRE, VXLAN) und gleichzeitig sicherstellen virtueller Computer mit einem virtuellen Netzwerk von hnv verwalten-Gast eine 1514 MTU.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Hyper-V-Netzwerkvirtualisierung – Übersicht](hyperv-network-virtualization-overview-windows-server.md)  
  
-   [Hyper-V-Netzwerkvirtualisierung – Technische Details](hyperv-network-virtualization-technical-details-windows-server.md)  
  
-   [Software-Defined Networking](../../Software-Defined-Networking--SDN-.md)  
  