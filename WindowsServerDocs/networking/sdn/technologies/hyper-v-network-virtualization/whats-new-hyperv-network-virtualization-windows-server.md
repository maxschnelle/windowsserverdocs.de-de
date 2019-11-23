---
title: Neuerungen bei der Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016
description: Dieses Thema enthält Informationen zu neuen Features bei der Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0254275a-0a77-40a9-b68a-1029284c03fe
ms.author: pashort
author: shortpatti
ms.date: 03/19/2018
ms.openlocfilehash: 57db82fdd8c7524afb427c61f754e9b8ede8e7b7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355665"
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>Neuerungen bei der Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema werden die Funktionen der Hyper-v-Netzwerkvirtualisierung (HNV) beschrieben, die in Windows Server 2016 neu oder geändert wurden.  
  
## <a name="BKMK_IPAM2012R2"></a>Updates in HNV  
HNV bietet eine verbesserte Unterstützung in den folgenden Bereichen:  
  
|Feature/Funktionalität|Neu oder verbessert|Beschreibung|  
|--------------------------|-------------------|---------------|  
|[Programmierbarer Hyper-V-Switch](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|Neu|Die HNV-Richtlinie kann über den Microsoft-Netzwerk Controller programmiert werden.|  
|[Unterstützung der vxlan-Kapselung](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|Neu|HNV unterstützt jetzt die vxlan-Kapselung.|  
|[Interoperabilität von Software Load Balancer (SLB)](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|Neu|HNV ist vollständig in die Microsoft-Software Load Balancer integriert.|  
|[Kompatible IEEE-Ethernet-Header](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|Verbessert|Kompatibel mit IEEE Ethernet-Standards|  
  
### <a name="SDN"></a>Programmierbarer Hyper-V-Switch  
HNV ist ein grundlegender Baustein der aktualisierten Software Defined Networking-Lösung (SDN) von Microsoft und ist vollständig in den Sdn-Stapel integriert.  
  
Der neue Netzwerk Controller von Microsoft überträgt die HNV-Richtlinien mithilfe von Open Vswitch Database Management Protocol (ovsdb) als Southbound Interface (SBI) auf einen Host-Agent, der auf jedem Host ausgeführt wird. Der Host-Agent speichert diese Richtlinie mithilfe einer Anpassung des [vtep-Schemas](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema) und Programm komplexe Fluss Regeln in eine leistungsstarke Fluss-Engine im Hyper-V-Switch.  
  
Die Flow-Engine innerhalb des Hyper-V-Switches ist das gleiche Modul, das in Microsoft Azure&trade;verwendet wird, das sich in der Microsoft Azure Public Cloud als hyperskaliert erwiesen hat. Darüber hinaus ist der gesamte Sdn-Stapel über den Netzwerk Controller und der Netzwerkressourcen Anbieter (Details in Kürze verfügbar) mit Microsoft Azure konsistent, sodass die Leistungsfähigkeit der Microsoft Azure Public Cloud an den Unternehmens-und Hostingdienst gebracht wird. Anbieter Kunden.  
  
> [!NOTE]  
> Weitere Informationen zu ovsdb finden Sie unter [RFC 7047](https://www.rfc-editor.org/info/rfc7047).  
  
Der Hyper-V-Switch unterstützt sowohl Zustands lose als auch Zustands behaftete Fluss Regeln basierend auf der einfachen "Match Action"-Anweisung in der Datenfluss-Engine  
 
![Windows Server 2016 Hyper-V-Switch](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)  
  
### <a name="VXLAN"></a>Unterstützung der vxlan-Kapselung  
Das virtuelle erweiterbare LAN (Local Area Network, vxlan- [RFC 7348](https://www.rfc-editor.org/info/rfc7348)) wurde auf dem Marktplatz weitgehend übernommen und bietet Unterstützung von Anbietern wie Cisco, Brocade, Dell, HP und anderen. HNV unterstützt jetzt auch dieses Kapselungs Schema mit dem Mac-Verteilungsmodus über den Microsoft-Netzwerk Controller zum Programmieren von Zuordnungen für Netzwerk-IP-Adressen von Mandanten überlagern (Kundenadresse oder Zertifizierungsstelle) zu den physischen Netzwerk-IP-Adressen (Anbieter Adresse oder PA). Sowohl nvgre-als auch vxlan-Aufgaben Offloads werden für eine verbesserte Leistung durch Treiber von Drittanbietern unterstützt.  
  
### <a name="SLB"></a>Interoperabilität von Software Load Balancer (SLB)  
Windows Server 2016 umfasst einen Software Lastenausgleich (Software Load Balancer, SLB) mit vollständiger Unterstützung für den Datenverkehr des virtuellen Netzwerks und eine nahtlose Interaktion mit HN Der SLB wird durch die leistungsfähige Fluss-Engine auf der Datenebene v-Switch implementiert und vom Netzwerk Controller für virtuelle IP-Zuordnungen (VIP)/dynamische IP (DIP) gesteuert.  
  
### <a name="L2"></a>Kompatible IEEE-Ethernet-Header  
HNV implementiert korrekte L2-Ethernet-Header, um die Interoperabilität mit virtuellen und physischen Geräten von Drittanbietern zu gewährleisten, die von branchenüblichen Protokollen abhängen. Microsoft stellt sicher, dass alle übertragenen Pakete über kompatible Werte in allen Feldern verfügen, um diese Interoperabilität zu gewährleisten. Darüber hinaus muss die Unterstützung für groß Rahmen (MTU > 1780) im physischen L2-Netzwerk den Paket Overhead berücksichtigen, der durch Kapselungs Protokolle (nvgre, vxlan) eingeführt wurde, und gleichzeitig sicherstellen, dass der Gast Virtual Machines an einen HNV angeschlossen ist Virtual Network 1514 MTU.  
  
## <a name="see-also"></a>Weitere Informationen  
  
-   [Hyper-V-Netzwerkvirtualisierung – Übersicht](hyperv-network-virtualization-overview-windows-server.md)  
  
-   [Hyper-V-Netzwerkvirtualisierung – Technische Details](hyperv-network-virtualization-technical-details-windows-server.md)  
  
-   [Software-Defined Networking](../../Software-Defined-Networking--SDN-.md)  
  