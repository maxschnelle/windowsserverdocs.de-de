---
title: Planen einer Software-Defined Networking-Infrastruktur
description: Dieses Thema enthält Informationen zum Planen der infrastrukturbereitstellung (Software Defined Network, SDN).
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
ms.openlocfilehash: e3f7f2b6e2f815ec1924b4d476d5e3fd3ab181ec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821061"
---
# <a name="plan-a-software-defined-network-infrastructure"></a>Planen einer Software-Defined Networking-Infrastruktur

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Informationen Sie zu planen der Bereitstellung für eine Software-Defined Networking-Infrastruktur, einschließlich der Hardware- und softwarevoraussetzungen. 


## <a name="prerequisites"></a>Vorraussetzungen
Dieses Thema beschreibt eine Reihe von Voraussetzungen von Hardware und Software, einschließlich:

-   **Konfiguriert die Sicherheitsgruppen, Speicherorten von Protokolldateien und dynamische DNS-Registrierung** müssen Sie Ihr Rechenzentrum vorbereiten, für die Bereitstellung des Netzwerkcontrollers, die einen oder mehrere Computer oder virtuelle Computer und einen Computer oder virtuellen Computer erforderlich ist. Bevor Sie den Netzwerkcontroller bereitstellen können, müssen Sie die Sicherheitsgruppen, die Speicherorte der Protokolldateien (falls erforderlich) und die dynamische DNS-Registrierung konfigurieren.  Wenn Sie Ihr Rechenzentrum nicht für die Bereitstellung des Netzwerkcontrollers vorbereitet haben, finden Sie unter [Installation und Anforderungen bei der Vorbereitung für die Bereitstellung des Netzwerkcontrollers](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md) Details.

-   **Physischen Netzwerk** benötigen Sie Zugriff auf Ihren physischen Netzwerkgeräten zum Konfigurieren von VLANs, Routing, BGP, Data Center Bridging (ETS), wenn eine RDMA-Technologie verwenden, und Data Center Bridging (PCF) bei Verwendung einer RoCE basierte RDMA-Technologie. In diesem Thema wird das manuelle Netzwerkswitch-Konfiguration sowie das BGP-Peering auf Layer-3 Switches / Router oder einen Routing- und RAS-Server (RRAS) virtuellen Computer.   

-   **Physische rechen-Hosts** diese Hosts, Hyper-V ausführen und sind erforderlich, um SDN-Infrastruktur und Mandanten virtuelle Computer gehostet.  Bestimmte Netzwerkhardware ist erforderlich, auf diesen Hosts für eine optimale Leistung, die in einem späteren Zeitpunkt beschrieben wird die **Netzwerkhardware** Abschnitt.  
      
  
## <a name="physical-network-and-compute-host-configuration"></a>Physische Netzwerk- und Compute-Hostkonfiguration

Jede physische computehost sind Netzwerkverbindungen über eine oder mehrere Netzwerkadapter auf einem physischen Switch-Ports erforderlich.  Ein Layer-2 [VLAN](https://en.wikipedia.org/wiki/Virtual_LAN) unterstützt Netzwerke, die in mehrere logische Netzwerksegmente unterteilt. 

>[!TIP]
>VLAN 0 für logische Netzwerke im Zugriffsmodus verwenden oder nicht gekennzeichnet. 

>[!IMPORTANT]
>IPv4-Adressierung für die dabei und die Überlagerung Defined Networking mit Windows Server 2016-Software unterstützt werden. IPv6 wird nicht unterstützt.
  
### <a name="logical-networks"></a>Logische Netzwerke

#### <a name="management-and-hnv-provider"></a>Verwaltungs- und hnv-Anbieternetzwerk 

Alle physischen computeressourcen Hosts müssen es sich um das logische Verwaltungsnetzwerk und das logische hnv-anbieternetzwerk zugreifen.  Für Planungszwecke IP-Adresse muss jede physische computehost mindestens eine IP-Adresse aus dem logischen Verwaltungsnetzwerk zugewiesen haben. Die Netzwerkcontroller ist erforderlich, eine reservierte IP-Adresse als der REST-IP-Adresse verwendet werden. 

Ein DHCP-Server kann IP-Adressen für das Verwaltungsnetzwerk automatisch zuweisen, oder Sie können statische IP-Adresse manuell zuweisen. SDN-Stapel weist automatisch IP-Adressen für das HNV-Anbieternetzwerk logisches Netzwerk für die einzelnen Hyper-V-Hosts aus einem IP-Adresspool angegeben und verwaltet durch den Netzwerkcontroller. 

>[!NOTE]
>Der Netzwerkcontroller weist hnv-Anbieter-IP-Adresse zu einer physischen computehost, erst nach der Netzwerk-Controller-Host-Agent die Netzwerkrichtlinie für einen bestimmten Mandanten virtuelle Computer erhält. 


|Situation  |Folge  |
|---------|---------|
|Die logischen Netzwerke verwenden, VLANs,     |die physischen computehost muss mit einem einen Trunk bilden Switchport verbinden, das Zugriff auf diese VLANs hat. Es ist wichtig zu beachten, dass die physischen Netzwerkadapter auf dem Computerhost keine müssen eine VLAN-Filterung aktiviert.          |
|Switched-Embedded Teaming (SET) und mehreren NIC-Teammitgliedern, wie z. B. Netzwerkadapter     |Sie müssen alle NIC-Team-Mitglieder für den bestimmten Host der gleichen Schicht-2-broadcast-Domäne verbinden.         |
|Der physische computehost, die zusätzlichen virtuellen Computern der Infrastruktur, z. B. dem Netzwerkcontroller, SLB/MUX-Instanz oder Gateway ausgeführt wird,  |Dieser Host muss es sich um eine zusätzliche IP-Adresse aus dem logischen Verwaltungsnetzwerk zugewiesen wird, für die einzelnen gehosteten virtuellen Computer verfügen.<p>Jede VM der SLB/MUX-Infrastruktur muss auch eine IP-Adresse für das logische hnv-anbieternetzwerk reserviert haben. Doppelte IP-Adressen in Ihrem Netzwerk möglicherweise Fehler um eine reservierte IP-Adresse zu erhalten.  |
---

Informationen zu Hyper-V-Netzwerk Netzwerkvirtualisierung (HNV), die Sie auf die Virtualisierung von Netzwerken in einer Microsoft-SDN-Bereitstellung verwenden können, finden Sie unter [Hyper-V-Netzwerkvirtualisierung](../technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md).  
  

  
#### <a name="gateways-and-the-software-load-balancer"></a>Gateways und des Software Load Balancer
  
Zusätzlicher logische Netzwerke erstellt und für das Gateway und Verwendung von SLB bereitgestellt werden müssen. Stellen Sie sicher, dass die richtige IP-Adresspräfixe, VLAN-IDs und Gateway-IP-Adressen für diese Netzwerke zu erhalten.


|  |  |
|---------|---------|
|**Logische Transitnetzwerk**     |Die RAS-Gateway und die SLB/MUX-Instanz verwenden das logische Transitnetzwerk zum Austauschen von BGP-peeringinformationen und (externen intern) Nord/Süd-mandantendatenverkehr ein. Die Größe des diesem Subnetz werden in der Regel kleiner als die anderen. Nur physische Compute-Hosts, auf denen RAS-Gateway oder SLB/MUX-VM ausgeführt werden müssen auf die Switch-Ports eine Verbindung mit diesem Subnetz mit diesen VLANs, die einen Trunk bilden und zugänglich kann mit dem Netzwerkadapter für die Compute-Hosts verbunden sind. Jede SLB/MUX-Instanz oder RAS-Gateway-VM wird eine IP-Adresse statisch aus das logische Transitnetzwerk zugewiesen werden.         |
|**Logisches Netzwerk mit öffentlicher VIP**     |Das logische Netzwerk mit öffentlicher VIP ist erforderlich, um IP-Subnetzpräfixe erhalten, die außerhalb der Cloud-Umgebung (in der Regel Internet routingfähige) geroutet werden.  Dieser werden die Front-End-IP-Adressen, die von externen Clients den Zugriff auf Ressourcen in den virtuellen Netzwerken, einschließlich der Front-End-VIP-Adresse für das Standort-zu-Standort-Gateway verwendet.         |
|**Logisches Netzwerk mit privater VIP**     |Das logische Netzwerk mit privater VIP ist nicht erforderlich, um außerhalb der Cloud über Router weitergeleitet werden, da es für VIPs verwendet wird, die nur über interne Cloud-Clients, z. B. die SLB-Manager oder den privaten Dienste zugegriffen werden.         |
|**Logisches GRE-VIP-Netzwerk**     |Das GRE-VIP-Netzwerk ist ein Subnetz, das nur zum Definieren von VIPs, die für eine S2S-GRE-Verbindungstyp Ihre SDN-Fabric laufenden Gateway-VMs zugewiesen sind. Dieses Netzwerk nicht vorab in den physischen Switches oder Router konfiguriert werden müssen und müssen nicht VLAN zugewiesen sein.            |
---


#### <a name="sample-network-topology"></a>Beispiel-Netzwerktopologie
Ändern Sie die Präfixe von Beispiel-IP-Subnetz und VLAN-IDs für Ihre Umgebung an. 

| **Netzwerkname** | **Subnetz** | **Maske** | **VLAN-ID auf LKW** | **Gateway** | **Reservierungen (Beispiele)** |
| --- | --- | --- | --- | --- | --- |
| Management | 10.184.108.0 | 24 | 7 | 10.184.108.1 | 10.184.108.1 – Router10.184.108.4 - Netzwerk Controller10.184.108.10 - computehost 110.184.108.11 - Computeressourcen hosten 210.184.108.X - computehost X |
| Hnv-Anbieternetzwerk | 10.10.56.0 | 23 | 11 | 10.10.56.1 | 10.10.56.1 – Router10.10.56.2 - SLB/MUX1   |
| Während der Übertragung | 10.10.10.0 | 24 | 10 | 10.10.10.1 | 10.10.10.1 – router |
| Öffentliche VIP-Adresse | 41.40.40.0 | 27 | Nicht verfügbar | 41.40.40.1 | 41.40.40.1 – Router41.40.40.2 VIP41.40.40.3 SLB/MUX - IPSec-S2S-VPN-VIP   |
| Private VIP-Adresse | 20.20.20.0 | 27 | Nicht verfügbar | 20.20.20.1 | 20.20.20.1 - Standard-Gateways (Router)   |
| GRE-VIP | 31.30.30.0 | 24 | Nicht verfügbar | 31.30.30.1 | 31.30.30.1 - Standard-GW |
---
  
### <a name="logical-networks-required-for-rdma-based-storage"></a>Logische Netzwerke, die für RDMA-basierten Speicher erforderlich sind  
  
Wenn Sie RDMA-basierten Speicher verwenden zu können, definieren Sie ein VLAN und ein Subnetz für jeden physischen Adapter (zwei Adapter pro Knoten) auf den Hosts Ihrer COMPUTE- und Speicherressourcen.  

>[!IMPORTANT]
>Für Quality of Service, (QoS) entsprechend angewendet werden erfordert physische Switches markierten VLAN für RDMA-Datenverkehr.

| **Netzwerkname** | **Subnetz** | **Maske** | **VLAN-ID auf LKW** | **Gateway** | **Reservierungen (Beispiele)** |
| --- | --- | --- | --- | --- | --- |
| Storage1 | 10.60.36.0 | 25 | 8 | 10.60.36.1 | 10.60.36.1 – router<p>10.60.36.X - computehost X<p>10.60.36.Y - computehost Y<p>10.60.36.V - Compute-cluster<p>10.60.36.W - speichercluster |
| Storage2 | 10.60.36.128 | 25 | 9 | 10.60.36.129 | 10.60.36.129 – router<p>10.60.36.X - computehost X<p>10.60.36.Y - computehost Y<p>10.60.36.V - Compute-cluster<p>10.60.36.W - speichercluster   |
---

 
## <a name="routing-infrastructure"></a>Routing-Infrastruktur  
  
Wenn Sie Ihre SDN-Infrastruktur mithilfe von Skripts bereitstellen, muss die Verwaltung, hnv-Anbieternetzwerk, während der Übertragung und VIP-Adresse der Subnetze miteinander im physischen Netzwerk geroutet.     
  
Routinginformationen \(z. B. nächsten Hop\) für die VIP Subnetze des SLB/MUX-Instanz und der RAS-Gateways, mit dem physischen Netzwerk mithilfe von internen BGP-peering angekündigt wird. Die logischen VIP-Netzwerke müssen sich nicht auf einem VLAN zugewiesen, und es ist nicht vorkonfiguriert, dass in der Schicht-2-Switch (z. B. Tor Switch).  
  
Sie müssen BGP-Peer auf dem Router zu erstellen, die von Ihrer SDN-Infrastruktur verwendet wird, um Routen für die logischen VIP-Netzwerke, die von den SLB/MUX- und den RAS-Gateways angekündigten zu erhalten. BGP-peering muss nur eine Möglichkeit (von SLB/MUX-Instanz oder RAS-Gateways, die externe BGP-Peer) auftreten.  Über die erste Ebene des Routings, Sie können statische Routen oder eine andere dynamisches Routingprotokoll wie z. B. OSPF, allerdings wie zuvor erwähnt, das IP-Subnetz-Präfix für die logischen VIP-Netzwerke müssen aus dem physischen Netzwerk auf die externe BGP-Peers geroutet werden.   
  
BGP-peering wird in der Regel in einen verwalteten Switch oder Router als Teil der Netzwerkinfrastruktur konfiguriert. Der BGP-Peer konnte auch auf einem Windows Server mit der in einem Modus nur Routing-Rolle (Remote Access Server, RAS) konfiguriert werden. Diese BGP-routerpeer in der Netzwerkinfrastruktur muss konfiguriert werden, um eigene ASN und Zulassen des peerings von einem ASN, die der SDN-Komponenten zugewiesen wird \(SLB/MUX-Instanz und RAS-Gateways\). Sie müssen die folgende Informationen aus dem physischen Router oder der Netzwerkadministrator Kontrolle über diese Router abrufen:

- Router-ASN  
- Router-IP-Adresse  
- ASN für die Verwendung von SDN-Komponenten (kann eine beliebige Anzahl AS aus dem private ASN-Bereich sein)

>[!NOTE]
>Vier-Byte-ASNs werden von der SLB/MUX-Instanz nicht unterstützt. Sie müssen die SLB/MUX-Instanz als auch dem Router 2-Byte-ASNs zuordnen wei an der sie eine Verbindung herstellt. Sie können in Ihrer Umgebung an anderer Stelle auf 4-Byte-ASNs verwenden.  
  
Sie oder Ihr Netzwerkadministrator muss zum Akzeptieren von Verbindungen von der ASN und IP-Adresse oder das logische Transitnetzwerk, das das RAS-Gateway und die SLB/MUX-verwenden-Subnetzadresse der BGP-routerpeer konfigurieren.
  
Weitere Informationen finden Sie unter [Border Gateway Protocol (BGP)](../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md).
  
## <a name="default-gateways"></a>Standard-gateways
Computer, die für die Verbindung zu mehreren Netzwerken, z. B. die physische Hosts und Gateway-VMs konfiguriert werden, müssen nur eine Standard-Gateway konfiguriert sein. Konfigurieren Sie das Standardgateway für den Adapter verwendet, um das Internet zu erreichen.

Führen Sie diese Regeln, um zu entscheiden, welches Netzwerk für die Verwendung als Standardgateway für virtuelle Computer:

1. Verwenden Sie das logische Transitnetzwerk als Standardgateway, wenn ein virtuellen Computers mit dem Transitnetzwerk verbunden ist, oder ist er mehrfach vernetzt, das Transitnetzwerk oder einem anderen Netzwerk.
2. Verwenden Sie das Verwaltungsnetzwerk als Standardgateway, wenn eine VM nur mit dem Verwaltungsnetzwerk verbunden. 
3. Verwenden Sie das hnv-anbieternetzwerk für SLB/MUX und RAS-Gateways. Verwenden Sie nicht das hnv-anbieternetzwerk als Standard-Gateway. 
4. Verbinden Sie virtuelle Computer nicht direkt mit den Storage1 Storage2, öffentliche VIP-Adresse oder privaten VIP-Netzwerken.

Verwenden Sie für Hyper-V-Hosts und Speicherknoten das Verwaltungsnetzwerk als Standardgateway ein.  Die Speichernetzwerke müssen nie ein Standardgateway zugewiesen.

  
## <a name="network-hardware"></a>Netzwerkhardware

Sie können in den folgenden Abschnitten verwenden, hardwarebereitstellung planen.

### <a name="network-interface-cards-nics"></a>Netzwerkschnittstellenkarten (NICs)

Der Netzwerkschnittstellenkarten (NICs) verwendet, in der Hyper-V-Hosts und Speicher-Hosts erfordern bestimmte Funktionen, um die bestmögliche Leistung zu erzielen. 

(Remote Direct Memory Access, RDMA) ist ein Kernel umgehen Technik, die es ermöglicht, übertragen große Mengen von Daten ohne Verwendung des Hosts-CPU, die die CPU für andere Aufgaben freigibt. 

Switch Embedded Teaming (SET) ist eine Alternative NIC-Teamvorgang-Lösung, mit denen Sie in Umgebungen, die Hyper-V und den Stapel Software Defined Networking (SDN) in Windows Server 2016 enthalten. SET integriert einige Funktionen mit NIC-Teamvorgang in den virtuellen Hyper-V-Switch. 

Weitere Informationen finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](../../../virtualization//hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).   

Um den Aufwand in virtuellen mandantennetzwerk-Datenverkehr durch VXLAN oder NVGRE-Kapselung-Header verursacht berücksichtigen, die maximale Übertragungseinheit der Schicht-2-Fabric-Netzwerk (Switches und Hosts) muss festgelegt werden auf größer als oder gleich 1674 Bytes \(einschließlich Layer-2-Ethernet Header\). 

Netzwerkkarten, die die Unterstützung der neuen *EncapOverhead* erweiterte Adapter Schlüsselwort legt die maximale Übertragungseinheit automatisch über den Netzwerkcontroller-Host-Agent. NICs, die nicht die neue unterstützen *EncapOverhead* Schlüsselwort müssen manuell festlegen, die MTU-Größe für jeden physischen Host, der mit der *JumboPacket* \(o.ä.\) Schlüsselwort. 


### <a name="switches"></a>Switches
  
Wenn Sie einen physischen Switches und Router für Ihre Umgebung auswählen, stellen Sie sicher, dass sie den folgenden Satz von Funktionen unterstützt:  

- Switchport MTU-Einstellungen \(erforderlich\)  
- Legen Sie die maximale Übertragungseinheit auf > = 1674 Bytes \(einschließlich L2-Ethernet-Headers\)  
- L3-Protokolle \(erforderlich\)  
- ECMP  
- BGP \(IETF RFC 4271\)\-ECMP basierend

Implementierungen sollten die Anweisungen müssen in den folgenden IETF-Standards unterstützen.

- RFC 2545: "BGP-4-Multiprotocol-Erweiterungen für IPv6-Inter-Domain Routing"  
- RFC 4760: "Multiprotokoll-Erweiterungen für die BGP-4"  
- RFC 4893: "BGP-Unterstützung für 4-Oktett-AS-Nummer Speicherplatz"  
- RFC 4456: "Reflektion der BGP-Route: Eine Alternative zum vollständig Vermaschte internes BGP (IBGP)"  
- RFC 4724: "Ordnungsgemäß neu starten-Mechanismus für BGP"  

Die folgenden Tags Protokolle sind erforderlich.

- VLAN - Isolierung der verschiedenen Arten von Datenverkehr
- 802. 1Q "Trunk"

Geben Sie die folgenden Elemente Link-Steuerelement.

- Quality of Service, \(PCF nur erforderlich, wenn Sie RoCE verwenden\)
- Erweitert die Auswahl der Datenverkehr \(802.1Qaz\)
- Prioritätsbasierte flusssteuerung \(802.1 p/Q und 802.1Qbb\)

Geben Sie die folgenden Elemente, Verfügbarkeit und Redundanz.

- Verfügbarkeit des Switchs (erforderlich)
- Ein hoch verfügbarer Router muss Gatewayfunktionen ausführen. Sie erreichen dies, indem Sie einen Multi-Chassis Switch\-Router oder Technologien wie VRRP.
        
Die folgenden Elemente bieten Verwaltungsfunktionen.

**Überwachung**

- SNMP-v1- oder SNMP-v2 (erforderlich bei mithilfe von Netzwerkcontroller für die Überwachung der physischen Switch)  
- SNMP-MIBs \(erforderlich, wenn Sie den Netzwerkcontroller für die Überwachung der physischen Switch verwenden\)  
- MIB-II (RFC 1213) LLDP, Interface MIB \(RFC 2863\), IF-MIB, IP-MIB, IP-Weiterleitung-MIB, Q-BRIDGE-MIB, BRIDGE-MIB, LLDB-MIB, Entity-MIB, IEEE8023-Verzögerung-MIB  
  
Die folgenden Diagramme zeigen ein Beispiel mit vier Knoten Setup. Aus Gründen der Übersichtlichkeit das erste Diagramm zeigt nur die dem Netzwerkcontroller, das zweite zeigt, die dem Netzwerkcontroller und den Software Load Balancer und das dritte Diagramm zeigt, die dem Netzwerkcontroller, softwarelastenausgleich und das Gateway.  
  
Diese Diagramme anzeigen nicht Speichernetzwerke und vNICs. Wenn Sie SMB-basierten Speicher verwenden möchten, müssen diese.
  
Auf jedem physischen computehost (vorausgesetzt, dass die richtigen Netzwerkkonnektivität für die richtigen logischen Netzwerke vorhanden ist), kann die Infrastruktur und die Mandanten-VMs verteilt werden.  
  

  
## <a name="switch-configuration-examples"></a>Beispiele für wechseln  
  
Damit können einen physischen Switch oder Router konfigurieren, ein Satz von Beispielkonfigurationsdateien für eine Vielzahl von Switch-Modelle und Anbietern finden Sie unter den [Microsoft SDN Github-Repository](https://github.com/microsoft/SDN/tree/master/SwitchConfigExamples). Einer detaillierten Infodatei und getestete über die Befehlszeilenschnittstelle (CLI)-Befehle für spezifische Schalter werden bereitgestellt.         
  
  
## <a name="compute"></a>Compute  
Alle Hyper-V-Hosts müssen Windows Server 2016 installiert haben, Hyper-V aktiviert und ein externes virtuelles Switches von Hyper-V erstellt, die mit mindestens einem physischen Netzwerkadapter, die mit dem logischen Verwaltungsnetzwerk verbunden. Der Host muss über eine Verwaltungs-IP-Adresse, die die Verwaltung von Host-vNIC zugewiesen sein.  
  
Jeder Storage-Typ, der mit Hyper-V, freigegebenen oder lokalen kompatibel ist, kann verwendet werden.   
  
> [!TIP]  
> Es ist sinnvoll, wenn Sie den gleichen Namen für alle virtuellen Switches, aber es nicht erforderlich ist. Wenn Sie mit Skripts bereitstellen möchten, finden Sie unter den zugeordneten Kommentar der `vSwitchName` Variable in der Datei config.psd1.  
  
**Host-computeanforderungen**  
Die folgende Tabelle zeigt die Mindestanforderungen für Hardware und Software für die vier physischen Hosts, die in der beispielsbereitstellung verwendet.  
  
Host|Hardwareanforderungen|Softwareanforderungen|  
--------|-------------------------|-------------------------  
|Physischen Hyper-V-host|4-Kern-CPU, 2,66 GHz<br /><br />32 GB RAM<br /><br />300 GB Speicherplatz<br /><br />1 Gbit/s (oder schneller) physischen Netzwerkadapter|OS: Windows Server 2016<br /><br />Hyper-V-Rolle|  
  
  
**SDN-Infrastruktur-Anforderungen für virtuelle Computer-Rolle**  
  
Role-Eigenschaft|vCPU-Anforderungen|Arbeitsspeicheranforderungen|Datenträgeranforderungen|  
--------|---------------------|-----------------------|---------------------  
|Netzwerkcontroller (drei Knoten)|4 vCPUs|4 GB min. (8 GB empfohlen)|75 GB für das Betriebssystemlaufwerk  
|SLB/MUX-Instanz (drei Knoten)|8 vCPUs|8 GB empfohlen|75 GB für das Betriebssystemlaufwerk  
|RAS-Gateway<br /><br />(einzigen Pool von drei Knoten Gateways, zwei aktive, eine passiv)|8 vCPUs|8 GB empfohlen|75 GB für das Betriebssystemlaufwerk  
|RAS-Gateway-BGP-Router für SLB/MUX-peering<br /><br />(Alternativ verwenden Sie ToR-Switch als BGP-Router)|2 vCPUs|2 GB|75 GB für das Betriebssystemlaufwerk|  
  
  
Wenn Sie VMM für die Bereitstellung verwenden, sind zusätzliche Infrastruktur, VM-Ressourcen für VMM und anderen nicht-SDN-Infrastruktur erforderlich. Weitere Informationen finden Sie unter [Minimum Hardware Recommendations for System Center Technical Preview.](https://technet.microsoft.com/library/dn997303.aspx)  
  
## <a name="extending-your-infrastructure"></a>Erweiterung der Infrastruktur  
Die Anforderungen für Ihre Infrastruktur zur größenanpassung und Ressourcen sind abhängig von den Mandanten Workload-VMs, die Sie hosten möchten. Die CPU, Arbeitsspeicher und datenträgeranforderungen für den virtuellen Computern der Infrastruktur (z. B.: SLB-Controller-Netzwerkgateways, usw.) werden in der vorherigen Tabelle aufgeführt. Sie können mehrere dieser Infrastruktur-VMs zu skalieren, je nach Bedarf hinzufügen. Allerdings müssen alle Mandanten virtuelle Maschinen auf Hyper-V-Hosts ihre eigenen CPU, Arbeitsspeicher und datenträgeranforderungen, die Sie berücksichtigen müssen.   
  
Wenn die virtuellen Maschinen des Mandanten Workload beginnen, die zu viele Ressourcen auf den physischen Hyper-V-Hosts zu nutzen, können Sie Ihrer Infrastruktur erweitern, indem zusätzliche physische Hosts hinzufügen. Dies kann erfolgen mit Virtual Machine Manager oder mithilfe von PowerShell-Skripts (je nachdem, wie Sie zunächst die Infrastruktur bereitgestellt) zum Erstellen von neuen Serverressourcen über den Netzwerkcontroller. Wenn Sie das hnv-anbieternetzwerk zusätzliche IP-Adressen hinzufügen möchten, können Sie neue logische Subnetze (mit der entsprechenden IP-Adresspools) erstellen, die die Hosts verwenden können.  
  
  
## <a name="see-also"></a>Siehe auch  
[Installation und Anforderungen bei der Vorbereitung für die Bereitstellung des Netzwerkcontrollers](Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
[Software-Defined Networking &#40;SDN&#41;](../Software-Defined-Networking--SDN-.md)  
  


