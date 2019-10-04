---
title: Was ist neu in Netzwerken
description: Dieses Thema enthält eine Übersicht über neue Features und Technologien für Netzwerke in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: get-started-article
ms.assetid: 08fb7563-d319-48a9-b181-ca0ca3032c18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: da2166d28edda5662797824d9b26ad930f51083c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406755"
---
# <a name="whats-new-in-networking"></a>Was ist neu in Netzwerken

>Gilt für: Windows Server 2016

Im folgenden finden Sie die neuen oder verbesserten Netzwerktechnologien in Windows Server 2016.  
  UPD dieses Thema enthält die folgenden Abschnitte.  
  
-   [Neue Netzwerk Features und-Technologien](#bkmk_features)  
  
-   [Neue Features für zusätzliche Netzwerktechnologien](#bkmk_existing)  
  
## <a name="bkmk_features"></a>Neue Netzwerk Features und-Technologien

Der Netzwerkbetrieb ist ein grundlegender Bestandteil der Plattform für die Software-Defined Datacenter (SDDC), und Windows Server 2016 bietet neue und verbesserte Sdn-Technologien (Software Defined Networking), mit denen Sie zu einer vollständig erkannten SDDC-Lösung für Ihre Organisation wechseln können.  
  
Wenn Sie Netzwerke als softwaredefinierte Ressource verwalten, können Sie die Infrastrukturanforderungen einer Anwendung einmalig beschreiben und dann auswählen, wo die Anwendung ausgeführt wird (lokal oder in der Cloud).  Diese Konsistenz bedeutet, dass Ihre Anwendungen nun einfacher zu skalieren sind, und Sie können Anwendungen nahtlos und überall mit gleichem Vertrauen in Bezug auf Sicherheit, Leistung, Dienst Qualität und Verfügbarkeit ausführen.  
  
Die folgenden Abschnitte enthalten Informationen zu diesen neuen Netzwerk Features und-Technologien.  
  
### <a name="software-defined-networking-infrastructure"></a>Software-Defined Networking-Infrastruktur

Im folgenden finden Sie die neuen oder verbesserten Sdn-Infrastruktur Technologien.  
  
-   **Netzwerk Controller**. Der Netzwerk Controller ist neu in Windows Server 2016 und bietet einen zentralisierten, programmierbaren Automatisierungs Punkt für die Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Daten Center. Mithilfe von Netzwerkcontroller können Sie die Konfiguration der Netzwerkinfrastruktur automatisieren und müssen Netzwerkgeräte und -dienste nicht länger manuell konfigurieren. Weitere Informationen finden Sie unter [Netzwerk Controller](sdn/technologies/network-controller/Network-Controller.md) und Bereitstellen von [Software definierten Netzwerken mithilfe von Skripts](https://technet.microsoft.com/library/mt427380.aspx).  
  
-   **Virtueller Hyper-V-Switch**. Der virtuelle Hyper-v-Switch wird auf Hyper-v-Hosts ausgeführt und ermöglicht die Erstellung verteilter Wechsel und Routing sowie eine mit Microsoft Azure ausgerichtete und kompatible Richtlinien Erzwingungs Ebene. Weitere Informationen finden Sie unter [Hyper-V Virtual Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).  
  
-   **Network Function Virtualization (NFV)** . In den heutigen Software definierten Rechenzentren werden Netzwerkfunktionen, die von Hardware Geräten (z. b. Lasten Ausgleichs Module, Firewalls, Router, Switches usw.) ausgeführt werden, zunehmend als virtuelle Geräte bereitgestellt. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung. Virtuelle Geräte werden schnell neu entwickelt und erstellen einen neuen Markt. Sie generieren weiterhin Interessen und gewinnen Dynamik sowohl bei Virtualisierungsplattformen als auch bei Clouddiensten. Die folgenden NFV-Technologien sind in Windows Server 2016 verfügbar.  
  
    -   **Datacenter Firewall**. Diese verteilte Firewall bietet differenzierte Zugriffs Steuerungs Listen (Access Control Lists, ACLs), mit denen Sie Firewallrichtlinien auf VM-Schnittstellen Ebene oder auf Subnetzebene anwenden können.  
  
        Weitere Informationen finden Sie unter [Übersicht über die Datacenter-Firewall](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).  
  
    -   **RAS-Gateway**. Sie können das RAS-Gateway für das Routing von Datenverkehr zwischen virtuellen Netzwerken und physischen Netzwerken verwenden, einschließlich Site-to-Site-VPN-Verbindungen aus Ihrem cloudrechenzentrum mit den Remote Standorten ihrer Mandanten. Insbesondere können Sie Internetschlüsselaustausch Version 2 (IKEv2) Site-to-Site-VPNs (Virtual Private Networks), L3-VPN (Layer 3) und GRE-Gateways (Generic Routing Kapselung) bereitstellen. Außerdem werden die gatewaypools und die M + N-Redundanz von Gateways jetzt unterstützt. und Border Gateway Protocol (BGP) mit Routen reflektorfunktionen bietet dynamisches Routing zwischen Netzwerken für alle Gatewayszenarien (IKEv2-VPN, GRE-VPN und L3-VPN).  
  
        Weitere Informationen finden Sie unter [Neues beim RAS-Gateway](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) und [RAS-Gateway für Sdn](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md).  
          
    - **Software Load Balancer (SLB) und Netzwerk Adressübersetzung (NAT)** . Das Lasten Ausgleichs Modul "Nord-Süd" und "Ost-West" und "NAT" verbessern den Durchsatz durch Unterstützung von Direct Server Return, mit dem der Netzwerk Lastenausgleich für den Lastenausgleich umgangen werden kann.  
       Weitere Informationen finden Sie unter [Software Lastenausgleich &#40;SLB&#41; für Sdn](sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).  
  
    Weitere Informationen finden Sie unter [netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md).  
  
-   **Standardisierte Protokolle**. Der Netzwerk Controller verwendet Representational State Transfer (Rest) auf der Northbound-Schnittstelle mit JavaScript Object Notation Nutzlasten (JSON). Die Netzwerk Controller-Southbound-Schnittstelle verwendet das Open Vswitch Database Management Protocol (ovsdb).  
  
-   **Flexible Kapselungs Technologien**. Diese Technologien arbeiten auf der Datenebene und unterstützen sowohl vxlan (Virtual Extensible LAN) als auch nvgre (Generic Routing Kapselung) für die Netzwerkvirtualisierung. Weitere Informationen finden Sie unter [GRE tunnelingin Windows Server 2016](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md).  
  
Weitere Informationen zu Sdn finden Sie unter [Software Defined Networking &#40;(SDN&#41;](sdn/software-defined-networking.md)).  
  
### <a name="cloud-scale-fundamentals"></a>Grundlagen der Cloud
 
Die folgenden Grundlagen der Cloud sind jetzt verfügbar.  
  
-   **Konvergierte Netzwerkschnittstellenkarte (Network Interface Card, NIC)** . Die konvergierte NIC ermöglicht Ihnen die Verwendung eines einzelnen Netzwerkadapters für die Verwaltung, RDMA (Remote Direct Memory Access)-aktivierten Speichers und Mandanten Datenverkehr. Dies reduziert die Kapitalausgaben, die den einzelnen Servern in Ihrem Rechenzentrum zugeordnet sind, da Sie weniger Netzwerkadapter benötigen, um unterschiedliche Arten von Datenverkehr pro Server zu verwalten.  
  
-   **Paket direkt**.  Paket Direct bietet einen hohen Durchsatz für den Netzwerk Datenverkehr und eine Paket Verarbeitungs Infrastruktur mit niedriger Latenz.  
  
-   **Switch Embedded Teaming (Set)** .        Set ist eine NIC-Team Vorgangs Lösung, die in den virtuellen Hyper-V-Switch integriert ist. Set ermöglicht das Team Vorgang von bis zu acht physischen NICs in ein einzelnes Set-Team, das die Verfügbarkeit verbessert und Failover bereitstellt. In Windows Server 2016 können Sie Set-Teams erstellen, die auf die Verwendung von Server Message Block (SMB) und RDMA beschränkt sind. Außerdem können Sie Set Teams zum Verteilen von Netzwerk Datenverkehr für die Hyper-V-Netzwerkvirtualisierung verwenden. Weitere Informationen finden Sie unter [Remote Zugriff auf den direkten Speicher &#40;RDMA&#41; und Switch Embedded Teaming &#40;Set&#41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  
  
## <a name="bkmk_existing"></a>Neue Features für zusätzliche Netzwerktechnologien

Dieser Abschnitt enthält Informationen zu neuen Features für vertraute Netzwerktechnologien.
  
## <a name="bkmk_dhcp"></a>KONFIGURIERT  
DHCP ist ein IETF (Internet Engineering Task Force)-Standard, der den Verwaltungsaufwand und die Komplexität beim Konfigurieren von Hosts in einem TCP/IP-basierten Netzwerk, wie z. B. einem privaten Intranet, reduziert. Der DHCP-Serverdienst führt den Konfigurationsprozess für TCP/IP auf DHCP-Clients automatisch durch.  
  
Weitere Informationen finden Sie unter [Neues in DHCP](technologies/dhcp/What-s-New-in-DHCP.md).  
  
## <a name="bkmk_dns"></a>DNS-  
Bei DNS handelt es sich um ein System, das in TCP/IP-Netzwerke zum Benennen von Computern und Netzwerkdiensten verwendet wird. Die DNS-Namensgebung sucht Computer und Dienste über benutzerfreundliche Namen. Wenn ein Benutzer in einer App einen DNS-Namen eingibt, können die DNS-Dienste den Namen in andere dem Namen entsprechende Informationen auflösen, z. B. in eine IP-Adresse.  
  
Im folgenden finden Sie Informationen zum DNS-Client und DNS-Server.  
  
### <a name="bkmk_dnsc"></a>DNS-Client  
Im folgenden finden Sie die neuen oder verbesserten DNS-Client Technologien.  
  
-   **DNS-Client Dienst Bindung**. In Windows 10 bietet der DNS-Client Dienst eine verbesserte Unterstützung für Computer mit mehr als einer Netzwerkschnittstelle.  
  
Weitere Informationen finden Sie unter [What es New in DNS Client in Windows Server 2016](dns/What-s-New-in-DNS-Client.md) .  
  
### <a name="bkmk_dnss"></a>DNS-Server  
Im folgenden finden Sie die neuen oder verbesserten DNS-Server Technologien.  
  
-   **DNS-Richtlinien**  Sie können DNS-Richtlinien konfigurieren, um anzugeben, wie ein DNS-Server auf DNS-Abfragen antwortet. DNS-Antworten können auf der Client-IP-Adresse (Speicherort), der Tageszeit und mehreren anderen Parametern basieren. DNS-Richtlinien ermöglichen standortabhängige DNS, Datenverkehrs Verwaltung, Lastenausgleich, Split-Brain-DNS und andere Szenarien.  
  
-   **Nano Server-Unterstützung für Datei basiertes DNS**: Sie können den DNS-Server in Windows Server 2016 auf einem Nano Server-Image bereitstellen. Diese Bereitstellungs Option steht Ihnen zur Verfügung, wenn Sie Datei basiertes DNS verwenden. Wenn Sie DNS-Server auf einem Nano Server-Image ausführen, können Sie Ihre DNS-Server mit eingeschränktem Speicherbedarf, schnellstarttyp und minimierten Patches ausführen.  
  
    > [!NOTE]   
    > Active Directory integrierter DNS wird auf Nano Server nicht unterstützt.  
  
-   **Antwortraten Begrenzung (RRL)** .  Sie können die Reaktionsraten Begrenzung für Ihre DNS-Server aktivieren. Auf diese Weise können Sie verhindern, dass böswillige Systeme, die Ihre DNS-Server verwenden, einen Denial-of-Service-Angriff auf einen DNS-Client initiieren.  
  
-   **DNS-basierte Authentifizierung von benannten Entitäten (Dane)** .   Sie können die Datensätze von TLSA (Transport Layer Security Authentication) verwenden, um Informationen für DNS-Clients bereitzustellen, die angeben, von welcher Zertifizierungsstelle ein Zertifikat für Ihren Domänen Namen erwartet werden soll. Dadurch werden man-in-the-Middle-Angriffe verhindert, bei denen jemand den DNS-Cache beschädigen könnte, um auf seine eigene Website zu verweisen, und ein Zertifikat bereitstellen, das von einer anderen Zertifizierungsstelle ausgestellt wurde.  
  
-   **Unterstützung für unbekannte Datensätze**.   
     Sie können Datensätze hinzufügen, die vom Windows-DNS-Server nicht explizit unterstützt werden. verwenden Sie dazu die Funktion für unbekannte Einträge  
  
-   **IPv6**-Stamm Hinweise.   
     Mithilfe der systemeigenen IPv6-Stamm Hinweis Unterstützung können Sie die Internet Namensauflösung mithilfe der IPv6-Stamm Server durchführen.  
  
-   **Verbesserte Windows PowerShell-Unterstützung**.   
      Für den DNS-Server sind neue Windows PowerShell-Cmdlets verfügbar.  
  
Weitere Informationen finden Sie unter [What es New in DNS Server in Windows Server 2016](dns/What-s-New-in-DNS-Server.md) .  
  
## <a name="bkmk_GRE"></a>GRE-Tunnelung  
RAS-Gateway unterstützt jetzt allgemeine hoch Verfügbarkeits Tunnel für Site-to-Site-Verbindungen und M + N-Redundanz von Gateways. GRE ist ein einfaches Tunneling-Protokoll, das eine Vielzahl von Protokollen der Vermittlungsschicht in virtuellen Point-to-Point-Links über ein IP-Internetwork kapseln kann.  
  
Weitere Informationen finden Sie unter [GRE tunnelingin Windows Server 2016](../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md).  
  
## <a name="HNV"></a>Hyper-V-Netzwerkvirtualisierung  
Hyper-v Network Virtualization (HNV) wurde in Windows Server 2012 eingeführt und ermöglicht die Virtualisierung von Kunden Netzwerken auf der Grundlage einer gemeinsam genutzten physischen Netzwerkinfrastruktur. Bei minimalen Änderungen, die auf dem physischen netzwerkfabric erforderlich sind, bietet HNV Dienstanbietern die Flexibilität, mandantenworkloads überall in den drei Clouds bereitzustellen und zu migrieren: die Dienstanbieter-Cloud, die Private Cloud oder die Microsoft Azure Public Cloud.  
  
Weitere Informationen finden Sie unter [Neues bei der Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md) .  
  
## <a name="bkmk_ipam"></a>IPAM  
IPAM bietet hochgradig anpassbare Verwaltungs-und Überwachungsfunktionen für die IP-Adresse und die DNS-Infrastruktur in einem Unternehmensnetzwerk. Mithilfe von IPAM können Sie Server überwachen, überwachen und verwalten, auf denen DHCP (Dynamic Host Configuration-Protokoll) und Domain Name System (DNS) ausgeführt werden.  
  
-   **Erweiterte IP-Adressverwaltung**.  
     Die IPAM-Funktionen werden für Szenarien verbessert, wie z. b. das Verarbeiten von IPv4/32-und IPv6/128-Subnetzen und das Auffinden von Subnetzen und Bereichen für freie IP-Adressen in einem  
  
-   **Erweiterte DNS-Dienst Verwaltung**.  
     IPAM unterstützt DNS-Ressourcen Einträge, bedingte Weiterleitungen und DNS-Zonenverwaltung sowohl für in die Domäne eingebundenen Active Directory integrierte als auch für Datei gestützte DNS-Server.  
  
-   **Integrierte DNS-, DHCP-und IP-Adressverwaltung (DDI)** .  
     Es sind mehrere neue Oberflächen und integrierte Lebenszyklus Verwaltungsvorgänge aktiviert, z. b. das Visualisieren aller DNS-Ressourcen Einträge, die sich auf eine IP-Adresse beziehen, die automatisierte Inventur von IP-Adressen auf der Grundlage von DNS-Ressourcen Einträgen und die Lebenszyklus Verwaltung für DNS-und DHCP-Vorgänge.  
  
-   **Unterstützung mehrerer Active Directory**-Gesamtstrukturen.  
     Mit IPAM können Sie die DNS-und DHCP-Server mehrerer Active Directory Gesamtstrukturen verwalten, wenn eine bidirektionale Vertrauensstellung zwischen der Gesamtstruktur vorhanden ist, in der IPAM installiert ist, und den einzelnen Remote Gesamtstrukturen.  
  
-   **Windows PowerShell-Unterstützung für rollenbasierte Access Control**.  
     Sie können Windows PowerShell verwenden, um Zugriffs Bereiche für IPAM-Objekte festzulegen.  
  
Weitere Informationen finden Sie unter [Neues in IPAM](technologies/ipam/What-s-New-in-IPAM.md) und Verwalten von [IPAM](technologies/ipam/Manage-IPAM.md).  
  

