---
title: Neues bei Netzwerken
description: Dieses Thema enthält allgemeine Informationen zu neuen Features und Technologien für Netzwerke in Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: get-started-article
ms.assetid: 08fb7563-d319-48a9-b181-ca0ca3032c18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 85b1a573e8ac724a2a9e22863f890db668423cad
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-networking"></a>Neues bei Netzwerken

>Gilt für: Windows Server 2016

Im folgenden werden die neuen oder verbesserten netzwerktechnologien in Windows Server 2016.  
  
Dieses Thema enthält die folgenden Abschnitte.  
  
-   [Neue Netzwerkfeatures und -Technologien](#bkmk_features)  
  
-   [Neue Features für zusätzliche Networking-Technologien](#bkmk_existing)  
  
## <a name="bkmk_features"></a>Neue Netzwerkfeatures und -Technologien

Netzwerk ist ein grundlegender Bestandteil der Plattform (Software definierten Datacenter, SDDC), und Windows Server 2016 bietet neue und verbesserte Software Defined Networking (SDN)-Technologien, um Ihnen zu einer vollständig implementierten SDDC-Lösung für Ihre Organisation zu erleichtern.  
  
Wenn Sie Netzwerke als softwaredefinierte Ressource verwalten, können Sie eine Anwendung infrastrukturanforderungen einmal beschreiben, und wählen Sie dann, wo die Anwendung ausgeführt wird – lokal oder in der Cloud.  Diese Konsistenz bedeutet, dass Ihre Anwendungen jetzt einfacher zu skalieren sind und nahtlos mit der gleichen Zuverlässigkeit hinsichtlich Sicherheit, Leistung, Qualität und Verfügbarkeit überall ausgeführt werden können.  
  
Die folgenden Abschnitte enthalten Informationen zu diesen neuen Features und Technologien zum Netzwerk.  
  
### <a name="software-defined-networking-infrastructure"></a>Software-Defined Networking-Infrastruktur

Im folgenden werden die neuen oder verbesserten SDN-Infrastruktur-Technologien.  
  
-   **Netzwerk-Controller**. Neue bietet in Windows Server 2016 Netzwerkcontroller einer zentralen, programmierbaren Automatisierung zu verwalten, Konfiguration, Überwachung und Problembehandlung von virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum. Mithilfe von Netzwerkcontroller können Sie die Konfiguration der Netzwerkinfrastruktur, sondern die manuelle Konfiguration von Netzwerkgeräten und Diensten automatisieren. Weitere Informationen finden Sie unter [Netzwerkcontroller](sdn/technologies/network-controller/Network-Controller.md) und [Bereitstellen von Softwaredefinierten Netzwerken mithilfe von Skripts](https://technet.microsoft.com/library/mt427380.aspx).  
  
-   **Hyper-V Virtual Switch**. Der Hyper-V-Switch auf Hyper-V-Hosts ausgeführt und ermöglicht es Ihnen, verteilte wechseln und das routing zu erstellen und eine Richtlinie Erzwingung Ebene ausgerichtet und mit Microsoft Azure kompatibel ist. Weitere Informationen finden Sie unter [virtuellen Hyper-V-Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).  
  
-   **Netzwerkvirtualisierung Funktion (NFV)**. In der heutigen Software sind definierte Rechenzentren, Netzwerkfunktionen, die von Hardware (z. B. zum Lastenausgleich, Firewalls, Routern, Switches usw.) ausgeführt werden, zunehmend als virtuelle Appliances bereitgestellt wird. Diese "netzwerkfunktionsvirtualisierung" ist ein natürlicher Fortschritt der Servervirtualisierung und Netzwerkvirtualisierung. Virtuelle Appliances sind schnell neu aufkommender und erstellen einen völlig neuen Markt. Generierung von Interesse und Dynamik in beiden Virtualisierungsplattformen und cloud-Dienste weiter. Die folgenden NFV Technologien sind in Windows Server 2016 verfügbar.  
  
    -   **Datacenter Firewall**. Dieser verteilten Firewall bietet präzise Zugriffssteuerungslisten (ACLs), aktivieren Sie auf der Ebene der VM-Schnittstelle oder auf der Subnetzebene-Firewall-Richtlinien anwenden.  
  
        Weitere Informationen finden Sie unter [Datacenter Firewall (Übersicht)](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).  
  
    -   **RAS-Gateway**. Sie können die RAS-Gateway Datenverkehr zwischen virtuellen Netzwerken und physischen Netzwerken, einschließlich der Standort-zu-Standort-VPN-Verbindungen von Ihrem clouddatencenter an Remotestandorte Ihrer Mandanten verwenden. Genauer gesagt: Sie können Internet Key Exchange Version 2 (IKEv2) bereitstellen Standort-zu-Standort virtuelle private Netzwerke (VPNs), VPN-Layer 3 (L3) und Gateways Generic Routing Encapsulation (GRE). Darüber hinaus werden die Gateway-Pools und M + N Redundanz Gateways jetzt unterstützt. und Border Gateway Protocol (BGP) mit Route-Reflector-Funktionen bietet dynamisches routing zwischen Netzwerken für alle Gateway-Szenarien (IKEv2-VPN-GRE VPN und L3-VPN).  
  
        Weitere Informationen finden Sie unter [What's New in RAS-Gateway](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) und [RAS-Gateway für SDN](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md).  
          
    - **Softwarelastenausgleich (SLB) und Netzwerkadressübersetzung (NAT)**. Die Nord-Süd und OST-West layer-4-Lastenausgleich und NAT verbessert den Durchsatz durch die Unterstützung der direkten Server zurück, mit dem der Rückgabetyp Netzwerkdatenverkehr der Netzwerklastenausgleich zur Vereinheitlichung umgehen.  
       Weitere Informationen finden Sie unter [Lastenausgleich & #40; SLB & #41; für SDN](sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).  
  
    Weitere Informationen finden Sie unter [Netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md).  
  
-   **Protokolle standardisiert**. Netzwerkcontroller verwendet Representational State Transfer (REST) auf der northbound-Schnittstelle mit Nutzlasten, die JavaScript Object Notation (JSON). Die southbound Netzwerkcontroller-Schnittstelle verwendet öffnen vSwitch Datenbank-Management-Protokoll (OVSDB).  
  
-   **Flexible Kapselung Technologien**. Diese Technologien arbeiten auf der Ebene für Daten und Unterstützung für Virtual Extensible LAN (VxLAN) und Network Virtualization Generic Routing Encapsulation (NVGRE). Weitere Informationen finden Sie unter [GRE-Tunneling in Windows Server 2016](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md).  
  
Weitere Informationen zu den SDN, finden Sie unter [Software Defined Networking & #40; SDN & #41; ](sdn/software-defined-networking.md).  
  
### <a name="cloud-scale-fundamentals"></a>Grundlagen der Cloud-Skalierung
 
Die folgenden Cloud Skalierung Grundlagen sind jetzt verfügbar.  
  
-   **Zusammengeführtes Netzwerkschnittstellenkarte (NIC)**. Die zusammengeführte NIC können Sie einen einzigen Netzwerkadapter für die Verwaltung, Remote Direct Memory Access RDMA-fähigen Speicher verwenden und mandantendatenverkehr. Dies verringert die Kapitalkosten, die mit jedem Server in Ihrem Datencenter verbunden sind, da Sie weniger Netzwerkadapter benötigen, um verschiedene Arten von Datenverkehr pro Server verwalten.  
  
-   **Paket Direct**.  Paket Direct bietet einen hohen Datenverkehr Durchsatz und verarbeitungsinfrastruktur mit geringer Wartezeit Paket.  
  
-   **Switch Embedded Teaming (SET)**.        Ist eine NIC-Teaming-Lösung, die in den virtuellen Hyper-V-Switch integriert ist. Das teaming von bis zu acht physische NICS in einem einzelnen Satz-Team, dadurch verbessert die Verfügbarkeit und Failover können. In Windows Server 2016 können Sie SET-Teams erstellen, die für die Verwendung von Server Message Block (SMB) und RDMA eingeschränkt werden. Darüber hinaus können Sie SET-Teams zur Verteilung des Netzwerkdatenverkehrs für Hyper-V-Netzwerkvirtualisierung. Weitere Informationen finden Sie unter [Remote Direct Memory Access & 40; RDMA & 41; und Switch Embedded Teaming & 40; SET & 41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  
  
## <a name="bkmk_existing"></a>Neue Features für zusätzliche Networking-Technologien

Dieser Abschnitt enthält Informationen zu neuen Features für netzwerktechnologien vertraut.
  
## <a name="bkmk_dhcp"></a>DHCP  
DHCP ist ein Internet Engineering Task Force (IETF)-Standard, der den Verwaltungsaufwand und die Komplexität beim Konfigurieren von Hosts in einem TCP/IP-basierten Netzwerk, z. B. einem privaten Intranet zu reduzieren. Mithilfe des DHCP-Serverdiensts führt den Konfigurationsprozess für TCP/IP auf DHCP-Clients automatisch.  
  
Weitere Informationen finden Sie unter [What's New in DHCP](technologies/dhcp/What-s-New-in-DHCP.md).  
  
## <a name="bkmk_dns"></a>DNS  
DNS ist ein System, das in TCP/IP-Netzwerken zum Benennen von Computern und Netzwerkdiensten verwendet wird. DNS-Namensgebung sucht Computer und Dienste über benutzerfreundliche Namen. Wenn ein Benutzer einen DNS-Namen in einer Anwendung eingibt, können DNS-Dienste den Namen in andere Informationen auflösen, die den Namen, z. B. eine IP-Adresse zugeordnet ist.  
  
Im folgenden sehen Informationen zu DNS-Client und DNS-Server.  
  
### <a name="bkmk_dnsc"></a>DNS-Client  
Im folgenden werden die neuen oder verbesserten DNS-Client-Technologien.  
  
-   **DNS-Client die Bindung**. In Windows 10 bietet der DNS-Clientdienst verbesserte Unterstützung für Computer mit mehr als einer Netzwerkschnittstelle.  
  
Weitere Informationen finden Sie unter [What's New in DNS-Client unter Windows Server 2016](dns/What-s-New-in-DNS-Client.md)  
  
### <a name="bkmk_dnss"></a>DNS-Server  
Im folgenden werden die neuen oder verbesserten DNS-Server-Technologien.  
  
-   **DNS-Richtlinien**.  Sie können konfigurieren, dass DNS-Richtlinien, um anzugeben, wie ein DNS-Server auf DNS-Abfragen reagiert. DNS-Antworten können basierend auf Client-IP-Adresse (Standort), des Tages sowie einige andere Parameter. DNS-Richtlinien können Standortbestimmung DNS, Verwaltung, den Lastenausgleich, Split-Brain-DNS- und andere Szenarien.  
  
-   **Nano Server-Unterstützung für die Datei auf der Basis-DNS-**, können Sie DNS-Server unter Windows Server 2016 auf einem Nano Server-Image bereitstellen. Dieser Bereitstellungsoption steht Ihnen bei Verwendung von dateibasierten DNS. Vom DNS-Server auf einem Nano Server-Image ausführen können Sie die DNS-Server mit reduzierten schnell starten und minimiert das Patchen ausführen.  
  
    > [!NOTE]   
    > Active Directory integrierten DNS wird unter Nano Server nicht unterstützt.  
  
-   **Antwort bewerten einschränkende (RRL)**.  Sie können die Antwort die Begrenzung der Übertragungsrate die DNS-Server aktivieren. Auf diese Weise vermeiden Sie die Möglichkeit, schädliche Systeme, die mithilfe von DNS-Servern zum Initiieren eines Denial-of-Service-Angriff auf einen DNS-Client.  
  
-   **DNS-basierte Authentifizierung von benannten Entitäten (DANE)**.   TLSA (Transport Layer Security-Authentifizierung) Datensätze können Sie Informationen zu DNS-Clients bereitzustellen, die ausstellende Zertifizierungsstelle (CA) ein Zertifikat für Ihren Domänennamen erwarten soll Zustand. Dies verhindert, dass Man-in-the-Middle-Angriffe, in denen eine Person kann den DNS-Cache auf ihrer Website gewonnenen beschädigt, und geben ein Zertifikat, das sie von einer anderen Zertifizierungsstelle ausgestellt.  
  
-   **Unterstützung für unbekannte Datensatz**.   
     Sie können Datensätze hinzufügen, die nicht explizit durch den Windows-DNS-Server mithilfe der Funktion unbekannten Eintrag unterstützt werden.  
  
-   **IPv6-Stammhinweise**.   
     Sie können die systemeigene IPV6 verwenden, Stammhinweise zu unterstützen, um die Auflösung von Internetnamen verwenden die IPV6-Server ausführen.  
  
-   **Verbesserte Unterstützung für Windows PowerShell**.   
      Neue Windows PowerShell-Cmdlets sind für DNS-Server verfügbar.  
  
Weitere Informationen finden Sie unter [What's New in DNS-Server unter Windows Server 2016](dns/What-s-New-in-DNS-Server.md)  
  
## <a name="bkmk_GRE"></a>GRE-Tunneling  
RAS-Gateway unterstützt jetzt Generic Routing Encapsulation (GRE)-Tunnel mit hoher Verfügbarkeit für Standort-zu-Standort-Verbindungen und M + N Redundanz Gateways. GRE ist ein einfaches Tunneling-Protokoll, das eine Vielzahl von Ebene Netzwerkprotokolle in virtuellen Point-Links über eine IP-Internetwork kapseln kann.  
  
Weitere Informationen finden Sie unter [GRE-Tunneling in Windows Server 2016](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md).  
  
## <a name="HNV"></a>Hyper-V-Netzwerkvirtualisierung  
Hyper-V-Netzwerkvirtualisierung (HNV) ermöglicht in Windows Server 2012 eingeführt wurde, die Virtualisierung von Kundennetzwerken auf der Basis einer gemeinsam genutzten physischen Netzwerkinfrastruktur. Mit nur minimalen Änderungen auf dem physischen Netzwerk-Fabric, bietet Hyper-v-Dienstanbieter die Flexibilität, bereitstellen und Migrieren von mandantenworkloads an einer beliebigen Stelle auf die drei Wolken: die Cloud Service Provider, die private Cloud oder der öffentlichen Microsoft Azure-Cloud.  
  
Weitere Informationen finden Sie unter [What's New in Hyper-V-Netzwerkvirtualisierung in Windows Server 2016](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)  
  
## <a name="bkmk_ipam"></a>IPAM  
IPAM bietet äußerst anpassbare Verwaltungs- und Überwachungsfunktionen für die IP-Adresse und DNS-Infrastruktur im Netzwerk einer Organisation. Verwenden von IPAM, können Sie überwachen, überwachen und Verwalten von Servern, auf denen Dynamic Host Configuration-Protokoll (DHCP) und Domain Name System (DNS) ausgeführt werden.  
  
-   **Erweiterte IP-Adressverwaltung**.  
     IPAM-Funktionen werden für Szenarien wie das Behandeln von /32 IPv4 und IPv6-/128 Subnetze und finden kostenlose Subnetze von IP-Adressen und Adressbereiche in einem IP-Adressblock verbessert.  
  
-   **Erweiterte Verwaltung von DNS-Dienst**.  
     IPAM unterstützt die DNS-Ressourceneintrag, Weiterleitung und Verwaltung von DNS-Zone für Domäne Active Directory-integriert und Sicherungsdatei DNS-Server.  
  
-   **Integrierte DNS, DHCP und IP-Adressverwaltung (DDI)**.  
     Mehrere neue Funktionen und integrierte Lifecycle Management Operations aktiviert sind, z. B. alle DNS-Ressourceneinträge, die auf eine IP-Adresse beziehen visualisieren, automatisierten Inventur der IP-Adressen, die auf der Grundlage von DNS-Ressourceneinträgen und IP-Adresse lebenszyklusverwaltung für DNS- und DHCP-Vorgänge.  
  
-   **Unterstützung für mehrere Active Directory-Gesamtstruktur**.  
     Sie können IPAM verwenden, verwalten Sie die DNS- und DHCP-Server von mehreren Active Directory-Gesamtstrukturen, wenn eine bidirektionale Vertrauensstellung zwischen der Gesamtstruktur, auf dem IPAM installiert ist, und die einzelnen der Remotegesamtstrukturen ist.  
  
-   **Windows PowerShell-Unterstützung für Role Based Access Control**.  
     Sie können Windows PowerShell verwenden, zum Festlegen von zugriffsbereichen für IPAM-Objekte.  
  
Weitere Informationen finden Sie unter [What's New in IPAM](technologies/ipam/What-s-New-in-IPAM.md) und [Verwalten von IPAM](technologies/ipam/Manage-IPAM.md).  
  

