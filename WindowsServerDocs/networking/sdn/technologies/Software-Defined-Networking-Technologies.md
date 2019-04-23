---
title: SDN-Technologien
description: Die Themen in diesem Abschnitt enthalten Übersicht und technische Informationen zu den Software Defined Networking-Technologien, die in Windows Server 2016 enthalten sind.
manager: dougkim
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: article
ms.assetid: b491089c-5bcb-49d4-95b1-915b7ce69f88
ms.author: pashort
author: shortpatti
ms.date: 02/14/2019
ms.openlocfilehash: acf3e1dc3e5a229c525ba7cad23819640c0d5261
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891161"
---
# <a name="sdn-technologies"></a>SDN-Technologien

>Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)

Die Themen in diesem Abschnitt enthalten Übersicht und technische Informationen zu den Software Defined Networking-Technologien, die in Windows Server 2016 enthalten sind.  

## <a name="network-controllernetwork-controllernetwork-controllermd"></a>[Netzwerkcontroller](network-controller/Network-Controller.md)

Netzwerkcontroller stellt einen zentralen, programmierbaren Automatisierung zu verwalten, konfigurieren, überwachen und Problembehandlung für beide virtuellen und physischen Netzwerkinfrastruktur in Ihrem Datencenter bereit. Mit dem Netzwerkcontroller können Sie die Konfiguration der Netzwerkinfrastruktur anstatt manuelle Konfiguration von Netzwerkgeräten und Diensten automatisieren. 

Die Netzwerkcontroller ist eine hoch verfügbare und skalierbare Server und bietet zwei Anwendungsprogrammierschnittstellen (APIs):

1. **Southbound-API** – können Sie den Netzwerkcontroller für die Kommunikation mit dem Netzwerk.
2. **Northbound-API** – können Sie für die Kommunikation mit dem Netzwerkcontroller.

Sie können Windows PowerShell, die Representational State Transfer (REST) API oder einer Anwendung zur Verwaltung verwenden, zum Verwalten der folgenden physischen und virtuellen Netzwerkinfrastrukturkomponenten einsetzen:

- Virtuelle Hyper-V-Computer und -Switches 
- Physische Netzwerkswitches 
- Physische Netzwerkrouter 
- Firewallsoftware 
- VPN-Gateways, einschließlich Remote Access Service (RAS) mehrinstanzenfähigen Gateways 
- Komponenten für den Lastenausgleich 
  

  
## <a name="hyper-v-network-virtualizationhyper-v-network-virtualizationhyper-v-network-virtualizationmd"></a>[Hyper-V-Netzwerkvirtualisierung](hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-V-Netzwerkvirtualisierung (HNV) hilft Ihnen, Ihre Anwendungen und arbeitsauslastungen aus dem physischen Netzwerk mithilfe von virtuellen Netzwerken zu abstrahieren. Virtuelle Netzwerke bieten die erforderliche mehrinstanzenfähige Isolation bei Ausführung in einem freigegebenen physischen Netzwerk-Fabric und erhöhen auf diese Weise die Ressourcenverwendung. Um sicherzustellen, dass Sie Ihre vorhandenen Investitionen Rollforward ausführen können, können Sie virtuelle Netzwerke in der vorhandenen netzwerkausrüstung einrichten. Darüber hinaus sind die virtuellen Netzwerke mit virtuelle lokale Netzwerke (VLANs) kompatibel.   
  
  
## <a name="hyper-v-virtual-switchvirtualizationhyper-v-virtual-switchhyper-v-virtual-switchmd"></a>[Hyper-V-Switches](../../../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md) 

Der Hyper-V-Switch ist einen softwarebasierten Schicht-2-Ethernet-Netzwerkswitch, der im Hyper-V-Manager verfügbar ist, nachdem Sie die Hyper-V-Serverrolle installiert haben. Der Switch umfasst programmgesteuert verwaltete und erweiterbare Funktionen zum Verbinden virtueller Computer mit virtuellen Netzwerken und dem physischen Netzwerk. Zudem enthält virtuellen Hyper-V-Switch richtlinienerzwingung für Sicherheits-, Isolations- und Servicelevels.
  
Sie können auch den virtuellen Hyper-V-Switch mit Switch Embedded Teaming (SET) und (Remote Direct Memory Access, RDMA) bereitstellen. Weitere Informationen finden Sie im Abschnitt [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](#bkmk_rdma) in diesem Thema.  

## <a name="internal-dns-service-idns-for-sdnidns-for-sdnmd"></a>[Interne DNS-Dienst (iDNS) für SDN](Idns-for-Sdn.md)

Benötigen DNS in ihren Netzwerken und mit externen Ressourcen im Internet kommunizieren, gehostete virtuelle Computer (VMs) und Anwendungen. Mit iDNS können Sie DNS-Namensauflösungsdienste für isolierte, lokalen-Namespace und Internetressourcen Mandanten bereitstellen. 
  
## <a name="network-function-virtualizationnetwork-function-virtualizationnetwork-function-virtualizationmd"></a>[Netzwerkfunktionsvirtualisierung](network-function-virtualization/Network-Function-Virtualization.md)

Hardwaregeräte, z.B. Load balancer, Firewalls, Router und Switches Produktivitätsgründen zunehmend virtuelle Geräte. Microsoft verfügt über Netzwerke, Switches, Gateways, NATs, Lastenausgleichsmodule und Firewalls virtualisiert. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung. Virtuelle Geräte sind schnell entwickelt und erstellen einen völlig neuen Markt. Generieren von Interesse sind und erhalten Momentum auf beiden Virtualisierungsplattformen und cloud-Dienste weiterhin. 
  
Die folgenden Netzwerkfunktionsvirtualisierung Technologien sind verfügbar.  
  
-   **Softwarelastenausgleich (SLB) und Netzwerkadressübersetzung (NAT)**. Verbessern Sie Durchsatz durch die Unterstützung von Direct Server Return in der das Load Balancing multiplexer die Rückgabe des Netzwerkdatenverkehrs umgangen werden kann. Weitere Informationen finden Sie unter [Softwarelastenausgleich /(SLB/) für SDN](network-function-virtualization/software-load-balancing-for-sdn.md).
  
-   **Datacenter Firewall**. Geben Sie eine präzise Zugriffssteuerungslisten (ACLs), aktivieren Sie auf der VM-Schnittstellenebene Subnetzebene oder der-Firewall-Richtlinien anwenden. Weitere Informationen finden Sie unter [Datacenter Firewall – Übersicht](network-function-virtualization/Datacenter-Firewall-Overview.md).
  
-   **RAS-Gateway für SDN**. Weiterleiten von Netzwerkdatenverkehr zwischen dem physischen Netzwerk und VM-Netzwerkressourcen, unabhängig davon, wo. Sie können den Netzwerkdatenverkehr am am selben physischen Standort oder an vielen unterschiedlichen Standorten weiterleiten. Weitere Informationen finden Sie unter [RAS-Gateway für SDN](network-function-virtualization/RAS-Gateway-for-SDN.md).

  
## <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-sethttpsdocsmicrosoftcomwindows-servervirtualizationhyper-v-virtual-switchrdma-and-switch-embedded-teaming"></a>[Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)  
In Windows Server 2016 können Sie RDMA auf den Netzwerkadaptern aktivieren, die mit einem virtuellen Hyper-V-Switch mit oder ohne Switch Embedded Teaming (SET) gebunden sind. Dadurch können Sie weniger Netzwerkadapter zu verwenden, wenn der gewünschte RDMA- und SET zur gleichen Zeit.  
  
Eine alternative Lösung NIC-Teamvorgang, mit denen Sie in Umgebungen, die Hyper-V und den Stapel Software Defined Networking (SDN) in Windows Server 2016 enthalten ist. SET ist Teil der NIC-Teamvorgang-Funktionen in den virtuellen Hyper-V-Switch integriert.  
  
Satz ermöglicht Ihnen, zwischen einem und acht physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter zu gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.  
SET-Member-Netzwerkadapter müssen alle in dem gleichen physischen Hyper-V-Host in einem Team platziert werden installiert.  
  
Darüber hinaus können Sie Windows PowerShell-Befehle verwenden, aktivieren Data Center Bridging (DCB), erstellen einen virtuellen Hyper-V-Switch mit einem virtuellen RDMA-Netzwerkkarte (vNIC), und erstellen einen virtuellen Hyper-V-Switch mit SET und RDMA-vNICs.  

  

## <a name="border-gateway-protocol-bgpremoteremote-accessbgpborder-gateway-protocol-bgpmd"></a>[Border Gateway Protocol (BGP)](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)
  
Border Gateway Protocol (BGP) ist ein dynamisches Routingprotokoll, das automatisch Routen zwischen Standorten lernt, die Standort-zu-Standort-VPN-Verbindungen verwenden. Aus diesem Grund wird BGP manuelle Konfiguration von Routern reduziert.   Wenn Sie die RAS-Gateway konfigurieren, Sie können BGP Verwalten des Routings von Netzwerkdatenverkehr zwischen VM-Netzwerken Ihrer Mandanten und den Remotestandorten.  
  
## <a name="software-load-balancing-slb-for-sdnnetwork-function-virtualizationsoftware-load-balancing-for-sdnmd"></a>[Softwarelastenausgleich (SLB) für SDN](network-function-virtualization/software-load-balancing-for-sdn.md)
Clouddienstanbieter (CSPs) und Unternehmen, das Bereitstellen von SDN können (Software Load Balancing, SLB) Sie um Mandanten und Kunden mandantennetzwerk-Datenverkehr auf virtuelle Netzwerkressourcen gleichmäßig zu verteilen. Windows Server-SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen. 

## <a name="windows-server-containerscontainerscontainer-networking-overviewmd"></a>[Windows Server-Container](Containers/Container-networking-overview.md)

Windows Server-Container können schlankes Betriebssystem Virtualisierung Trennen der Anwendungen oder Dienste von anderen Diensten auf demselben containerhost ausgeführt wird. Jeder Container verfügt über eine eigene Betriebssystem, Prozesse, Dateisystem, Registrierung und IP-Adressen, die Sie eine Verbindung mit virtuellen Netzwerken herstellen können. 


## <a name="system-center"></a>System Center  
Bereitstellen und verwalten die SDN-Infrastruktur mit [Virtual Machine Management (VMM)](https://docs.microsoft.com/system-center/vmm/) und [Operations Manager](https://docs.microsoft.com/system-center/scom/). Mit VMM bereitstellen und Verwalten von erforderlichen Ressourcen zum Erstellen und Bereitstellen von virtuellen Maschinen und Dienste in privaten Clouds.  Mit Operations Manager überwachen Sie Dienste, Geräte und Vorgänge in Ihrem gesamten Unternehmen Probleme für die sofortige Aktion zu identifizieren. 


---