---
title: Planen einer Software-Defined Networking-Infrastruktur
description: Dieses Thema enthält Informationen zum Planen der Bereitstellung von Software definierten Netzwerken (SDN).
manager: dougkim
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
ms.date: 08/10/2018
ms.openlocfilehash: e2c125867b461cee9f694849db5c8f61be91211d
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869941"
---
# <a name="plan-a-software-defined-network-infrastructure"></a>Planen einer Software-Defined Networking-Infrastruktur

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Erfahren Sie mehr über die Bereitstellungs Planung für eine Software definierte Netzwerkinfrastruktur, einschließlich der Hardware-und Software Voraussetzungen. 


## <a name="prerequisites"></a>Erforderliche Komponenten
In diesem Thema werden eine Reihe von Hardware-und Software Voraussetzungen beschrieben, einschließlich der folgenden:

-   **Konfigurierte Sicherheitsgruppen, Protokolldatei Speicherorte und dynamische DNS-Registrierung** Sie müssen Ihr Rechenzentrum für die Bereitstellung des Netzwerk Controllers vorbereiten. hierfür sind mindestens ein Computer oder ein virtueller Computer und ein Computer oder ein virtueller Computer erforderlich. Bevor Sie den Netzwerk Controller bereitstellen können, müssen Sie die Sicherheitsgruppen, die Protokolldatei Speicherorte (falls erforderlich) und die dynamische DNS-Registrierung konfigurieren.  Wenn Sie Ihr Rechenzentrum nicht für die Bereitstellung des Netzwerk Controllers vorbereitet haben, finden Sie weitere Informationen unter [Installations-und Vorbereitungs Anforderungen für](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md) die Bereitstellung des Netzwerk Controllers.

-   **Physisches Netzwerk**  Sie benötigen Zugriff auf ihre physischen Netzwerkgeräte, um VLANs, Routing, BGP, Data Center Bridging (ETS) bei Verwendung einer RDMA-Technologie und Data Center Bridging (PFC) zu konfigurieren, wenn Sie eine ROCE-basierte RDMA-Technologie verwenden. In diesem Thema wird die manuelle Switchkonfiguration sowie das BGP-Peering auf Layer-3-Switches/-Routern oder einem virtuellen RRAS-Computer (Routing and Remote Access Server) gezeigt.   

-   **Physische Compute-Hosts**  Diese Hosts führen Hyper-V aus und sind zum Hosten der Sdn-Infrastruktur und der virtuellen Mandanten Computer erforderlich.  Eine bestimmte Netzwerkhardware ist auf diesen Hosts erforderlich, um eine optimale Leistung zu erzielen, die später im Abschnitt " **Netzwerkhardware** " beschrieben wird.  


## <a name="physical-network-and-compute-host-configuration"></a>Konfiguration des physischen Netzwerks und des computehosts

Jeder physische computehost erfordert Netzwerk Konnektivität über mindestens einen Netzwerkadapter, der mit einem physischen Switchport verbunden ist.  Ein Layer-2- [VLAN](https://en.wikipedia.org/wiki/Virtual_LAN) unterstützt Netzwerke, die in mehrere logische Netzwerksegmente aufgeteilt sind. 

>[!TIP]
>Verwenden Sie VLAN 0 für logische Netzwerke im Zugriffsmodus oder als nicht markiert. 

>[!IMPORTANT]
>Software-Defined Networking von Windows Server 2016 unterstützt IPv4-Adressierung für die unter-und Überlagerung. IPv6 wird nicht unterstützt.

### <a name="logical-networks"></a>logische Netzwerke

#### <a name="management-and-hnv-provider"></a>Verwaltungs-und HNV-Anbieter 

Alle physischen computehosts müssen auf das logische Verwaltungs Netzwerk und das logische HNV-anbieternetzwerk zugreifen.  Bei der Planung von IP-Adressen muss jedem physischen computehost mindestens eine IP-Adresse aus dem logischen Verwaltungs Netzwerk zugewiesen werden. Für den Netzwerk Controller ist eine reservierte IP-Adresse erforderlich, die als Rest-IP-Adresse fungiert. 

Ein DHCP-Server kann automatisch IP-Adressen für das Verwaltungs Netzwerk zuweisen, oder Sie können eine statische IP-Adresse manuell zuweisen. Der Sdn-Stapel weist automatisch IP-Adressen für das logische HNV-anbieternetzwerk für die einzelnen Hyper-v-Hosts aus einem IP-Adress Pool zu, der durch angegeben und vom Netzwerk Controller verwaltet wird. 

>[!NOTE]
>Der Netzwerk Controller weist einem physischen computehost eine IP-Adresse für den HNV-Anbieter zu, nachdem der Netzwerk Controller-Host-Agent eine Netzwerk Richtlinie für einen bestimmten virtuellen Mandanten Computer empfangen hat. 


|                                                               Situation                                                               |                                                                                                                                                                          Folge                                                                                                                                                                           |
|-----------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                  In den logischen Netzwerken werden VLANs verwendet,                                                  |                                                                 der physische computehost muss eine Verbindung mit einem abgeverkürzten Switchport herstellen, der Zugriff auf diese VLANs hat. Beachten Sie, dass für die physischen Netzwerkadapter auf dem Computer Host keine VLAN-Filterung aktiviert werden darf.                                                                 |
|                Mithilfe von umschtem Embedded-Team Vorgang (Set) und mehreren NIC-Teammitgliedern (z. b. Netzwerkadaptern)                |                                                                                                                        Sie müssen alle NIC-Teammitglieder für diesen bestimmten Host mit derselben Schicht-2-Broadcast Domäne verbinden.                                                                                                                         |
| Auf dem physischen computehost werden zusätzliche Infrastruktur-VMS ausgeführt, z. b. Netzwerk Controller, SLB/MUX oder Gateway. | dieser Host muss über eine zusätzliche IP-Adresse verfügen, die über das logische Verwaltungs Netzwerk für jeden gehosteten virtuellen Computer zugewiesen ist.<p>Außerdem muss jeder virtuelle Computer der SLB/MUX-Infrastruktur über eine IP-Adresse verfügen, die für das logische HNV-anbieternetzwerk reserviert ist. Wenn eine IP-Adresse nicht reserviert ist, kann dies zu doppelten IP-Adressen in Ihrem Netzwerk führen. |

---

Informationen zu Hyper-v-Netzwerkvirtualisierung (Hyper-v-Netzwerkvirtualisierung), mit der Sie Netzwerke in einer Microsoft Sdn-Bereitstellung virtualisieren können, finden Sie unter [Hyper-v-Netzwerkvirtualisierung](../technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md).  



#### <a name="gateways-and-the-software-load-balancer"></a>Gateways und die Software Load Balancer

Es müssen zusätzliche logische Netzwerke erstellt und für die Gateway-und SLB-Verwendung bereitgestellt werden. Stellen Sie sicher, dass Sie die richtigen IP-Präfixe, VLAN-IDs und Gateway-IP-Adressen für diese Netzwerke erhalten.


|                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **Logisches Transit Netzwerk**   | Das RAS-Gateway und SLB/MUX verwenden das logische Übertragungs Netzwerk, um BGP-peeringinformationen und den Nord/Süd-Mandanten Datenverkehr (externer interner Mandanten) auszutauschen. Die Größe dieses Subnetzes ist normalerweise kleiner als die anderen. Nur physische Compute-Hosts, auf denen RAS-Gateway-oder SLB/MUX-VMS ausgeführt werden, müssen mit diesem Subnetz verbunden sein, wobei diese VLANs abgeschnitten sind und über die Switchports zugänglich sind, mit denen die Netzwerkadapter der computehosts verbunden sind. Jedem virtuellen SLB/MUX-oder RAS-Gateway-Computer wird eine IP-Adresse aus dem logischen Transit Netzwerk zugewiesen. |
| **Logisches Netzwerk mit öffentlicher VIP**  |                                                                                                                             Das logische Netzwerk der öffentlichen VIP muss über IP-Subnetzpräfixe verfügen, die außerhalb der cloudumgebung Routing fähig sind (in der Regel über das Internet Routing fähig).  Dies sind die Front-End-IP-Adressen, die von externen Clients verwendet werden, um auf Ressourcen in den virtuellen Netzwerken zuzugreifen, einschließlich der Front-End-VIP für das Standort-zu-Standort-Gateway.                                                                                                                             |
| **Logisches Netzwerk mit Privater VIP** |                                                                                                                                                                                       Es ist nicht erforderlich, dass das logische Netzwerk für die private VIP außerhalb der Cloud Routing fähig ist, da es für VIPs verwendet wird, auf die nur von internen cloudclients zugegriffen wird, z. b. SLB Mananger oder private Services.                                                                                                                                                                                       |
|   **Logisches GRE-VIP-Netzwerk**   |                                                                                                                                           Das GRE-VIP-Netzwerk ist ein Subnetz, das ausschließlich zum Definieren von VIPs vorhanden ist, die virtuellen gatewaycomputern zugewiesen werden, die in Ihrem Sdn-Fabric für einen S2S GRE-Verbindungstyp ausgeführt werden Dieses Netzwerk muss nicht in ihren physischen Switches oder Router vorkonfiguriert werden, und es muss kein VLAN zugewiesen sein.                                                                                                                                            |

---


#### <a name="sample-network-topology"></a>Beispiel für eine Netzwerktopologie
Ändern Sie die IP-Subnetzpräfixe und VLAN-IDs für Ihre Umgebung. 


| **Netzwerkname** |  **Subnetz**  | **Chel** | **VLAN-ID auf LKW** | **Zugang**  |                                                           **Reservierungen (Beispiele)**                                                           |
|------------------|--------------|----------|----------------------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
|    Management    | 10.184.108.0 |    24    |          7           | 10.184.108.1 | 10.184.108.1 – Router 10.184.108.4-Network Controller 10.184.108.10-Compute Host 110.184.108.11-Compute Host 210.184.108. X-computehost X |
|   HNV-Anbieter   |  10.10.56.0  |    23    |          11          |  10.10.56.1  |                                                    10.10.56.1 – Router 10.10.56.2-SLB/MUX1                                                     |
|     Mitteln      |  "10.10.10.0  |    24    |          10          |  10.10.10.1  |                                                               10.10.10.1 –-Router                                                               |
|    Öffentliche VIP    |  41.40.40.0  |    27    |          Nicht verfügbar          |  41.40.40.1  |                                    41.40.40.1 – Router 41.40.40.2-SLB/MUX VIP 41.40.40.3-IPSec S2S VPN-VIP                                    |
|   Private VIP    |  20.20.20.0  |    27    |          Nicht verfügbar          |  20.20.20.1  |                                                        20.20.20.1-default GW (Router)                                                         |
|     GRE-VIP      |  31.30.30.0  |    24    |          Nicht verfügbar          |  31.30.30.1  |                                                             31.30.30.1-Standard-GW                                                             |

---

### <a name="logical-networks-required-for-rdma-based-storage"></a>Für RDMA-basierten Speicher erforderliche logische Netzwerke  

Wenn Sie RDMA-basierten Speicher verwenden, definieren Sie ein VLAN und Subnetz für jeden physischen Adapter (zwei Adapter pro Knoten) in ihren COMPUTE-und Speicher Hosts.  

>[!IMPORTANT]
>Damit Quality of Service (QoS) ordnungsgemäß angewendet wird, benötigen physische Switches ein markierter VLAN für RDMA-Datenverkehr.

| **Netzwerkname** |  **Subnetz**  | **Chel** | **VLAN-ID auf LKW** | **Zugang**  |                                                           **Reservierungen (Beispiele)**                                                            |
|------------------|--------------|----------|----------------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
|     Storage1     |  10.60.36.0  |    25    |          8           |  10.60.36.1  |  10.60.36.1 –-Router<p>10.60.36. x-computehost X<p>10.60.36. y-computehost Y<p>10.60.36. V-Compute-Cluster<p>10.60.36. W-Speicher Cluster  |
|     Storage2     | 10.60.36.128 |    25    |          9           | 10.60.36.129 | 10.60.36.129 –-Router<p>10.60.36. x-computehost X<p>10.60.36. y-computehost Y<p>10.60.36. V-Compute-Cluster<p>10.60.36. W-Speicher Cluster |

---


## <a name="routing-infrastructure"></a>Routing Infrastruktur  

Wenn Sie die Sdn-Infrastruktur mithilfe von Skripts bereitstellen, müssen die Verwaltungs-, HNV-Anbieter-, Transit-und VIP-Subnetze im physischen Netzwerk Routing fähig sein.     

Routing Informationen \(, z. b.\) der nächste Hop für die VIP-Subnetze, werden von den SLB/MUX-und RAS-Gateways im physischen Netzwerk mithilfe des internen BGP-Peerings angekündigt. Den logischen VIP-Netzwerken ist kein VLAN zugewiesen, und es ist nicht im Layer-2-Switch vorkonfiguriert (z. b. ein Top-of-Rack-Switch).  

Sie müssen einen BGP-Peer auf dem Router erstellen, der von ihrer Sdn-Infrastruktur zum Empfangen von Routen für die von den SLB/muxes und RAS-Gateways angekündigten logischen VIP-Netzwerke verwendet wird. BGP-Peering muss nur unidirektional erfolgen (von SLB/MUX oder RAS-Gateway zum externen BGP-Peer).  Oberhalb der ersten Routing Ebene können Sie statische Routen oder ein anderes dynamisches Routing Protokoll wie z. b. OSPF verwenden. wie bereits erwähnt, muss das IP-Subnetzpräfix für die logischen VIP-Netzwerke jedoch vom physischen Netzwerk an den externen BGP-Peer übertragen werden können.   

BGP-Peering wird in der Regel in einem verwalteten Switch oder Router als Teil der Netzwerkinfrastruktur konfiguriert. Der BGP-Peer kann auch auf einem Windows-Server konfiguriert werden, auf dem die RAS-Rolle (Remote Access Server) in einem reinen Routing Modus installiert ist. Dieser BGP-routerpeer in der Netzwerkinfrastruktur muss so konfiguriert sein, dass er über eine eigene ASN verfügt und das Peering von einer ASN zulässt, \(die den SLB/MUX-\)und RAS-Gateways der Sdn-Komponenten zugewiesen ist. Sie müssen die folgenden Informationen von Ihrem physischen Router oder vom Netzwerkadministrator zur Steuerung dieses Routers abrufen:

- Routerasn  
- IP-Adresse des Routers  
- ASN für die Verwendung durch Sdn-Komponenten (kann beliebig viele aus dem privaten ASN-Bereich sein)

>[!NOTE]
>Vier Byte-ASNS werden von SLB/MUX nicht unterstützt. Sie müssen den SLB/MUX-und dem Router, an dem die Verbindung hergestellt wird, zwei Byte-ASNS zuordnen. Sie können vier Byte-ASNS an anderer Stelle in Ihrer Umgebung verwenden.  

Sie oder Ihr Netzwerkadministrator müssen den BGP-routerpeer so konfigurieren, dass Verbindungen von der ASN und der IP-Adresse oder Subnetzadresse des logischen Transit Netzwerks, das von Ihrem RAS-Gateway und von SLB/muxes verwendet wird, angenommen werden.

Weitere Informationen finden Sie unter [Border Gateway Protocol (BGP)](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md).

## <a name="default-gateways"></a>Standard Gateways
Für Computer, die zum Herstellen einer Verbindung mit mehreren Netzwerken konfiguriert sind, z. b. die physischen Hosts und die virtuellen Gatewaycomputer, muss nur ein Standard Gateway konfiguriert sein Konfigurieren Sie das Standard Gateway auf dem Adapter, der zum Erreichen des Internets verwendet wird.

Befolgen Sie für virtuelle Computer die folgenden Regeln, um zu entscheiden, welches Netzwerk als Standard Gateway verwendet werden soll:

1. Verwenden Sie das logische Übertragungs Netzwerk als Standard Gateway, wenn eine virtuelle Maschine mit dem Transit Netzwerk verbunden ist, oder wenn Sie mit dem Transit Netzwerk oder einem anderen Netzwerk mehrfach vernetzt ist.
2. Verwenden Sie das Verwaltungs Netzwerk als Standard Gateway, wenn ein virtueller Computer nur eine Verbindung mit dem Verwaltungs Netzwerk herstellt. 
3. Verwenden Sie das HNV-anbieternetzwerk für SLB/muxes und RAS-Gateways. Verwenden Sie das HNV-anbieternetzwerk nicht als Standard Gateway. 
4. Verbinden Sie virtuelle Computer nicht direkt mit den Netzwerken Storage1, Storage2, Public VIP oder private VIP.

Verwenden Sie für Hyper-V-Hosts und Speicher Knoten das Verwaltungs Netzwerk als Standard Gateway.  Den Speicher Netzwerken darf nie ein Standard Gateway zugewiesen sein.


## <a name="network-hardware"></a>Netzwerkhardware

In den folgenden Abschnitten finden Sie Informationen zum Planen der Bereitstellung von Netzwerkhardware.

### <a name="network-interface-cards-nics"></a>Netzwerkschnittstellenkarten (NICs)

Die Netzwerkschnittstellenkarten (NICs), die auf Ihren Hyper-V-Hosts und Speicher Hosts verwendet werden, erfordern bestimmte Funktionen, um die beste Leistung zu erzielen. 

Der Remote Zugriff auf den direkten Speicher (Remote Direct Memory Access, RDMA) ist eine Kernel Umgehungs Technik, mit der große Datenmengen ohne Verwendung der Host-CPU übertragen werden können. Dadurch wird die CPU zur Durchführung anderer Aufgaben freigegeben. 

Switch Embedded Teaming (Set) ist eine Alternative NIC-Team Vorgangs Lösung, die Sie in Umgebungen verwenden können, die Hyper-V und den Sdn-Stapel (Software Defined Networking) in Windows Server 2016 enthalten. Set integriert einige NIC-Team Vorgangs Funktionen in den virtuellen Hyper-V-Switch. 

Weitere Informationen finden Sie unter [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](../../../virtualization//hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).   

Um den mehr Aufwand für den Datenverkehr des virtuellen Mandanten Netzwerks zu berücksichtigen, der durch vxlan-oder nvgre-Kapselungs Header verursacht wird, muss die MTU des Layer-2-Fabric-Netzwerks (Switches und Hosts \() größer oder gleich 1674 bytes, einschließlich Layer-2-Ethernet, festgelegt werden. Header\). 

NICs, die das neue Schlüsselwort " *encapoverhead* Advanced Adapter" unterstützen, legt die MTU automatisch über den Netzwerk Controller-Host-Agent fest. NICs, die das neue *encapoverhead* -Schlüsselwort nicht unterstützen, müssen die MTU-Größe manuell auf jedem physischen Host mithilfe des Schlüssel Worts "\) *jumbopacket* \(" oder "äquivalente" festlegen. 


### <a name="switches"></a>Mikro

Wenn Sie einen physischen Switch und Router für Ihre Umgebung auswählen, stellen Sie sicher, dass er die folgenden Funktionen unterstützt:  

- Switchport-MTU \(-Einstellungen erforderlich\)  
- MTU auf > = 1674 Bytes \(einschließlich L2-Ethernet-Header festgelegt\)  
- L3- \(Protokolle erforderlich\)  
- ECMP  
- BGP \(IETF RFC 4271\)\--basiertes ECMP

Implementierungen sollten die-Anweisungen in den folgenden IETF-Standards unterstützen.

- RFC 2545: "BGP-4-multiprotokollerweiterungen für IPv6-Domänen übergreifendes Routing"  
- RFC 4760: "MultiProtocol-Erweiterungen für BGP-4"  
- RFC 4893: "BGP-Unterstützung für vier Oktett als Zahlenbereich"  
- RFC 4456: "BGP-Routen Reflektion: Eine Alternative zum vollständigen Mesh Internal BGP (IBGP)  
- RFC 4724: "Ordnungsgemäßer Neustart Mechanismus für BGP"  

Die folgenden taggingprotokolle sind erforderlich.

- VLAN-Isolation verschiedener Arten von Datenverkehr
- 802.1 q-trunk

Die folgenden Elemente stellen ein Link Steuerelement bereit.

- Quality of Service \(PFC ist nur erforderlich, wenn ROCE verwendet wird.\)
- Erweiterte Datenverkehrs \(Auswahl 802.1 QAZ\)
- Prioritäts basierte Fluss \(Steuerung 802.1 p/Q und 802.1 qbb\)

Die folgenden Elemente bieten Verfügbarkeit und Redundanz.

- Wechsel Verfügbarkeit (erforderlich)
- Ein hochverfügbarer Router ist erforderlich, um Gatewayfunktionen auszuführen. Hierfür können Sie einen Multichassis-Switch \ Router oder Technologien wie VRRP verwenden.

Die folgenden Elemente bieten Verwaltungsfunktionen.

**Chtungs**

- SNMP v1 oder SNMP v2 (erforderlich, wenn Netzwerk Controller für die Überwachung physischer Switches verwendet wird)  
- SNMP-MIB \(ist erforderlich, wenn Sie den Netzwerk Controller für die Überwachung physischer Switches verwenden.\)  
- MIB-II (RFC 1213), LLDP, Interface MIB \(RFC 2863\), if-MIB, IP-MIB, IP-Forward-MIB, Q-Bridge-MIB, Bridge-MIB, lldb-MIB, Entity-MIB, IEEE8023-lag-MIB  

Die folgenden Diagramme zeigen eine Beispiel Einrichtung mit vier Knoten. Aus Gründen der Übersichtlichkeit zeigt das erste Diagramm nur den Netzwerk Controller an, das zweite zeigt den Netzwerk Controller und den Software Lastenausgleich, und das dritte Diagramm zeigt den Netzwerk Controller, den Software Lastenausgleich und das Gateway.  

In diesen Diagrammen werden keine Speicher Netzwerke und vNICs angezeigt. Wenn Sie beabsichtigen, SMB-basierten Speicher zu verwenden, sind diese erforderlich.

Sowohl die Infrastruktur als auch die virtuellen Mandanten Computer können auf jeden physischen computehost verteilt werden (vorausgesetzt, die richtige Netzwerk Konnektivität ist für die richtigen logischen Netzwerke vorhanden).  



## <a name="switch-configuration-examples"></a>Switchkonfigurationsbeispiele  

Zur Unterstützung der Konfiguration des physischen Switchs oder Routers steht eine Reihe von Beispiel Konfigurationsdateien für eine Vielzahl von Switchmodellen und Anbietern im [Microsoft Sdn GitHub-Repository](https://github.com/microsoft/SDN/tree/master/SwitchConfigExamples)zur Verfügung. Eine ausführliche und getestete Befehlszeilenschnittstelle (Command Line Interface, CLI)-Befehle für bestimmte Switches werden bereitgestellt.         


## <a name="compute"></a>Compute  
Auf allen Hyper-v-Hosts muss Windows Server 2016 installiert sein, Hyper-v aktiviert und ein externer virtueller Hyper-v-Switch, der mit mindestens einem physischen Adapter erstellt wurde, der mit dem logischen Verwaltungs Netzwerk verbunden ist. Der Host muss über eine der Verwaltungs Host-vNIC zugewiesene Verwaltungs-IP-Adresse erreichbar sein.  

Jeder Speichertyp, der mit Hyper-V, Shared oder local kompatibel ist, kann verwendet werden.   

> [!TIP]  
> Es ist praktisch, wenn Sie für alle virtuellen Switches denselben Namen verwenden, aber dies ist nicht zwingend erforderlich. Wenn Sie die Bereitstellung mit Skripts planen, sehen Sie sich den `vSwitchName` mit der Variablen in der Datei config. psd1 verknüpften Kommentar an.  

**Hostcomputeanforderungen**  
In der folgenden Tabelle werden die Mindestanforderungen an die Hardware und Software für die vier physischen Hosts, die in der Beispiel Bereitstellung verwendet werden, angezeigt.  

Host|Hardwareanforderungen|Softwareanforderungen|  
--------|-------------------------|-------------------------  
|Physischer Hyper-v-Host|4-Kern-CPU mit 2,66 GHz<br /><br />32 GB RAM<br /><br />300 GB Speicherplatz<br /><br />1 GB/s (oder schneller) physischer Netzwerkadapter|VULKANE Windows Server 2016<br /><br />Hyper-V-Rolle installiert|  


**Rollenanforderungen für virtuelle Computer in der Sdn-Infrastruktur**  

Rolle|vCPU-Anforderungen|Arbeitsspeicheranforderungen|Datenträgeranforderungen|  
--------|---------------------|-----------------------|---------------------  
|Netzwerk Controller (drei Knoten)|4 vCPUs|4 GB min. (8 GB empfohlen)|75 GB für das Betriebssystem Laufwerk  
|SLB/Mux (drei Knoten)|8 vCPUs|8 GB empfohlen|75 GB für das Betriebssystem Laufwerk  
|RAS-Gateway<br /><br />(einzelner Pool von drei Knoten Gateways, zwei aktiv, ein passiv)|8 vCPUs|8 GB empfohlen|75 GB für das Betriebssystem Laufwerk  
|RAS-Gateway-BGP-Router für SLB/MUX-Peering<br /><br />(Alternativ können Sie den Tor-Switch als BGP-Router verwenden)|2 vCPUs|2 GB|75 GB für das Betriebssystem Laufwerk|  


Wenn Sie VMM für die Bereitstellung verwenden, sind zusätzliche Infrastruktur Ressourcen für virtuelle Maschinen für VMM und andere nicht-Sdn-Infrastrukturen erforderlich. Weitere Informationen finden Sie unter [Minimal Hardware Empfehlungen für System Center Technical Preview.](https://technet.microsoft.com/library/dn997303.aspx)  

## <a name="extending-your-infrastructure"></a>Erweitern der Infrastruktur  
Die Größenanpassung und Ressourcenanforderungen für Ihre Infrastruktur sind abhängig von den virtuellen Computern der Mandanten Arbeitsauslastung, die Sie hosten möchten. Die CPU-, Arbeitsspeicher-und Datenträger Anforderungen für die virtuellen Computer der Infrastruktur (z. b. Netzwerk Controller, SLB, Gateway usw.) werden in der vorherigen Tabelle aufgelistet. Sie können weitere dieser Infrastruktur-VMS hinzufügen, um nach Bedarf horizontal hochskalieren zu können. Alle auf den Hyper-V-Hosts laufenden virtuellen Mandanten Computer verfügen jedoch über eigene CPU-, Arbeitsspeicher-und Datenträger Anforderungen, die Sie beachten müssen.   

Wenn die virtuellen Computer der Mandanten Arbeitsauslastung zu viele Ressourcen auf den physischen Hyper-V-Hosts belegen, können Sie Ihre Infrastruktur erweitern, indem Sie zusätzliche physische Hosts hinzufügen. Dies kann mit Virtual Machine Manager oder mithilfe von PowerShell-Skripts (abhängig von der anfänglichen Bereitstellung der Infrastruktur) erfolgen, um neue Server Ressourcen über den Netzwerk Controller zu erstellen. Wenn Sie zusätzliche IP-Adressen für das HNV-anbieternetzwerk hinzufügen müssen, können Sie neue logische Subnetze (mit den entsprechenden IP-Pools) erstellen, die die Hosts verwenden können.  


## <a name="see-also"></a>Siehe auch  
[Installations-und Vorbereitungs Anforderungen für die Bereitstellung des Netzwerk Controllers](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
[SDN des &#40;Software-Defined Networking&#41;](../Software-Defined-Networking--SDN-.md)  



