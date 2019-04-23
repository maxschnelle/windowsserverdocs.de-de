---
title: Was ist neu in Netzwerken
description: Dieses Thema enthält allgemeine Informationen zu neuen Features und Technologien für Netzwerke in Windows Server 2016
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: get-started-article
ms.assetid: 08fb7563-d319-48a9-b181-ca0ca3032c18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 43ce6290f6559be7cb078032b79519d1681506d4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829191"
---
# <a name="whats-new-in-networking"></a>Was ist neu in Netzwerken

>Gilt für: Windows Server 2016

Im folgenden werden die neuen oder verbesserten netzwerktechnologien in Windows Server 2016.  
  Benutzerprofil-Datenträger in diesem Thema enthält die folgenden Abschnitte.  
  
-   [Neue Netzwerkfeatures und-Technologien](#bkmk_features)  
  
-   [Neue Features für zusätzliche Networking-Technologien](#bkmk_existing)  
  
## <a name="bkmk_features"></a>Neue Netzwerkfeatures und-Technologien

Netzwerk ist ein grundlegender Bestandteil der Plattform (Software definiert Datacenter, SDDC), und Windows Server 2016 bietet neue und verbesserte Software Defined Networking (SDN)-Technologien, um Ihnen zu einer vollständig implementierten SDDC-Lösung für Ihre Organisation zu erleichtern.  
  
Wenn Sie Netzwerke als softwaredefinierte Ressource verwalten, können Sie Beschreiben der Anforderungen an die Infrastruktur von einer Anwendung nur einmal, und wählen Sie dann, wo die Anwendung ausgeführt wird – lokal oder in der Cloud.  Diese Konsistenz bedeutet, dass Ihre Anwendungen jetzt leichter zu skalieren sind und nahtlos mit der gleichen Zuverlässigkeit hinsichtlich Sicherheit, Leistung, Dienstqualität und Verfügbarkeit überall ausgeführt werden können.  
  
Die folgenden Abschnitte enthalten Informationen zu diesen new networking Features und Technologien.  
  
### <a name="software-defined-networking-infrastructure"></a>Software-Defined Networking-Infrastruktur

Im folgenden werden die neuen oder verbesserten SDN-Infrastruktur-Technologien.  
  
-   **Netzwerkcontroller**. In Windows Server 2016 bietet neue Netzwerkcontroller einen Punkt zentralen, programmierbaren Automatisierung von Verwaltung, konfigurieren, überwachen und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum an. Mithilfe von Netzwerkcontroller können Sie die Konfiguration der Netzwerkinfrastruktur automatisieren und müssen Netzwerkgeräte und -dienste nicht länger manuell konfigurieren. Weitere Informationen finden Sie unter [Netzwerkcontroller](sdn/technologies/network-controller/Network-Controller.md) und [Bereitstellen von Softwaredefinierten Netzwerken mithilfe von Skripts](https://technet.microsoft.com/library/mt427380.aspx).  
  
-   **Hyper-V-Switches**. Der virtuelle Hyper-V-Switches auf Hyper-V-Hosts ausgeführt und ermöglicht Ihnen die Erstellung verteilter wechseln und routing, und eine Ebene der Richtlinie erzwingen, ausgerichtet und mit Microsoft Azure kompatibel ist. Weitere Informationen finden Sie unter [Hyper-V Virtual Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).  
  
-   **(NFV)-Funktion Netzwerkvirtualisierung**. In die heutige Software sind definierte Rechenzentren, Netzwerkfunktionen, die von Hardware (z. B. Load balancer, Firewalls, Routern, Switches usw.) ausgeführt werden, zunehmend als virtuelle Appliances bereitgestellt wird. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung. Virtuelle Geräte sind schnell entwickelt und erstellen einen völlig neuen Markt. Generieren von Interesse sind und erhalten Momentum auf beiden Virtualisierungsplattformen und cloud-Dienste weiterhin. Die folgenden NFV Technologien sind in Windows Server 2016 verfügbar.  
  
    -   **Datacenter Firewall**. Diese verteilte Firewall bietet eine präzise Zugriffssteuerungslisten (ACLs), aktivieren Sie auf der VM-Schnittstellenebene oder auf Subnetzebene-Firewall-Richtlinien anwenden.  
  
        Weitere Informationen finden Sie unter [Datacenter Firewall – Übersicht](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).  
  
    -   **RAS-Gateway**. Sie können die RAS-Gateway für den Datenverkehr zwischen virtuellen Netzwerken und physischen Netzwerken, einschließlich von Standort-zu-Standort-VPN-Verbindungen aus Ihrem clouddatencenter an Remotestandorte Ihres Mandanten verwenden. Sie können insbesondere Internet Key Exchange Version 2 (IKEv2) bereitstellen Standort-zu-Standort virtuelle private Netzwerke (VPNs), VPN mit Layer-3 (L3), und Generic Routing Encapsulation (GRE)-Gateways. Darüber hinaus werden gatewaypools und M + N-Redundanz von Gateways jetzt unterstützt. und Border Gateway Protocol (BGP) mit Route-Reflector-Funktionen bietet, dynamisches routing zwischen Netzwerken für alle Gateway-Szenarios (IKEv2-VPN-GRE VPN und L3-VPN-).  
  
        Weitere Informationen finden Sie unter [Neuigkeiten in der RAS-Gateway](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) und [RAS-Gateway für SDN](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md).  
          
    - **Softwarelastenausgleich (SLB) und Netzwerkadressübersetzung (NAT)**. Die Nord-Süd und OST-West-layer-4-Lastenausgleich und NAT verbessert den Durchsatz durch die Unterstützung von Direct Server Return, mit dem kann die Netzwerk-antwortdatenverkehr umgehen der Load Balancing multiplexer.  
       Weitere Informationen finden Sie unter [Softwarelastenausgleich &#40;SLB&#41; für SDN](sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).  
  
    Weitere Informationen finden Sie unter [Netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md).  
  
-   **Standardisierte Protokolle**. Netzwerkcontroller verwendet Representational State Transfer (REST) auf die northbound-Schnittstelle mit JavaScript Object Notation (JSON)-Nutzlasten. Die Netzwerkcontroller-southbound-Benutzeroberfläche verwendet Open-vSwitch-Datenbank-Management-Protokoll (OVSDB).  
  
-   **Flexible Kapselung Technologien**. Diese Technologien arbeiten auf der Datenebene und virtuellen Extensible LANS (VxLAN) und Network Virtualization Generic Routing Encapsulation (NVGRE) unterstützen. Weitere Informationen finden Sie unter [GRE Tunneling in Windows Server 2016](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md).  
  
Weitere Informationen zu den SDN, finden Sie unter [Software Defined Networking &#40;SDN&#41;](sdn/software-defined-networking.md).  
  
### <a name="cloud-scale-fundamentals"></a>Grundlagen der Cloud skalieren
 
Die folgenden Grundlagen des Cloud-skalieren sind jetzt verfügbar.  
  
-   **Zusammengeführte Netzwerkschnittstellenkarte (NIC)**. Die zusammengeführte NIC können Sie einen Netzwerkadapter für Remote Direct Memory Access, RDMA-fähigen Speicher, Verwaltung und mandantendatenverkehr. Dies reduziert die Ausgaben, die mit jedem Server in Ihrem Datencenter, verknüpft sind, da Sie weniger Netzwerkadapter zum Verwalten von verschiedenen Arten von Datenverkehr pro Server benötigen.  
  
-   **Packetdirect**.  Packetdirect bietet einen hohen Durchsatz beim Datenverkehr und verarbeitungsinfrastruktur mit geringer Latenz-Paket.  
  
-   **Switch Embedded Teaming (SET)**.        Ist eine NIC-Teamvorgang-Lösung, die in den virtuellen Hyper-V-Switch integriert ist. Gruppe ermöglicht den Teamvorgang von bis zu acht physische NICS in einem einzelnen Satz-Team, das verbessert die Verfügbarkeit und ermöglicht ein Failover. In Windows Server 2016 können Sie die SET-Teams erstellen, die für die Verwendung von Server Message Block (SMB) und RDMA beschränkt sind. Darüber hinaus können Sie SET-Teams verwenden, um Netzwerkdatenverkehr für die Hyper-V-Netzwerkvirtualisierung zu verteilen. Weitere Informationen finden Sie unter [Remote Direct Memory Access &#40;RDMA&#41; und Switch Embedded Teaming &#40;festgelegt&#41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  
  
## <a name="bkmk_existing"></a>Neue Features für zusätzliche Networking-Technologien

Dieser Abschnitt enthält Informationen zu neuen Features für networking-Technologien vertraut sind.
  
## <a name="bkmk_dhcp"></a>DHCP  
DHCP ist ein IETF (Internet Engineering Task Force)-Standard, der den Verwaltungsaufwand und die Komplexität beim Konfigurieren von Hosts in einem TCP/IP-basierten Netzwerk, wie z. B. einem privaten Intranet, reduziert. Der DHCP-Serverdienst führt den Konfigurationsprozess für TCP/IP auf DHCP-Clients automatisch durch.  
  
Weitere Informationen finden Sie unter [Neues in DHCP](technologies/dhcp/What-s-New-in-DHCP.md).  
  
## <a name="bkmk_dns"></a>DNS  
Bei DNS handelt es sich um ein System, das in TCP/IP-Netzwerke zum Benennen von Computern und Netzwerkdiensten verwendet wird. Die DNS-Namensgebung sucht Computer und Dienste über benutzerfreundliche Namen. Wenn ein Benutzer in einer App einen DNS-Namen eingibt, können die DNS-Dienste den Namen in andere dem Namen entsprechende Informationen auflösen, z. B. in eine IP-Adresse.  
  
Im folgenden sehen Informationen zu DNS-Client und DNS-Server.  
  
### <a name="bkmk_dnsc"></a>DNS-Client  
Im folgenden werden die neuen oder verbesserten DNS-Client-Technologien.  
  
-   **DNS-Client-dienstbindung**. In Windows 10 bietet der DNS-Clientdienst die verbesserte Unterstützung für Computer mit mehr als eine Netzwerkschnittstelle.  
  
Weitere Informationen finden Sie unter [Neuigkeiten in DNS-Client unter Windows Server 2016](dns/What-s-New-in-DNS-Client.md)  
  
### <a name="bkmk_dnss"></a>DNS-Server  
Im folgenden werden die neuen oder verbesserten DNS-Server-Technologien.  
  
-   **DNS-Richtlinien**.  Sie können konfigurieren, dass DNS-Richtlinien, um anzugeben, wie ein DNS-Server auf DNS-Abfragen reagiert. DNS-Antworten können basierend auf IP-Adresse für die Clients (Standort), der den Tag und einige andere Parameter. DNS-Richtlinien ermöglichen die Speicherort-fähigen DNS-Verwaltung des Datenverkehrs, Lastenausgleich, Split-Brain-DNS- und andere Szenarien.  
  
-   **Nano Server-Unterstützung für die Datei auf der Basis-DNS-**, Sie können DNS-Server unter Windows Server 2016 auf einem Nano Server-Image bereitstellen. Diese Bereitstellungsoption ist Ihnen zur Verfügung, bei Verwendung der dateibasierte DNS. Von ausgeführten DNS-Server auf einem Nano Server-Image können Sie Ihre DNS-Server mit reduzierten schnell gestartet und minimierten Patches ausführen.  
  
    > [!NOTE]   
    > Active Directory integrierten DNS wird für Nano Server nicht unterstützt.  
  
-   **Antwort bewerten begrenzenden (RRL)**.  Sie können die Antwort die Begrenzung der Übertragungsrate für Ihre DNS-Server aktivieren. Auf diese Weise vermeiden Sie die Möglichkeit, böswillige Systeme, die mit Ihrer DNS-Server um einen DoS-Angriff auf einen DNS-Client zu initiieren.  
  
-   **DNS-basierte Authentifizierung von benannten Entitäten (DANE)**.   Sie können TLSA (Transport Layer Security-Authentifizierung) Datensätze verwenden, um Informationen für DNS-Clients bereitzustellen, die Status der ausstellende Zertifizierungsstelle (CA) für Ihren Domänennamen ein Zertifikat erwarten, sollten. Dies verhindert, dass Man-in-the-Middle-Angriffe, in denen ein Benutzer möglicherweise beschädigen den DNS-Cache auf ihrer eigenen Website verweisen, und geben Sie ein Zertifikat, das sie von einer anderen Zertifizierungsstelle ausgestellt.  
  
-   **Unterstützung für unbekannte Datensatz**.   
     Sie können Datensätze hinzufügen, die nicht explizit vom Windows-DNS-Server mithilfe der Funktion unbekannt Datensatz unterstützt werden.  
  
-   **IPv6-Stammhinweise**.   
     Sie können die systemeigene IPv6-Adresse verwenden, Stammhinweise zu unterstützen, um die Auflösung von Internetnamen verwenden die IPV6-Server ausführen.  
  
-   **Verbesserte Unterstützung für Windows PowerShell**.   
      Neue Windows PowerShell-Cmdlets sind für DNS-Server verfügbar.  
  
Weitere Informationen finden Sie unter [Neuigkeiten in DNS-Server unter Windows Server 2016](dns/What-s-New-in-DNS-Server.md)  
  
## <a name="bkmk_GRE"></a>GRE-Tunneling  
RAS-Gateway unterstützt jetzt hochverfügbarkeit Generic Routing Encapsulation (GRE)-Tunnel für die Standort-zu-Standort-Verbindungen und M + N-Redundanz von Gateways. GRE ist ein einfaches Tunneling-Protokoll, das eine Vielzahl von Protokollen der Vermittlungsschicht in virtuellen Point-to-Point-Links über ein IP-Internetwork kapseln kann.  
  
Weitere Informationen finden Sie unter [GRE Tunneling in Windows Server 2016](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md).  
  
## <a name="HNV"></a>Hyper-V-Netzwerkvirtualisierung  
In Windows Server 2012 eingeführt wurde, ermöglicht Hyper-V-Netzwerkvirtualisierung (HNV) die Virtualisierung von Kundennetzwerken auf der Basis einer gemeinsam genutzten physischen Netzwerkinfrastruktur. Mit nur minimale Änderungen erforderlich, auf dem physischen Netzwerk-Fabric, bietet HNV-Dienstanbieter die Agilität, bereitstellen und Migrieren von mandantenworkloads an einer beliebigen Stelle in der drei Clouds: der Service Provider-Cloud, die private Cloud oder der öffentlichen Cloud von Microsoft Azure.  
  
Weitere Informationen finden Sie unter [Neues in Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)  
  
## <a name="bkmk_ipam"></a>IPAM  
IPAM stellt umfassend anpassbare Verwaltungs- und Überwachungsfunktionen Funktionen für die IP-Adresse und DNS-Infrastruktur im Netzwerk einer Organisation bereit. Verwenden von IPAM, können Sie überwachen, überwachen und Verwalten von Servern, auf denen Dynamic Host Configuration-Protokoll (DHCP) und Domain Name System (DNS) ausgeführt werden.  
  
-   **Erweiterte IP-Adressverwaltung**.  
     IPAM-Funktionen werden für Szenarien wie das Behandeln von /32 für IPv4 und IPv6-/128 Subnetze, und Suchen von kostenlose Subnetze von IP-Adressen und Bereiche in eine IP-Adressblock verbessert.  
  
-   **Erweiterte DNS-dienstverwaltung**.  
     IPAM unterstützt die DNS-Ressourceneintrag, bedingte Weiterleitung und Verwaltung der DNS-Zone für Domäne Active Directory-integriert und zugrunde liegender Datei DNS-Server.  
  
-   **Integrierte Verwaltung von DNS, DHCP und IP-Adresse (DDI)**.  
     Viele neue Funktionen und integrierte Lifecycle-Verwaltungsvorgänge aktiviert sind, wie z. B. das Visualisieren von Ressourcen für alle DNS-Datensätze, die eine IP-Adresse betreffen, beheben, automatisierte Inventarisierung von IP-Adressen, die basierend auf DNS-Ressourceneinträgen und lebenszyklusverwaltung für IP-Adresse für sowohl DNS- und DHCP-Vorgänge.  
  
-   **Unterstützung für mehrere Active Directory-Gesamtstruktur**.  
     Sie können IPAM verwenden, verwalten Sie die DNS- und DHCP-Server, der mehrere Active Directory-Gesamtstrukturen aus, wenn eine bidirektionale Vertrauensstellung zwischen der Gesamtstruktur, auf dem IPAM installiert ist, und jede vorhandene remote vorhanden ist.  
  
-   **Windows PowerShell-Unterstützung für die rollenbasierte Zugriffssteuerung**.  
     Sie können Windows PowerShell verwenden, zum Festlegen von zugriffsbereichen für IPAM-Objekte.  
  
Weitere Informationen finden Sie unter [Neues in IPAM](technologies/ipam/What-s-New-in-IPAM.md) und [Verwalten von IPAM](technologies/ipam/Manage-IPAM.md).  
  

