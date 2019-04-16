---
title: SDN-Technologien
description: Die Themen in diesem Abschnittenthalten Übersicht und technischen Informationen zu der Software Defined Networking-Technologien, die in Windows Server2016 enthalten sind.
manager: brianlic
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: article
ms.assetid: b491089c-5bcb-49d4-95b1-915b7ce69f88
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1f842ac0d1a09106c1898374cf8dd1c7823d7dae
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="sdn-technologies"></a>SDN-Technologien

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Die Themen in diesem Abschnittenthalten Übersicht und technischen Informationen zu der Software Defined Networking-Technologien, die in Windows Server2016 enthalten sind.  
  
> [!NOTE]  
> Weitere Dokumentation für die Software Defined Networking können Sie die folgenden Abschnitte der Bibliothek verwenden.  
>   
> - [Planen der SDN](../plan/Plan-Software-Defined-Networking.md)
> - [Bereitstellen von SDN](../deploy/Deploy-Software-Defined-Networking.md)
> - [Verwalten von SDN](../manage/manage-sdn.md)
> - [Sicherheit für SDN](../security/sdn-security-top.md)
> - [Problembehandlung für SDN](../troubleshoot/Troubleshoot-Software-Defined-Networking.md)

Es gibt viele Technologien, mit die Microsoft Software Defined Networking (SDN) Lösungen, u. a. folgende:  
  
-   **[Border Gateway Protocol & 40; BGP & 41;](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)**  
  
    Wenn auf einem Windows Server2016 Remote Access Service (RAS)-Gateway konfiguriert ist, bietet Border Gateway Protocol (BGP) die Möglichkeit zum Verwalten des Routings von Netzwerkdatenverkehr zwischen VM-Netzwerken Ihrer Mandanten und Remotestandorten. BGP verringert den Bedarf an manueller Routingkonfiguration auf Routern, da er ein dynamisches Routingprotokoll ist, lernt automatisch Routen zwischen Standorten, die mithilfe von Standort-zu-Standort-VPN-Verbindungen verbunden sind.  
  
-   **[Datacenter Firewall (Übersicht)](../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)**  
  
    Datacenter Firewall ist ein neuer Dienst, der mit Windows Server2016 enthalten. Es ist ein Vermittlungsschicht, 5-Tupel (Protokoll, Quell- und Zielserver Portnummern, Quell- und Ziel-IP-Adressen), zustandsbehaftete, mehrinstanzenfähige Firewall. Wenn bereitgestellt und als Dienst vom Dienstanbieter angeboten, können Mandantenadministratoren installieren und Konfigurieren der Firewall-Richtlinien zum Schutz ihrer virtuellen Netzwerken von unerwünschten Datenverkehr aus dem Internet und Intranetnetzwerke.  
  
  
-   **[Hyper-V-Netzwerkvirtualisierung](../../sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)**  
  
    Hyper-V-Netzwerkvirtualisierung (HNV) ermöglicht die Virtualisierung von Kundennetzwerken auf der Basis einer gemeinsam genutzten physischen Netzwerkinfrastruktur.  
  
- **[Interne DNS-Dienst & 40; iDNS & 41; für SDN](../../sdn/technologies/Idns-for-Sdn.md)**

    \(VMs\) gehosteten virtuellen Computer und Anwendungen benötigen DNS innerhalb ihrer eigenen Netzwerke und mit externen Ressourcen im Internet kommunizieren. Mit iDNS können Sie Mandanten mit DNS-Namensauflösungsdienste für ihre isoliert, lokale Namensbereich und Ressourcen im Internet bereitstellen.

-   **[Netzwerkcontroller](../../sdn/technologies/network-controller/Network-Controller.md)**  
  
    Netzwerkcontroller bietet einen zentralen, programmierbaren Automatisierung zu verwalten, Konfiguration, Überwachung und Problembehandlung von virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum.  
  
-   **[Netzwerkfunktionsvirtualisierung](../../sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)**  
  
    Netzwerkfunktionen, die von Hardware (z.B. zum Lastenausgleich, Firewalls, Routern, Switches usw.) ausgeführt werden, sind zunehmend als virtuelle Appliances virtualisiert wird.  
  
    Microsoft hat Netzwerke, Switches, Gateways, NATs, Lastenausgleichsmodule und Firewalls virtualisiert.  

-   **[RAS-Gateway für SDN](../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)**
  
    RAS-Gateway ist ein softwarebasierter, mehrinstanzenfähiger, Border Gateway Protocol (BGP) fähigen Router in Windows Server2016, die für Clouddienstanbieter (CSPs) und Unternehmen, die mehrere Mandanten virtuelle Netzwerke mithilfe von Hyper-V-Netzwerkvirtualisierung hosten entwickelt wurde.  
      
- **[Remote Direct Memory Access & 40; RDMA & 41; und Switch Embedded Teaming & 40; SET & 41;](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)**  
  
    Eine zusammengeführte NIC können Sie um mit einem einzelnen Netzwerkadapter RDMA und Ethernet-Datenverkehr kombinieren. Die zusammengeführte NIC können Sie einen einzigen Netzwerkadapter für die Verwaltung, Remote Direct Memory Access RDMA-fähigen Speicher verwenden und mandantendatenverkehr. Dies verringert die Kapitalkosten, die mit jedem Server in Ihrem Datencenter verbunden sind, da Sie weniger Netzwerkadapter benötigen, um verschiedene Arten von Datenverkehr pro Server verwalten.  
  
    Ist eine NIC-Teaming-Lösung, die in den virtuellen Hyper-V-Switch integriert ist. Das teaming von bis zu acht physische NICS in einem einzelnen Satz-Team, dadurch verbessert die Verfügbarkeit und Failover können. In Windows Server2016 können Sie SET-Teams erstellen, die für die Verwendung von Server Message Block (SMB) und RDMA eingeschränkt werden.
  

-   **[Lastenausgleich & #40; SLB & #41; für SDN](../../sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)**  

    Clouddienstanbieter (CSPs) und Unternehmen, die Software Defined Networking (SDN) in Windows Server2016 bereitstellen können Software Load Balancing (SLB) verwenden, um Mandanten und Netzwerkdatenverkehr zwischen Ressourcen im virtuellen Netzwerk gleichmäßig zu verteilen. Die Windows Server-SLB ermöglicht mehrere Server zum Hosten derselben Workload hohe Verfügbarkeit und Skalierbarkeit.
  
-   **[System Center](../../sdn/Sc-Tech-for-Sdn.md)** Verwenden von System Center 2016 Virtual Machine Manager (VMM) und Operations Manager zum Bereitstellen und Verwalten der SDN-Infrastruktur, einschließlich Netzwerk-Controllern, Software zum Lastenausgleich und Gateways. Sie können VMM auch zentral definieren und Richtlinien für virtuelle Netzwerke zu steuern und die Richtlinien auf Ihre Anwendungen oder Arbeitsauslastungen verknüpfen.
  
- **[Windows-Container](../technologies/Containers/Container-networking-overview.md)**
    
    Windows Server-Container sind eine einfache Methode zur Betriebssystemvirtualisierung dar verwendet, um Anwendungen oder Dienste von anderen Diensten zu trennen, die auf demselben containerhost ausgeführt werden. Um dies zu ermöglichen, verfügt jeder Container eine eigene Ansicht der das Betriebssystem, Prozesse, Dateisystem, Registrierung und IP-Adressen. Mit Windows Server2016 können Sie jetzt Windows Server-Container mit virtuellen Netzwerken verbinden. Windows-Containern funktionieren ähnlich wie virtuelle Maschinen in Bezug auf Netzwerke. Jeder Container verfügt über einen virtuellen Netzwerkadapter, der mit einem virtuellen Switch verbunden ist, über den eingehender und ausgehender Datenverkehr weitergeleitet wird. Um die Isolation zwischen Containern auf demselben Host zu erzwingen, ist ein Netzwerkbereich erstellt, für jeden Windows Server- und Hyper-V-Container, in dem der Netzwerkadapter für den Container installiert wird. Windows Server-Container verwenden eine Host-vNIC für die Verbindung mit dem virtuellen Switch. Hyper-V-Container verwenden eine synthetische VM-NIC (nicht verfügbar gemacht, die Utility-VM), um mit dem virtuellen Switch verbinden.

