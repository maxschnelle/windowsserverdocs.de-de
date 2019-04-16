---
title: Software-Defined Networking (SDN)
description: In diesem Thema können Sie die Software Defined Networking (SDN)-Technologien erläutert, die in Windows Server, System Center und Microsoft Azure bereitgestellt werden.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9a1ea73c-20cd-42c5-95ad-b003b9cc6d64
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33351ccfa1466f667ef9351768c89b373734075d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="software-defined-networking-sdn"></a>Software-Defined Networking (SDN)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie die Software Defined Networking (SDN)-Technologien erläutert, die in Windows Server Datacenter Edition, System Center 2016 und Microsoft Azure bereitgestellt werden.  
  
> [!NOTE]
> Zusätzlich zu diesem Thema wird der folgende SDN-Inhalt verfügbar.
> 
> - [Was ist neu in SDN für Windows Server](sdn-whats-new.md)
> - [Einführung in die SDN in Windows Server Datacenter](sdn-intro.md)
> - [SDN-Technologien](technologies/Software-Defined-Networking-Technologies.md)  
> - [Planen der SDN](plan/Plan-Software-Defined-Networking.md) 
> - [Bereitstellen von SDN](deploy/Deploy-Software-Defined-Networking.md)  
> - [Verwalten von SDN](manage/manage-sdn.md)
> - [Sicherheit für SDN](security/sdn-security-top.md)
> - [Problembehandlung für SDN](troubleshoot/Troubleshoot-Software-Defined-Networking.md)
> - [System Center-Technologien für SDN](Sc-Tech-for-Sdn.md)
> - [Microsoft Azure und SDN](Azure_and_Sdn.md)
> - [Wenden Sie sich an den Datacenter Netzwerkteam Cloud](contact-sdn-team.md)
  
## <a name="bkmk_sdn"></a>Software-Defined Networking (Übersicht)

Software-Defined Networking \(SDN\) bietet eine Methode zum zentral konfigurieren und verwalten physische und virtuelle Netzwerkgeräte wie Router, Switches und Gateways in Ihrem Datencenter. Virtuelle Netzwerkelemente, z.B. virtuelle Hyper-V-Switch, Hyper-V-Netzwerkvirtualisierung und RAS-Gateway dienen als integrale Bestandteile Ihrer SDN-Infrastruktur.

>[!NOTE]
>Für Hyper-V-Hosts und virtuellen Maschinen \(VMs\), auf denen SDN-Infrastrukturserver, z. B. Netzwerkcontroller und Lastenausgleich Knoten ausgeführt, müssen Sie Windows Server 2016 Datacenter Edition installieren. Für Hyper-V-Hosts, die nur Mandanten Arbeitslast VMs enthalten, die mit SDN\ gesteuerte Netzwerken verbunden sind, können Sie Windows Server 2016 Standard Edition ausführen.

Während Sie Ihre vorhandenen physischen Switches, Router und andere Hardwaregeräte weiterhin verwenden können, können Sie eine umfassendere Integration zwischen dem virtuellen Netzwerk und dem physischen Netzwerk erreichen, wenn diese Geräte für die Kompatibilität mit Software-defined Networking gedacht sind.  
  
SDN ist möglich, da die Netzwerkebenen - Verwaltung, Steuerung und Daten-Ebenen - nicht mehr an die Netzwerkgeräte selbst gebunden sind, aber für die Verwendung durch andere Entitäten, z.B. Verwaltungssoftware für Datencenter wie System Center 2016 abstrahiert werden.  
  
SDN können Sie Ihr datencenternetzwerk um eine automatisierte, zentrale Möglichkeit, die Anforderungen Ihrer Anwendungen und Arbeitsauslastungen dynamisch zu verwalten. Software-defined Networking bietet die folgenden Funktionen.  
  
-   Die Möglichkeit, Ihre Anwendungen und Arbeitsauslastungen aus dem zugrunde liegenden physischen Netzwerk durch Virtualisierung des Netzwerks zu abstrahieren. Wie bei der Servervirtualisierung mit Hyper-V, sind die Abstraktionen konsistent und können mit Ihrer Anwendungen und Arbeitsauslastungen in einer nicht verwendet werden. Beispielsweise bietet Software-defined Networking virtuelle Abstraktionen für physische Netzwerkelemente, z.B. IP-Adressen, Switches und Lastenausgleichsmodule.  
  
-   Die Möglichkeit, zentral zu definieren und die Richtlinien, die physische und virtuelle Netzwerken, einschließlich der Datenfluss zwischen diesen beiden Netzwerktypen Regeln.  
  
-   Die Möglichkeit, Netzwerkrichtlinien auf konsistente Weise bei der Skalierung zu implementieren, selbst wenn Sie neue Arbeitsauslastungen bereitstellen oder Arbeitsauslastungen auf virtuellen oder physischen Netzwerken verschieben.  
  
## <a name="bkmk_ws"></a>Windows Server-Technologien für Software-Defined Networking  
Windows Server beinhaltet die folgenden Software-defined networking-Technologien.  

### <a name="bkmk_nc"></a>Netzwerkcontroller

Neue bietet in Windows Server2016 Netzwerkcontroller einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung beide virtuelle und physische Netzwerkinfrastruktur in Ihrem Rechenzentrum. Mithilfe von Netzwerkcontroller können Sie die Konfiguration der Netzwerkinfrastruktur, sondern die manuelle Konfiguration von Netzwerkgeräten und Diensten automatisieren.  
  
Netzwerkcontroller ist eine hoch verfügbare und skalierbare Serverrolle, und bietet eine Application programming Interface (API) – die Southbound-API -, die Kommunikation zwischen Netzwerkcontroller mit dem Netzwerk ermöglicht, und eine zweite API – die Northbound-API -, die die Kommunikation mit Netzwerkcontroller ermöglicht.  
  
Mit Windows PowerShell, die Representational State Transfer (REST)-API oder einer Verwaltungsanwendung, können Netzwerkcontroller Sie um die folgenden physischen und virtuellen Netzwerkinfrastruktur verwalten.  
  
-   Hyper-V-VMs und virtuelle switches  
  
-   Physische Netzwerkswitches  
  
-   Physische Netzwerkrouter  
  
-   Firewall-Software  
  
-   VPN-Gateways, einschließlich Remote Access Service (RAS) mehrinstanzenfähige Gateways  
  
-   Lastenausgleich  
  
Weitere Informationen finden Sie unter [Netzwerkcontroller](../sdn/technologies/network-controller/Network-Controller.md).  
  
### <a name="bkmk_hv"></a>Hyper-V-Netzwerkvirtualisierung

Hyper-V-Netzwerkvirtualisierung hilft Ihnen, Ihre Anwendungen und Arbeitsauslastungen aus dem physischen Netzwerk mithilfe virtueller Netzwerke abstrahieren. Virtuelle Netzwerke bieten die erforderliche mehrinstanzenfähige Isolation bei Ausführung in einem freigegebenen physischen Netzwerk-Fabric, dadurch Ressourcenverwendung fahren. Um sicherzustellen, dass Sie Ihre vorhandenen Investitionen weiter ausführen können, können Sie virtuelle Netzwerke auf vorhandenen netzwerkausrüstung einrichten. Darüber hinaus sind virtuelle Netzwerke mit virtuelle lokale Netzwerke (VLANs) kompatibel.  
  
Weitere Informationen finden Sie unter [Hyper-V-Netzwerkvirtualisierung](../sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md).  
  
### <a name="bkmk_switch"></a>Virtuelle Hyper-V-Switch

Die Hyper-V Virtual Switch ist ein softwarebasierten Schicht-2-Ethernet-Netzwerk-Switch, der im Hyper-V-Manager verfügbar ist, nachdem Sie die Hyper-V-Serverrolle installiert haben. Der Switch umfasst programmgesteuert verwaltete und erweiterbare Funktionen zum Verbinden von virtuellen Maschinen mit virtuellen Netzwerken und dem physischen Netzwerk. Darüber hinaus bietet Hyper-V Virtual Switch richtlinienerzwingung für Sicherheits-, Isolations- und Dienststufen.  
  
Virtuelle Hyper-V-Switch in Windows Server2016 können Sie auch Switch Embedded Teaming (SET) und (Remote Direct Memory Access, RDMA) bereitstellen. Weitere Informationen finden Sie im Abschnitt [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](#bkmk_rdma) in diesem Thema.  
  
Weitere Informationen zu virtuellen Hyper-V-Switch, finden Sie unter [virtuellen Hyper-V-Switch](../../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).

### <a name="bkmk_idns"></a>Interne DNS-Dienst & 40; iDNS & 41;

\(VMs\) gehosteten virtuellen Computer und Anwendungen benötigen DNS innerhalb ihrer eigenen Netzwerke und mit externen Ressourcen im Internet kommunizieren. Mit iDNS können Sie Mandanten mit DNS-Namensauflösungsdienste für ihre isoliert, lokale Namensbereich und Ressourcen im Internet bereitstellen.

Weitere Informationen finden Sie unter [interner DNS-Dienst & 40; iDNS & 41; für SDN](technologies/Idns-for-Sdn.md).
  
### <a name="bkmk_nfv"></a>Netzwerkfunktionsvirtualisierung

In der heutigen Software sind definierte Rechenzentren, Netzwerkfunktionen, die von Hardware (z. B. zum Lastenausgleich, Firewalls, Routern, Switches usw.) ausgeführt werden, zunehmend als virtuelle Appliances virtualisiert wird. Diese "netzwerkfunktionsvirtualisierung" ist ein natürlicher Fortschritt der Servervirtualisierung und Netzwerkvirtualisierung. Virtuelle Appliances sind schnell neu aufkommender und erstellen einen völlig neuen Markt. Generierung von Interesse und Dynamik in beiden Virtualisierungsplattformen und cloud-Dienste weiter.  
  
Die folgenden Netzwerkfunktionsvirtualisierung Technologien sind verfügbar.  
  
-   **Softwarelastenausgleich (SLB) und Netzwerkadressübersetzung (NAT)**. Die Nord-Süd und OST-West layer-4-Lastenausgleich und NAT verbessert den Durchsatz durch die Unterstützung der direkten Server zurück, mit dem der Rückgabetyp Netzwerkdatenverkehr der Netzwerklastenausgleich zur Vereinheitlichung umgehen. Weitere Informationen finden Sie unter [Software Load Balancing (SLB) für SDN](technologies/network-function-virtualization/software-load-balancing-for-sdn.md).  
  
-   **Datacenter Firewall**. Dieser verteilten Firewall bietet präzise Zugriffssteuerungslisten (ACLs), aktivieren Sie auf der Ebene der VM-Schnittstelle oder auf der Subnetzebene-Firewall-Richtlinien anwenden.  
  
    Weitere Informationen finden Sie unter [Datacenter Firewall (Übersicht)](../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).  
  
-   **RAS-Gateway**. Sie können Gateways für Datenverkehr zwischen virtuellen Netzwerken und Netzwerken nicht virtualisierten Bridging verwenden. Insbesondere können Sie die Standort-zu-Standort-VPN-Gateways, Weiterleitung Gateways und Generic Routing Encapsulation (GRE)-Gateways bereitstellen. Darüber hinaus M+N Redundanz Gateways wird unterstützt. Weitere Informationen finden Sie unter [RAS-Gateway für SDN](technologies/network-function-virtualization/RAS-Gateway-for-SDN.md).
  
Weitere Informationen finden Sie unter [Netzwerkfunktionsvirtualisierung](technologies/network-function-virtualization/Network-Function-Virtualization.md).  
  
### <a name="bkmk_rdma"></a>Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (SET)  
In Windows Server2016 können Sie RDMA für Netzwerkadapter, die mit einem virtuellen Hyper-V-Switch mit oder ohne Switch Embedded Teaming (SET) gebunden sind. Dadurch können Sie weniger Netzwerkadapter verwenden, wenn Sie RDMA und SET verwenden möchten zur gleichen Zeit.  
  
Eine alternative NIC-Teaming-Lösung, die Sie in einer Umgebung verwenden können, die Hyper-V und der Stapel Software Defined Networking (SDN) in Windows Server2016 enthalten ist. SET integriert Teil der NIC-Teaming-Funktionen in den virtuellen Hyper-V-Switch.  
  
Können Sie zwischen einem und acht physische Ethernet-Netzwerkadapter in einen oder mehrere softwarebasierte virtuelle Netzwerkadapter gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei einem Fehler des Netzwerkadapters.  
SET-Member-Netzwerkadapter müssen in dem gleichen physischen Hyper-V-Host in einem Team platziert werden installiert sein.  
  
Darüber hinaus können Sie Windows PowerShell-Befehle zum Aktivieren von Data Center Bridging (DCB), erstellen einen virtuellen Hyper-V-Switch mit einer virtuellen RDMA-Netzwerkkarte (vNIC), und erstellen einen virtuellen Hyper-V-Switch mit SET und RDMA-vNICs.  
  
Weitere Informationen finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](https://technet.microsoft.com/library/mt403349.aspx).  
  
### <a name="bkmk_rras"></a>RAS-Gateway für SDN  
RAS-Gateway ist ein softwarebasierter, mehrinstanzenfähiger, Border Gateway Protocol (BGP) fähigen Router in Windows Server2016, die für Clouddienstanbieter (CSPs) und Unternehmen, die mehrere Mandanten virtuelle Netzwerke mithilfe von Hyper-V-Netzwerkvirtualisierung hosten entwickelt wurde.  
  
RAS-Gateway bietet Gateway Pools, M+N Redundanz, mehrere Typen von Standort-zu-Standort-VPN-Verbindungen und BGP-Route-Reflector um flexible Designoptionen für Ihre Gateway-Infrastruktur bereitzustellen.  
  
Weitere Informationen finden Sie unter [RAS-Gateway für SDN](technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
  
### <a name="bkmk_slb"></a>Softwarelastenausgleich (SLB)  
Clouddienstanbieter (CSPs) und Unternehmen, die Software Defined Networking (SDN) in Windows Server2016 bereitstellen können Software Load Balancing (SLB) verwenden, um Mandanten und Netzwerkdatenverkehr zwischen Ressourcen im virtuellen Netzwerk gleichmäßig zu verteilen. Die Windows Server-SLB ermöglicht mehrere Server zum Hosten derselben Workload hohe Verfügbarkeit und Skalierbarkeit.  
  
Weitere Informationen finden Sie unter [Lastenausgleich & 40; SLB & 41; für SDN](../sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md).

### <a name="windows-server-containers"></a>Windows Server-Container

Windows Server-Container sind eine einfache Methode zur Betriebssystemvirtualisierung dar verwendet, um Anwendungen oder Dienste von anderen Diensten zu trennen, die auf demselben containerhost ausgeführt werden. Um dies zu ermöglichen, verfügt jeder Container eine eigene Ansicht der das Betriebssystem, Prozesse, Dateisystem, Registrierung und IP-Adressen. Mit Windows Server2016 können Sie jetzt Windows Server-Container mit virtuellen Netzwerken verbinden. Weitere Informationen finden Sie unter [Windows Server-Container](technologies/containers/Container-networking-overview.md).

### <a name="contact-the-datacenter-and-cloud-networking-product-team"></a>Wenden Sie sich an das Produktteam Rechenzentren und Cloud-Netzwerk

Sie diskutieren SDN-Technologien, mit Microsoft oder anderen SDN-Kunden interessieren, stehen zahlreiche Methoden für die Herstellung Kontakt.

Weitere Informationen finden Sie unter [wenden Sie sich an den Datacenter Cloud zuständige Team](contact-sdn-team.md).
