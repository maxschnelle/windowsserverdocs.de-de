---
title: Planen einer Software-Defined Networking-Infrastruktur
description: Dieses Thema enthält Informationen zum Planen der Bereitstellung der Software definierten Netzwerk (SDN)-Infrastruktur.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: virtual-network
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ea7e53c8-11ec-410b-b287-897c7aaafb13
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bb3b9313996637fa5ee7367c538fe04d7cbefea9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="plan-a-software-defined-network-infrastructure"></a>Planen einer Software-Defined Networking-Infrastruktur

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Überprüfen Sie die folgende Informationen ein, um die Software definierten Netzwerk (SDN)-Infrastruktur-Bereitstellung planen. Wenn Sie diese Informationen finden Sie unter [Bereitstellen einer Software-Defined Networking-Infrastruktur](../deploy/Deploy-a-Software-Defined-Network-Infrastructure.md) Informationen zur Bereitstellung.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgende Planung SDN-Inhalt verfügbar.  
>
> - [Installation und Anforderungen an die Vorbereitung für die Bereitstellung von Netzwerkcontroller](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  

Informationen zu Hyper-V-Netzwerkvirtualisierung (HNV), die Sie zum Virtualisieren von Netzwerken in einer Microsoft-SDN-Bereitstellung verwenden können, finden Sie unter [Hyper-V-Netzwerkvirtualisierung](../technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md).  

## <a name="prerequisites"></a>Erforderliche Komponenten
Dieses Thema beschreibt eine Reihe von Hardware- und softwarevoraussetzungen, einschließlich:

-   **Physikalisches Netzwerk**  
    Sie benötigen Zugriff auf Ihre physischen Netzwerkgeräte konfigurieren, wenn eine RDMA-Technologie mit VLANs, Routing, BGP, Data Center Bridging (ETS) und Data Center Bridging (PFC) bei Verwendung einer RoCE RDMA-Technologie basiert. In diesem Thema wird die manuelle Switch-Konfiguration als auch für BGP-Peering Layer-3-Switches / Router oder eine virtuelle Maschine Routing- und RAS-Server (RRAS).   

-   **Physische Compute-Hosts**  
Diese Hosts Hyper-V ausführen und zum Hosten SDN Infrastruktur- und Mandantendatenverkehrs virtueller Computer erforderlich sind.  Bestimmte Netzwerkhardware ist erforderlich, in diese Hosts für eine optimale Leistung, die später in beschrieben wird die **Netzwerkhardware** Abschnitt.  
      
  
## <a name="physical-network-configuration"></a>Physische Netzwerkkonfiguration

Jedes physische Compute-Host muss eine Netzwerkkonnektivität über einen oder mehrere Netzwerkadapter mit einem physischen Switch-Ports verbunden. Das Netzwerk in mehrere logische Netzwerksegmente hinter dem optional eine Schicht-2 getrennt [VLAN](https://en.wikipedia.org/wiki/Virtual_LAN). Die Präfixe für IP-Subnetz und VLAN-IDs, die nachfolgend aufgeführten Beispiele sind, und müssen für Ihre Umgebung basierend auf Richtlinien von Ihrem Netzwerkadministrator angepasst werden. Verwenden Sie Wenn Ihre logischen Netzwerke nicht gekennzeichnet sind oder im Zugriffsmodus VLAN-ID 0 für diese Netzwerke die logische Subnetze in System Center Virtual Machine Manager oder PowerShell-Skript-Konfigurationsdateien konfigurieren.

>[!IMPORTANT]
>Windows Server2016-Software-definierte Netzwerke unterstützt IPv4-Adressierung für die dabei und der Überlagerung. IPv6 wird nicht unterstützt.
  
### <a name="management-and-hnv-provider-logical-networks"></a>Verwaltung und Hyper-v-Provider logische Netzwerke

Alle physische rechen-Hosts müssen Zugriff auf das logische Netzwerk für Verwaltung und das logische Netzwerk von Hyper-v-Anbieter haben. Wenn die logischen Netzwerke VLANs verwenden, müssen die physischen Compute-Hosts an einen Switchport mit Trunk-Leitungen verbunden werden, die Zugriff auf diese VLANs hat. Ebenso müssen die physischen Netzwerkadapter auf dem Host Compute kein VLAN Filterung aktiviert. Wenn Sie Switch-Embedded Teaming (SET) verwenden, haben mehrere NIC-Teammitglieder (d.h. Netzwerkadapter) in Ihre Compute-Hosts müssen Sie alle Mitglieder NIC-Team für den jeweiligen Host derselben Broadcast Schicht-2-Domäne verbinden.  
  
Für Planungszwecke IP-Adresse muss jeden physischen Compute-Host über mindestens eine IP-Adresse aus dem Management logischen Netzwerk zugewiesen haben. Netzwerkcontroller weist genau zwei IP-Adressen automatisch vom logischen Netzwerk Hyper-v-Anbieter. Wenn der physische Compute-Host sind zusätzliche virtuelle Maschinen (z.B. dem Netzwerkcontroller, SLB/MUX oder Gateway) ausgeführt wird müssen dem Host eine zusätzliche IP-Adresse aus dem Management logischen Netzwerk zugewiesen werden, für jede der Infrastruktur virtueller Maschinen gehostet.   
  
Darüber hinaus muss jeder SLB/MUX-Infrastruktur virtuelle Computer eine IP-Adresse in das logische Netzwerk von Hyper-v-Anbieter reserviert haben. 

>[!IMPORTANT]
>Diese SLB/MUX-IP-Adressen müssen von außerhalb des IP-Adresspools zugewiesen werden, die für das logische Netzwerk von Hyper-v-Anbieter konfiguriert ist. Wenn dies nicht der Fall möglicherweise doppelte IP-Adressen im Netzwerk. 

Netzwerkcontroller ist eine reservierte Adresse aus dem Management-Netzwerk und dient als REST-IP-Adresse erforderlich. Sie müssen die HOST-A-Eintrag manuell in DNS für die REST-IP-Adresse erstellen.  
  
Ein DHCP-Server kann automatisch IP-Adressen für das Verwaltungsnetzwerk zuweisen, oder Sie können statische IP-Adresse manuell zuweisen. Die SDN-Stapels weist automatisch IP-Adressen für die Hyper-v-Anbieter für die einzelnen Hyper-V-Hosts aus einem IP-Adresspool über angegeben und vom Netzwerkcontroller verwaltet.   
  
Der fabricadministrator weist statisch die Hyper-v-Anbieter-IP-Adressen, die von der SLB/MUX über PowerShell-Skripts oder VMM verwendet. Netzwerkcontroller einen physischen Compute-Host eine Hyper-v-Anbieter-IP-Adresse zugewiesen, nur, nachdem der Agent-Host-Controller Netzwerkrichtlinie für eine bestimmte Mandanten virtuelle Maschine erhält.  
  
#### <a name="sample-network-topology"></a>Beispiel-Netzwerktopologie

Passen Sie die Subnetzpräfixe, VLAN-IDs und Gateway-IP-Adressen basierend auf Ihren Netzwerkadministrator Richtlinien.  
  
Netzwerkname|Subnetz|Subnetzmaske|VLAN-ID auf "Trunk"|Gateway|Reservierungen<br />(Beispiele)  
----------------|----------|--------|--------------------|-----------|-----------------------------  
|**Verwaltung**|10.184.108.0|24|7|10.184.108.1|10.184.108.1 - router<br /><br />10.184.108.4 - Netzwerkcontroller<br /><br />10.184.108.10 - Compute-Host 1<br /><br />10.184.108.11 - Compute-Host 2<br /><br />10.184.108.X - Compute-Host X  
|**Hyper-v-Anbieter**|10.10.56.0|23|11|10.10.56.1|10.10.56.1 - router<br /><br />10.10.56.2 - SLB/MUX1  
  
### <a name="logical-networks-for-gateways-and-the-software-load-balancer"></a>Logische Netzwerke für Gateways und des Software Load Balancers
  
Zusätzliche logische Netzwerke erstellt und für Remotedesktopgateway und SLB Nutzung bereitgestellt werden müssen. In diesem Fall müssen Sie arbeiten mit Ihren Netzwerkadministrator, um die richtige IP-Adresspräfixe, VLAN-IDs und Gateway-IP-Adressen für diesen Netzwerken zu erhalten.

#### <a name="transit-logical-network"></a>Während der Übertragung logisches Netzwerk
  
Die RAS-Gateway und SLB/MUX verwenden das logische Netzwerk während der Übertragung auf exchange-BGP-Peers Informationen und Nord-Süd (externe intern) Mandantendatenverkehr. Die Größe der diesem Subnetz werden in der Regel kleiner als die anderen. Nur physische Compute-Hosts, auf denen RAS-Gateway oder SLB/MUX-VMs ausführen müssen eine Verbindung zwischen diesem Subnetz mit diesen VLANs mit Trunk-Leitungen und leicht zugänglichen auf die Switch-Ports mit dem Netzwerkadapter die Compute-Hosts verbunden sind. Jedes SLB/MUX oder RAS-Gateway-VM ist eine IP-Adresse statisch aus dem während der Übertragung logischen Netzwerk zugewiesen werden.

#### <a name="public-vip-logical-network"></a>Öffentliche VIP logisches Netzwerk  
  
Das logische Netzwerk von öffentlichen VIP-Adresse ist erforderlich, um die IP-Subnetzpräfixe verfügen, die außerhalb der Cloudumgebung (in der Regel Internet Routingfähigen) Routingfähigen sind.  Diese werden die Front-End-IP-Adressen, die von externen Clients Zugriff auf Ressourcen in den virtuellen Netzwerken, einschließlich der front-End VIP-Adresse für das Standort-zu-Standort-Gateway verwendet werden.

#### <a name="private-vip-logical-network"></a>Private VIP logisches Netzwerk
  
Im privaten VIP logische Netzwerk ist nicht erforderlich, außerhalb der Cloud Router weitergeleitet werden, da sie für VIPs verwendet wird, die nur über interne Cloud-Clients, z.B. die SLB-Manager unter oder privaten Dienste zugegriffen werden.
  
#### <a name="gre-vip-logical-network"></a>GRE-VIP logisches Netzwerk

Das GRE-VIP-Netzwerk ist ein Subnetz, das ausschließlich für die Definition von VIPs, die Gateway-VMs auf Ihre SDN-Fabric für einen S2S GRE-Verbindungstyp zugewiesen sind, vorhanden ist. Dieses Netzwerk nicht bereits in Ihrem physischen Switches oder Router konfiguriert werden müssen und müssen nicht in einem VLAN zugewiesen haben.   

### <a name="sample-network-topology"></a>Beispiel-Netzwerktopologie

Passen Sie die Subnetzpräfixe, VLAN-IDs und Gateway-IP-Adressen basierend auf Ihren Netzwerkadministrator Richtlinien.  
  
Netzwerkname|Subnetz|Subnetzmaske|VLAN-ID auf "Trunk"|Gateway|Reservierungen<br />(Beispiele)  
----------------|----------|--------|--------------------|-----------|-----------------------------  
|**Während der Übertragung**|10.10.10.0|24|10|10.10.10.1|10.10.10.1 - Router  
|**Öffentliche VIP**|41.40.40.0|27|NA|41.40.40.1|41.40.40.1 - Router<br /> 41.40.40.2 - SLB/MUX-VIP<br />41.40.40.3 - IPsec-S2S-VPN-VIP  
|**Private VIP**|20.20.20.0|27|NA|20.20.20.1|20.20.20.1 - Standard-GW (Router)  
|**GRE-VIP**|31.30.30.0|24|NA|31.30.30.1|31.30.30.1 - Standard-GW|  
  
### <a name="logical-networks-required-for-rdma-based-storage"></a>Logische Netzwerke, die für die RDMA-basierter Speicher erforderlich  
  
Wenn Sie sind mit RDMA-basierten Speicher, und Sie müssen ein VLAN und die Subnetzmaske für jeden physischen Adapter berechnungs- und Speicher-Hosts definieren. In der Regel müssen Sie zwei physische Adapter pro Knoten für diese Konfiguration.  
  
> [!IMPORTANT]  
> Die meisten physischen Switches erfordern RDMA-Datenverkehr in einem Tag markierten VLAN in der Reihenfolge für Quality of Service-Einstellungen korrekt übernommen gesendet werden.  Platzieren Sie RDMA-Datenverkehr auf eine nicht markierten VLAN oder auf einem physischen Zugriffsmodus Port nicht.  
  
Netzwerkname  |Subnetz  |Subnetzmaske  |VLAN-ID auf "Trunk"  |Gateway  |Reservierungen<br />(Beispiele)    
---------|---------|---------|---------|---------|---------  
**Storage1**     |    10.60.36.0     | 25        |   8      |  10.60.36.1       |  10.60.36.1 - Router<br />10.60.36.x - Compute-Host x<br />10.60.36.y - Compute-Host y<br />10.60.36.v - Compute-Cluster<br />10.60.36.w - speichercluster  
|**Storage2**|10.60.36.128|25|9|10.60.36.129|10.60.36.129 - Router<br />10.60.36.x - Compute-Host x<br />10.60.36.y - Compute-Host y<br />10.60.36.v - Compute-Cluster<br />10.60.36.w - speichercluster  
  
Weitere Informationen zum Konfigurieren von Switches finden Sie unter der **Konfigurationsbeispiele** Abschnitt.  
  
## <a name="routing-infrastructure"></a>Routing-Infrastruktur  
  
Wenn Sie Ihre SDN-Infrastruktur mithilfe von Skripts bereitstellen, müssen die Verwaltung, Hyper-v-Anbieter, während der Übertragung und VIP Subnetze miteinander im physischen Netzwerk Router weitergeleitet werden.     
  
Die Routinginformationen \ (z.B. weiter-Hop\) für die VIP-Adresse Subnetze vom SLB/MUX und RAS-Gateways in das physische Netzwerk mit internen BGP-Peering angekündigt wird. Die logischen Netzwerke für VIP kein VLAN zugewiesen und ist für die nicht in der Schicht-2-Switch (z.B. Top-of-Rack-Switch).  
  
Sie müssen einen BGP-Peer auf dem Router zu erstellen, die von Ihrer SDN-Infrastruktur verwendet wird, erhalten Sie Routen für die VIP logischen Netzwerke durch die SLB/MUXes und RAS-Gateways angekündigt. BGP-Peering muss nur eine Möglichkeit (von SLB/MUX oder RAS-Gateway an externe BGP-Peer) ausgeführt werden.  Über die erste Ebene von Routing Sie können statische Routen oder einem anderen dynamisches Routingprotokoll z.B. OSPF, jedoch wie bereits erwähnt, das IP-Subnetzpräfix für die VIP logischen Netzwerke müssen an den externen BGP-Peer aus dem physischen Netzwerk über Router weitergeleitet werden.   
  
BGP-Peering wird in der Regel in einem verwalteten Switch oder Router als Teil der Netzwerkinfrastruktur konfiguriert. Der BGP-Peer konnte auch auf einem Windows Server mit installierter Rolle Remote Access Server (RAS) in einem Modus nur Routing konfiguriert werden. Dieser Peer des BGP-Router in der Netzwerkinfrastruktur muss konfiguriert werden, um eine eigene ASN und zulässt, Peering aus einer ASN, die die Komponenten SDN zugewiesen ist \ (SLB/MUX und RAS-Gateways\). Sie müssen die folgende Informationen aus dem physischen Router oder der Netzwerkadministrator Kontrolle über die Router abrufen:

- Router ASN  
- Router-IP-Adresse  
- ASN für die Verwendung von SDN-Komponenten (kann eine beliebige Anzahl AS aus dem privaten ASN-Bereich)

>[!NOTE]
>4-Byte-ASNs werden von der SLB/MUX nicht unterstützt. Sie müssen die SLB/MUX und Router 2-Byte-ASNs zuordnen wo der er eine Verbindung herstellt. Sie können die 4-Byte-ASNs an anderer Stelle in Ihrer Umgebung verwenden.  
  
Konfigurieren den Peer des BGP-Router akzeptiert Verbindungen aus dem ASN und IP-Adresse oder eine Subnetzadresse des während der Übertragung logischen Netzwerks, die Ihre RAS-Gateway und SLB/MUXes verwenden müssen Sie oder Ihr Netzwerkadministrator.
  
Weitere Informationen finden Sie unter [Border Gateway Protocol & 40; BGP & 41;](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md).
  
## <a name="default-gateways"></a>Standard-Gateways

Computer, die Verbindung mit mehreren Netzwerken, z.B. die physische Hosts und Gateway-VMs konfiguriert werden müssen nur ein Standardgateway konfiguriert haben. Das Standardgateway wird in der Regel auf dem Adapter verwendet, um das erreichen ganz auf das Internet konfiguriert werden.

Verwenden Sie die folgenden Regeln für virtuelle Maschinen entscheiden, welches Netzwerk als Standardgateway verwenden:

1. Verwenden Sie das Netzwerk während der Übertragung als Standardgateway, wenn eine virtuelle Maschine mit dem Netzwerk während der Übertragung verbunden ist, oder ist er mehrfach vernetzt der während der Übertragung zu einem anderen Netzwerk.  
2. Verwenden Sie das Verwaltungsnetzwerk als Standardgateway, wenn eine virtuelle Maschine nur mit dem Verwaltungsnetzwerk verbunden ist.  
3.  Die Hyper-v-Anbieter Netzwerk muss nie als Standard-Gateway verwendet werden. Nur mit diesem Netzwerk verbundenen virtuellen Computer werden die SLB/MUXes und RAS-Gateways.  
4.  Virtuelle Computer wird nie direkt an den Storage1, Storage2, VIP öffentlichen oder privaten VIP-Netzwerken verbunden.  
  
Verwenden Sie für Hyper-V-Hosts und Speicherknoten als Standardgateway das Verwaltungsnetzwerk.  Der Speichernetzwerke müssen nie ein Standardgateway zugewiesen haben.
  
## <a name="network-hardware"></a>Netzwerkhardware

In den folgenden Abschnitten können Sie die Netzwerk-Hardware-Bereitstellung planen.

### <a name="network-interface-cards-nics"></a>Netzwerkschnittstellenkarten (NICs)

Um optimale Leistung zu erzielen, werden bestimmte Funktionen in Netzwerkschnittstellenkarten erforderlich, die Sie in der Hyper-V-Hosts und Speicher-Hosts verwenden.  
 
(Remote Direct Memory Access, RDMA) ist ein Kernel umgehen Technik, die große Datenmengen übertragen, ohne die Host-CPU ermöglicht. Da das DMA-Modul auf dem Netzwerkadapter die Übertragung ausgeführt wird, wird die CPU nicht für die speicherbewegung verwendet.  Dadurch wird die CPU anderer Aufgaben freigegeben.  

Switch Embedded Teaming (SET) ist eine Alternative NIC-Teaming-Lösung, die Sie in einer Umgebung verwenden können, die Hyper-V und der Stapel Software Defined Networking (SDN) in Windows Server2016 enthalten. SET integriert einige NIC-Teaming-Funktionen in den virtuellen Hyper-V-Switch.

Weitere Informationen finden Sie unter [Remote Direct Memory Access & 40; RDMA & 41; und Switch Embedded Teaming & 40; SET & 41;](../../../virtualization//hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  

Um den Aufwand in virtuellen mandantennetzwerk-Datenverkehr zurückzuführen sind, VXLAN oder NVGRE-Kapselung-Header zu berücksichtigen, die MTU des Netzwerks Fabric Schicht-2 (Switches und Hosts) größer als oder gleich 1674 Bytes festgelegt werden muss \ (einschließlich Schicht-2-Ethernet-Headers\). Netzwerkkarten, die die neue unterstützen *EncapOverhead* erweiterte Adapter-Schlüsselwort wird die MTU automatisch über den Netzwerk-Controller-Agent-Host festgelegt. Netzwerkkarten, die keine neuen *EncapOverhead* Schlüsselwort müssen die MTU-Größe manuell auf jedem physischen Host mit der *JumboPacket* \(or equivalent\)-Schlüsselwort.

### <a name="switches"></a>Switches
  
Stellen Sie beim Auswählen einer physischen Switches und Router für Ihre Umgebung sicher unterstützt sie den folgenden Satz von Funktionen.  

- Switchport MTU-Einstellungen \(required\)  
- Legen Sie die MTU auf > = 1674 Bytes \ (einschließlich L2-Ethernet-Verkaufskopf\)  
- L3-Protokolle \(required\)  
- ECMP  
- BGP \(IETF RFC 4271\)\-based ECMP

Implementierungen sollte die Anweisungen müssen in den folgenden IETF-Standards unterstützen.

- RFC 2545: "BGP-4 Multiprotokoll-Erweiterungen für IPv6-Inter-Domain Routing"  
- RFC 4760: "Multiprotokoll-Erweiterungen für BGP-4"  
- RFC 4893: "BGP-Unterstützung für vier-Oktett als Zahl Speicherplatz"  
- RFC 4456: "BGP-Routen Reflektion: eine Alternative zur vollständigen Mesh internes BGP (IBGP)"  
- RFC 4724: "Mechanismus für die BGP ordnungsgemäß neu starten"  

Die folgenden Tagging Protokolle sind erforderlich.

- VLAN - Isolation verschiedene Arten von Datenverkehr
- 802. 1Q "Trunk"

Die folgenden Artikel bieten Hyperlink-Steuerelement.

- Quality of Service für \ (PFC nur erforderlich, wenn RoCE\ mit)
- Erweiterte Datenverkehr Auswahl \(802.1Qaz\)
- Priority Based Flow Control \ (802.1 p/Q und 802.1Qbb\)

Die folgenden Artikel bieten Verfügbarkeit und Redundanz.

- Switch-Verfügbarkeit (erforderlich)
- Ein Router mit hoher Verfügbarkeit ist erforderlich, Gatewayfunktionen ausführen. Sie können dazu einen Router mit mehreren Gehäuse Switch\ oder Technologien wie VRRP.
        
Die folgenden Elemente geben Verwaltungsfunktionen.

**Überwachung**

- SNMP-v1 oder SNMP-v2 (erforderlich bei Verwendung von Netzwerk-Controller für die Überwachung von physischen Switch)  
- SNMP-MIBs \ (erforderlich, wenn Sie Netzwerkcontroller zum physischen Switch Sicherheit\ verwenden)  
- MIB-II (RFC 1213), LLDP, MIB-\(RFC 2863\) IF-MIB-IP-MIB, IP-FORWARD-MIB, Q-BRIDGE-MIB, BRIDGE-MIB, LLDB-MIB, Entität-MIB-, IEEE8023-Verzögerung-MIB-Schnittstelle  
  
Das folgende Diagramm zeigt ein Beispiel für die vier Knoten Setup. Aus Gründen der Klarheit die erste Abbildungzeigt den Netzwerk-Controller, das zweite zeigt den Netzwerkcontroller plus des Software Load Balancers und das dritte Diagramm zeigt, Netzwerkcontroller, softwarelastenausgleich und das Gateway.  
  
Speichernetzwerken und vNICs sind nicht in diesen Diagrammen Shonwn. Wenn Sie SMB-basierten Speicher verwenden möchten, sind diese erforderlich.    
  
Die Infrastruktur und die Mandanten virtuelle Computer können auf jedem physischen Compute-Host (vorausgesetzt, dass die richtigen Netzwerkkonnektivität für das richtige logische Netzwerke vorhanden ist) verteilt werden.  
  
### <a name="network-controller-deployment"></a>Bereitstellung von Domänencontrollern

Bevor Sie Netzwerkcontroller bereitstellen, müssen Sie die Installation und softwareanforderungen sowie Konfigurieren von Sicherheitsgruppen und dynamische DNS-Registrierung überprüfen. Weitere Informationen finden Sie unter [Installation und Anforderungen an die Vorbereitung für die Bereitstellung von Netzwerkcontroller](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md).

Die Einrichtung ist mit drei Netzwerkcontroller Knoten konfiguriert, die auf virtuellen Maschinen mit hoher Verfügbarkeit. Auch angezeigt wird, ist zwei Mandanten mit Mandanten 2 virtuelles Netzwerk in zwei virtuelle Subnetze aufgeteilt, eine Webebene und einer Datenbank-Ebene zu simulieren.  

![SDN NC-Planung](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-NC-Planning.png)

### <a name="network-controller-and-software-load-balancer-deployment"></a>Netzwerkcontroller und Software laden Lastenausgleichs-Bereitstellung

Für eine hohe Verfügbarkeit müssen Sie zwei oder mehr SLB/MUX-Knoten vorhanden sind.
   
![SDN NC-Planung](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-SLB-Deployment.png)
  
### <a name="network-controller-software-load-balancer-and-ras-gateway-deployment"></a>Netzwerkcontroller, Softwarelastenausgleich und RAS-Gateway-Bereitstellung

Es gibt drei Gateway-VMs. zwei aktiv sind, und ein redundant.

![SDN NC-Planung](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-GW-Deployment.png)  
  
  
  
Für die Automatisierung TP5-basierte Bereitstellung muss Active Directory verfügbar sind und von diesen Subnetzen aus erreichbar sein. Weitere Informationen zu Active Directory finden Sie unter [Active Directory Domain Services Overview](https://technet.microsoft.com/en-us/library/mt703721.aspx).  
  
>[!IMPORTANT] 
>Wenn Sie mithilfe von VMM bereitstellen, stellen Sie sicher Ihrer Infrastruktur virtuellen Computer (VMM-Server, Active Directory und DNS, SQL Server, usw.) nicht auf jedem der vier Hosts in den Diagrammen gezeigt gehostet werden.  
  
## <a name="switch-configuration-examples"></a>Beispiele für wechseln  
  
Sie können Ihre physischen Switch oder Router konfigurieren, eine Reihe von Beispiel-Konfigurationsdateien für eine Vielzahl von Switch-Modelle und Lieferanten finden Sie unter der [Microsoft-SDN-Github-Repository](https://github.com/microsoft/SDN/tree/master/SwitchConfigExamples). Eine ausführliche Infodatei und getestete über die Befehlszeilenschnittstelle (CLI)-Befehle für spezifische Schalter werden bereitgestellt.         
  
  
## <a name="compute"></a>Compute  
Alle Hyper-V-Hosts müssen Windows Server2016 installiert haben, Hyper-V aktiviert, und ein externer virtueller Switch mit Hyper-V erstellt mit mindestens einem physischen Netzwerkadapter mit dem logischen Management-Netzwerk verbunden. Der Host muss über eine Management-IP-Adresse der Management-Host-vNIC erreichbar sein.  
  
Beliebige Speichertypen, die mit Hyper-V, gemeinsam genutzten oder lokalen kompatibel ist, kann verwendet werden.   
  
> [!TIP]  
> Es ist praktisch, wenn Sie den gleichen Namen für alle virtuellen Switches verwenden, es ist jedoch nicht obligatorisch. Wenn Sie mit Skripts bereitstellen möchten, finden Sie unter den Kommentar der `vSwitchName`in der Datei config.psd1.  
  
**Host Compute-Anforderungen**  
Die folgende Tabelle zeigt die Mindestanforderungen an Hardware und Software für die vier physischen Hosts, die in der beispielbereitstellung verwendet.  
  
Host|Hardwareanforderungen|Anforderungen der Clientsoftware|  
--------|-------------------------|-------------------------  
|Physischen Hyper-V-Host|4-Core-CPU mit 2,66 GHz<br /><br />32GB RAM<br /><br />300GB Speicherplatz<br /><br />1 Gbit/s (oder schneller) physischen Netzwerkadapter|Betriebssystem: Windows Server 2016<br /><br />Hyper-V-Rolle|  
  
  
**Anforderungen für SDN-Infrastruktur VM-Rolle**  
  
Rolle|vCPU-Anforderungen|Speicherbedarf|Datenträgeranforderungen|  
--------|---------------------|-----------------------|---------------------  
|Netzwerkcontroller (drei Knoten)|4 vCPUs|4GB min (8GB empfohlen)|75GB für das Betriebssystem-Laufwerk  
|SLB/MUX (drei Knoten)|8 vCPUs|Empfohlen werden 8GB|75GB für das Betriebssystem-Laufwerk  
|RAS-Gateway<br /><br />(ein einziger Pool von drei Knoten Gateways, zwei aktive, eine passiv)|8 vCPUs|Empfohlen werden 8GB|75GB für das Betriebssystem-Laufwerk  
|RAS-Gateway-BGP-Router für SLB/MUX-Peering<br /><br />(Sie können auch verwenden Sie ToR-Switch als BGP-Router)|2 vCPUs|2GB|75GB für das Betriebssystem-Laufwerk|  
  
  
Wenn Sie VMM für die Bereitstellung verwenden, sind die Ressourcen für zusätzliche Infrastruktur virtueller Maschinen für VMM und anderen Nicht-SDN-Infrastruktur erforderlich. Weitere Informationen finden Sie unter [mindestens Hardwareempfehlungen für System Center Technical Preview.](https://technet.microsoft.com/library/dn997303.aspx)  
  
## <a name="extending-your-infrastructure"></a>Erweiterung der Infrastruktur  
Die Größe und die Ressource Anforderungen für die Infrastruktur hängen die Arbeitslast virtuellen mandantencomputer, die Sie hosten möchten. Die CPU, Arbeitsspeicher und datenträgeranforderungen für die Infrastruktur virtuellen Computer (z.B.: Netzwerk Controller SLB, Gateway usw.) sind in der obigen Tabelle aufgeführt. Sie können diese Infrastruktur virtueller Maschinen nach Bedarf skalieren hinzufügen. Alle Mandanten-VMs unter Hyper-V-Hosts müssen jedoch ihre eigenen CPU, Arbeitsspeicher und datenträgeranforderungen, die Sie berücksichtigen müssen.   
  
Wenn die virtuellen mandantencomputer Arbeitslast zu viele Ressourcen auf dem physischen Hyper-V-Hosts beginnen, können Sie Ihre Infrastruktur erweitern, durch zusätzliche physische Hosts hinzufügen. Dies kann mit Virtual Machine Manager oder mithilfe von PowerShell-Skripts (je nachdem, wie Sie zunächst die Infrastruktur bereitgestellt), neue Serverressourcen über das Netzwerk-Controller zu erstellen. Wenn Sie zusätzliche IP-Adressen für die Hyper-v-Anbieter hinzufügen müssen, können Sie neue logische Subnetze (mit der entsprechenden IP-Adresspools) erstellen, die die Hosts verwenden können.  
  
  
## <a name="see-also"></a>Siehe auch  
[Installation und Anforderungen an die Vorbereitung für die Bereitstellung von Netzwerkcontroller](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
[Software-Defined Networking & #40; SDN & #41;](../Software-Defined-Networking--SDN-.md)  
  


