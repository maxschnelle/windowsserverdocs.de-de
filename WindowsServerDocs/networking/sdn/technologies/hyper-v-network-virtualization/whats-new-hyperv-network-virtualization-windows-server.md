---
title: Neues in Hyper-V-Netzwerkvirtualisierung in Windows Server 2016
description: Dieses Thema enthält Informationen zu neuen Features in Hyper-V-Netzwerkvirtualisierung in Windows Server2016
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
ms.openlocfilehash: 0954768944e44848debfbb7fb752a13ca47031c2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>Neues in Hyper-V-Netzwerkvirtualisierung in Windows Server 2016

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema werden die Hyper-V-Netzwerkvirtualisierung (HNV)-Funktionen, die neuen oder geänderten in Windows Server2016 beschrieben.  
  
## <a name="BKMK_IPAM2012R2"></a>In Hyper-v-Updates  
Hyper-v-bietet verbesserte Unterstützung in den folgenden Bereichen:  
  
|Die Funktionalität|Neue oder verbesserte|Beschreibung|  
|--------------------------|-------------------|---------------|  
|[Programmierbaren Hyper-V-Switch](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|Neu|Hnv-Richtlinie wird über die Microsoft-Netzwerkcontroller programmierbaren.|  
|[VXLAN Kapselung Support](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|Neu|Hyper-v-unterstützt jetzt VXLAN Kapselung.|  
|[Interoperabilität von Software Load Balancer (SLB)](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|Neu|Hyper-v-ist vollständig mit einem Microsoft-Software-Lastenausgleich integriert.|  
|[Kompatible IEEE-Ethernet-Header](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|Verbesserte|Kompatibel mit IEEE-Ethernet-Standards|  
  
### <a name="SDN"></a>Programmierbaren Hyper-V-Switch  
Hyper-v-ist ein grundlegender Baustein der aktualisierten Software Defined Networking (SDN)-Lösung von Microsoft und vollständig in den SDN-Stapels integriert ist.  
  
Neue Microsoft Netzwerk-Controller wird Hyper-v-Richtlinien auf einen Host-Agent auf jedem Host mit öffnen vSwitch Datenbank-Management-Protokoll (OVSDB) als die SouthBound Schnittstelle (SBI) ausgeführt wird. Der Server-Agent speichert diese Richtlinie, die eine Anpassung mithilfe der [VTEP Schema](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema) und Programme komplexer fortlaufender Regeln in eine leistungsfähige Fluss Engine in Hyper-V-Switch.  
  
Der Fluss Motor Hyper-V-Switch Engine ist auch in Microsoft Azure verwendet&trade;, die auf hyper-Skalierung in der öffentlichen Microsoft Azure-Cloud bewährt hat. Darüber hinaus ist die gesamte SDN-Stapels Sie über die Netzwerkcontroller und dem Netzwerkressourcenanbieter (Detail in Kürze verfügbar) einheitlich mit Microsoft Azure, daher dabei, die Leistungsstärke von der öffentlichen Microsoft Azure-Cloud für Unternehmen und Hosting-Anbieter-Kunden.  
  
> [!NOTE]  
> Weitere Informationen zu OVSDB, finden Sie unter [RFC 7047](http://www.rfc-editor.org/info/rfc7047).  
  
Hyper-V-Switch unterstützt beide Zustandslose und zustandsbehaftete Flussregeln auf Grundlage der einfache 'entsprechen Aktion"in Microsoft Flow-Modul.  
 
![Windows Server2016 Hyper-V-Switch](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)  
  
### <a name="VXLAN"></a>VXLAN Kapselung Support  
Die Virtual eXtensible Local Area Network (VXLAN - [RFC 7348](http://www.rfc-editor.org/info/rfc7348)) Protokoll wurde umfassend im Markt, mit Unterstützung von Herstellern wie Cisco, Brocade, Dell, HP und andere übernommen. Hyper-v-unterstützt jetzt auch dieses Kapselung Schema Modus MAC Verteilung über den Microsoft Netzwerkcontroller Programm Zuordnungen für Mandanten Overlay Netzwerk IP-Adressen (Kundenadresse oder CA) in der physischen dabei Netzwerk-IP-Adressen (Anbieteradresse oder PA). Sowohl NVGRE als auch VXLAN Aufgabe verlagert werden zur Verbesserung der Leistung durch Drittanbieter-Treiber unterstützt.  
  
### <a name="SLB"></a>Interoperabilität von Software Load Balancer (SLB)  
Windows Server2016 enthält ein softwarelastenausgleich (SLB) vollständige Unterstützung für virtuellen Netzwerkdatenverkehr und die nahtlose Interaktion mit Hyper-v. Die SLB ist über das leistungsfähige Fluss-Modul in den Daten Ebene V-Switch implementiert und vom Netzwerkcontroller gesteuert werden, für die virtuelle IP-Adresse (VIP) / dynamische Zuordnung IP (DIP).  
  
### <a name="L2"></a>Kompatible IEEE-Ethernet-Header  
Hyper-v-implementiert die richtige L2-Ethernet-Header, um Interoperabilität mit virtuellen und physischen Einheiten von Drittanbietern zu gewährleisten, die Standardprotokolle abhängig sind. Microsoft wird sichergestellt, dass alle gesendeten Pakete kompatible Werte in alle Felder, um sicherzustellen, dass diese Interoperabilität. Darüber hinaus Unterstützung für Großrahmen (MTU > 1780) im physischen Netzwerk L2-Paket Aufwand von Protokollen der Encapsulation (NVGRE, VXLAN) eingeführt, bei gleichzeitiger Gewährleistung Gastbetriebssystem mit einem virtuellen Hyper-v-Netzwerk verbundenen virtuellen Maschinen zu berücksichtigen müssen verwalten eine 1514 MTU.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Hyper-V-Netzwerkvirtualisierung – Übersicht](hyperv-network-virtualization-overview-windows-server.md)  
  
-   [Hyper-V-Netzwerkvirtualisierung – technische Detail](hyperv-network-virtualization-technical-details-windows-server.md)  
  
-   [Software-Defined Networking](../../Software-Defined-Networking--SDN-.md)  
  