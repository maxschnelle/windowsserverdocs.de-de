---
title: SDN-Technologien
description: Die Themen in diesem Abschnitt bieten eine Übersicht und technische Informationen zu den Software-Defined Networking-Technologien, die in Windows Server 2016 enthalten sind.
manager: dougkim
ms.prod: windows-server
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: article
ms.assetid: b491089c-5bcb-49d4-95b1-915b7ce69f88
ms.author: lizross
author: eross-msft
ms.date: 02/14/2019
ms.openlocfilehash: f6a33d59cedecc49b50d01ebffb0fef9fe460afd
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317215"
---
# <a name="sdn-technologies"></a>SDN-Technologien

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

Die Themen in diesem Abschnitt bieten eine Übersicht und technische Informationen zu den Software-Defined Networking-Technologien, die in Windows Server 2016 enthalten sind.  

## <a name="network-controller"></a>[Netzwerkcontroller](network-controller/Network-Controller.md)

Der Netzwerk Controller bietet einen zentralisierten, programmierbaren Automatisierungs Punkt für die Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Daten Center. Mit dem Netzwerk Controller können Sie die Konfiguration der Netzwerkinfrastruktur automatisieren, anstatt die manuelle Konfiguration von Netzwerkgeräten und-Diensten durchzuführen. 

Der Netzwerk Controller ist ein hochverfügbarer und skalierbarer Server und bietet zwei APIs für die Anwendungsprogrammierung:

1. **Southbound-API** – ermöglicht dem Netzwerk Controller die Kommunikation mit dem Netzwerk.
2. **Northbound-API** – ermöglicht die Kommunikation mit dem Netzwerk Controller.

Zum Verwalten der folgenden physischen und virtuellen Netzwerkinfrastruktur können Sie Windows PowerShell, die Rest-API (Representational State Transfer) oder eine Verwaltungs Anwendung verwenden:

- Virtuelle Hyper-V-Computer und -Switches 
- Physische Netzwerkswitches 
- Physische Netzwerkrouter 
- Firewallsoftware 
- VPN-Gateways, einschließlich RAS-Gateways (Remote Access Service) 
- Lastenausgleich 
  
## <a name="hyper-v-network-virtualization"></a>[Hyper-V-Netzwerkvirtualisierung](hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-v-Netzwerkvirtualisierung (HNV) unterstützt Sie bei der Abstraktion Ihrer Anwendungen und Workloads aus dem physischen Netzwerk mithilfe von virtuellen Netzwerken. Virtuelle Netzwerke bieten die erforderliche mehrinstanzenfähige Isolation bei Ausführung in einem freigegebenen physischen Netzwerk-Fabric und erhöhen auf diese Weise die Ressourcenverwendung. Um sicherzustellen, dass Sie Ihre vorhandenen Investitionen weiter nutzen können, können Sie virtuelle Netzwerke auf vorhandenem Netzwerkgerät einrichten. Außerdem sind virtuelle Netzwerke mit virtuellen lokalen Netzwerken (Virtual Local Area Networks, VLANs) kompatibel.
  
## <a name="hyper-v-virtual-switch"></a>[Virtueller Hyper-V-Switch](../../../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md) 

Bei dem virtuellen Hyper-v-Switch handelt es sich um einen softwarebasierten Schicht-2-Ethernet-Netzwerk Switch, der im Hyper-v-Manager nach der Installation der Hyper-v-Server Rolle verfügbar ist. Der Switch umfasst programmgesteuert verwaltete und erweiterbare Funktionen zum Verbinden virtueller Computer mit virtuellen Netzwerken und dem physischen Netzwerk. Außerdem ermöglicht der virtuelle Hyper-V-Switch die Durchsetzung von Richtlinien für Sicherheit, Isolation und Service Levels.
  
Sie können auch den virtuellen Hyper-V-Switch mit Switch Embedded Teaming (Set) und Remote Direct Memory Access (RDMA) bereitstellen. Weitere Informationen finden Sie im Abschnitt [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](#remote-direct-memory-access-rdma-and-switch-embedded-teaming-set) in diesem Thema.

## <a name="internal-dns-service-idns-for-sdn"></a>[Interner DNS-Dienst (IDNs) für Sdn](Idns-for-Sdn.md)

Gehostete virtuelle Computer (VMS) und Anwendungen erfordern DNS für die Kommunikation innerhalb ihrer Netzwerke und mit externen Ressourcen im Internet. Mit IDNs können Sie Mandanten DNS-Namens Auflösungs Diensten für isolierte lokale Namespace-und Internet Ressourcen bereitstellen. 
  
## <a name="network-function-virtualization"></a>[Netzwerkfunktionsvirtualisierung](network-function-virtualization/Network-Function-Virtualization.md)

Hardware Geräte wie Load Balancer, Firewalls, Router und Switches werden zunehmend zu virtuellen Geräten. Microsoft verfügt über virtualisierte Netzwerke, Switches, Gateways, NATs, Lasten Ausgleichs Module und Firewalls. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung. Virtuelle Geräte werden schnell neu entwickelt und erstellen einen neuen Markt. Sie generieren weiterhin Interessen und gewinnen Dynamik sowohl bei Virtualisierungsplattformen als auch bei Clouddiensten. 
  
Die folgenden Technologien zur netzwerkfunktionsvirtualisierung sind verfügbar.  
  
-   **Software Load Balancer (SLB) und Netzwerk Adressübersetzung (NAT)** . Verbessern Sie den Durchsatz durch Unterstützung von Direct Server Return, bei dem der Rückgabe Netzwerk Datenverkehr den Lasten Ausgleichs-Multiplexer umgehen kann. Weitere Informationen finden Sie unter [Software Lastenausgleich/(SLB/) für Sdn](network-function-virtualization/software-load-balancing-for-sdn.md).
  
-   **Datacenter Firewall**. Stellen Sie differenzierte Zugriffs Steuerungs Listen (ACLs) bereit, mit denen Sie Firewallrichtlinien auf der Ebene der VM-Schnittstelle oder auf der Subnetzebene anwenden können. Weitere Informationen finden Sie unter [Übersicht über die Datacenter-Firewall](network-function-virtualization/Datacenter-Firewall-Overview.md).
  
-   **RAS-Gateway für Sdn**. Weiterleiten von Netzwerk Datenverkehr zwischen dem physischen Netzwerk und VM-Netzwerkressourcen, unabhängig vom Standort. Sie können den Netzwerk Datenverkehr an demselben physischen Standort oder an vielen verschiedenen Speicherorten weiterleiten. Weitere Informationen finden Sie unter [RAS-Gateway für Sdn](network-function-virtualization/RAS-Gateway-for-SDN.md).

## <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-set"></a>Remotezugriff auf den direkten Speicher (RDMA) und Switch Embedded Teaming (SET)  
In Windows Server 2016 können Sie RDMA auf Netzwerkadaptern aktivieren, die an einen virtuellen Hyper-V-Switch mit oder ohne Switch Embedded Teaming (Set) gebunden sind. Auf diese Weise können Sie weniger Netzwerkadapter verwenden, wenn Sie RDMA verwenden und gleichzeitig festlegen möchten.  
  
Set ist eine Alternative NIC-Team Vorgangs Lösung, die Sie in Umgebungen verwenden können, die Hyper-V und den Sdn-Stapel (Software Defined Networking) in Windows Server 2016 enthalten. Set integriert einige der NIC-Team Vorgangs Funktionen in den virtuellen Hyper-V-Switch.  
  
Mit Set können Sie zwischen einem und acht physischen Ethernet-Netzwerkadaptern in einem oder mehreren softwarebasierten virtuellen Netzwerkadaptern gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.  
Alle Netzwerkadapter für Mitglieder müssen auf demselben physischen Hyper-V-Host installiert sein, damit Sie in einem Team platziert werden können.  
  
Außerdem können Sie Windows PowerShell-Befehle verwenden, um Data Center Bridging (DCB) zu aktivieren, einen virtuellen Hyper-v-Switch mit einer virtuellen RDMA-NIC (VNIC) zu erstellen und einen virtuellen Hyper-v-Switch mit Set-und RDMA-vNICs zu erstellen. Weitere Informationen finden Sie unter [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming.md).

## <a name="border-gateway-protocol-bgp"></a>[Border Gateway Protocol (BGP)](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)
  
Border Gateway Protocol (BGP) ist ein dynamisches Routing Protokoll, das automatisch Routen Zwischenstand Orten lernt, die Standort-zu-Standort-VPN-Verbindungen verwenden. BGP reduziert daher die manuelle Konfiguration von Routern.   Wenn Sie das RAS-Gateway konfigurieren, können Sie mit BGP das Routing von Netzwerk Datenverkehr zwischen den VM-Netzwerken Ihrer Mandanten und Remote Standorten verwalten.  
  
## <a name="software-load-balancing-slb-for-sdn"></a>[Softwarelastenausgleich (SLB) für SDN](network-function-virtualization/software-load-balancing-for-sdn.md)
Clouddienstanbieter (Cloud Service Providers, CSPs) und Unternehmen, die Sdn bereitstellen, können den Software Lastenausgleich (Software Load Balancing, SLB) verwenden, um den Netzwerk Datenverkehr zwischen Mandanten und Mandanten Windows Server-SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen. 

## <a name="windows-server-containers"></a>[Windows Server-Container](Containers/Container-networking-overview.md)

Windows Server-Container sind eine vereinfachte Virtualisierungsmethode für das Betriebssystem, die Anwendungen oder Dienste von anderen Diensten trennt, die auf demselben Container Host ausgeführt werden. Jeder Container verfügt über ein eigenes Betriebssystem, Prozesse, Dateisystem, Registrierung und IP-Adressen, mit denen Sie eine Verbindung mit virtuellen Netzwerken herstellen können. 

## <a name="system-center"></a>System Center

Bereitstellen und Verwalten der Sdn-Infrastruktur mit [Virtual Machine Management (VMM)](https://docs.microsoft.com/system-center/vmm/) und [Operations Manager](https://docs.microsoft.com/system-center/scom/). Mit VMM können Sie die Ressourcen bereitstellen und verwalten, die zum Erstellen und Bereitstellen von virtuellen Computern und Diensten für private Clouds erforderlich sind.  Mit Operations Manager überwachen Sie Dienste, Geräte und Vorgänge in Ihrem gesamten Unternehmen, um ermitteln zu können, für welche Probleme sofortige Maßnahmen ergriffen werden müssen. 


---