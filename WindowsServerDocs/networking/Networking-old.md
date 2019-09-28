---
title: Netzwerk
description: Dieses Thema enthält eine Übersicht über die Software Defined Networking- und Netzwerkplattform-Technologien, die in Windows Server 2016 verfügbar sind.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: 05/08/2018
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 1cc30f239f1c4c9107ce0afcfb70647d43384949
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356782"
---
# <a name="networking"></a>Netzwerk

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf „docs.microsoft.com“ an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> Der Netzwerkbetrieb ist ein grundlegender Bestandteil der SDDC \(\) -Plattform für das Software-Defined Datacenter, und Windows Server 2016 bietet neue und\) verbesserte Software-Defined Networking \(-Sdn-Technologien, die Sie bei der Umstellung auf eine vollständig erkannte SDDC-Lösung für Ihre Organisation.

Wenn Sie Netzwerke als softwaredefinierte Ressource verwalten, können Sie die Infrastrukturanforderungen einer Anwendung einmalig beschreiben und dann auswählen, wo die Anwendung ausgeführt wird (lokal oder in der Cloud). 

Diese Konsistenz bedeutet, dass die Anwendungen sich jetzt leichter skalieren und nahtlos überall mit der gleichen Zuverlässigkeit hinsichtlich Sicherheit, Leistung, Dienstqualität und Verfügbarkeit ausführen lassen.

>[!Note]
> Weitere Informationen zum Download von Windows Server finden Sie unter [Windows Server-Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview).

Windows Server 2016 fügt die folgenden neuen Netzwerktechnologien ein:

- Software-Defined Networking: Netzwerkcontroller bietet die Möglichkeit einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum. Mit dem Netzwerk Controller können Sie die netzwerkfunktionsvirtualisierung verwenden, \(um\) virtuelle Computer-VMS \(für den\) Software Lastenausgleich-SLB problemlos bereitzustellen, um den Netzwerk Datenverkehr für Ihre Mandanten zu optimieren. Gateways zum Bereitstellen der Konnektivitätsoptionen, die Sie zwischen Internet-, lokalen und cloudressourcen benötigen. Mithilfe von Netzwerkcontrollern könne Sie zudem Datacenter Firewall auf virtuellen Computern und Hyper-V-Hosts verwalten.

- Netzwerkplattform: Mithilfe der neuen Features für vorhandene Netzwerk Plattformtechnologien können Sie die DNS-Server Antworten mithilfe der DNS-Richtlinie an Abfragen anpassen, eine konvergierte NIC verwenden, die \(den kombinierten\) Remote Zugriff auf den direkten Speicher für RDMA-und Ethernet-Datenverkehr Verwenden Sie Switch Embedded Teaming \(Set\) , um virtuelle Hyper-V-Switches zu erstellen, die mit RDMA-NICs verbunden \(sind,\) und verwenden Sie die IP-Adress Verwaltungs-IPAM, um DNS-Zonen und-Server sowie DHCP-und IP-Adressen

Weitere Informationen finden Sie unter [Von Windows Server unterstützte Netzwerkszenarien](windows-server-supported-networking-scenarios.md).

Die folgenden Abschnitte enthalten Informationen zu den SDN-Technologien und Netzwerkplattformtechnologien.

## <a name="software-defined-networking-technologies"></a>Software-Defined Networking-Technologien

### <a name="software-defined-networking-40sdn41sdnsoftware-defined-networkingmd"></a>[SDN des &#40;Software-Defined Networking&#41;](sdn/software-defined-networking.md)

Dieses Thema enthält Informationen zu den SDN-Technologien, die in Windows Server, System Center und Microsoft Azure bereitgestellt werden.

>[!NOTE]
>Bei Hyper-V-Hosts und virtuellen \(\) Computern, die Sdn-Infrastruktur Server ausführen, wie z. b. Netzwerk Controller und Software Lastenausgleich-Knoten, muss Windows Server 2016 Datacenter Edition installiert werden. Für Hyper-V-Hosts, die nur Mandanten-Arbeits Auslastungs-VMS\-enthalten, die mit Sdn-kontrollierten Netzwerken verbunden sind, können Sie Windows Server 2016 Standard Edition ausführen.

### <a name="deploy-a-software-defined-network-infrastructure-using-scriptssdndeploydeploy-a-software-defined-network-infrastructure-using-scriptsmd"></a>[Bereitstellen einer Software definierten Netzwerkinfrastruktur mithilfe von Skripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
Dieses Handbuch enthält Anweisungen zum Bereitstellen eines Netzwerkcontrollers mit virtuellen Netzwerken und Gateways in einer Testumgebung.

### <a name="network-controllersdntechnologiesnetwork-controllernetwork-controllermd"></a>[Netzwerkcontroller](sdn/technologies/network-controller/Network-Controller.md)

Netzwerkcontroller bietet die Möglichkeit einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum.

### <a name="software-load-balancing-40slb41-for-sdnsdntechnologiesnetwork-function-virtualizationsoftware-load-balancing-for-sdnmd"></a>[Software Lastenausgleich &#40;-&#41; SLB für Sdn](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

Clouddienstanbieter \(-\) CSPs und Unternehmen, die Software-Defined Networking (SDN) in Windows Server 2016 bereitstellen \(, können den Software Lastenausgleich-SLB\) zum gleichmäßigen Verteilen von Mandanten und Mandanten verwenden Netzwerk Datenverkehr von Kunden zwischen virtuellen Netzwerkressourcen. Windows Server-SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen.

### <a name="ras-gateway-for-sdnsdntechnologiesnetwork-function-virtualizationras-gateway-for-sdnmd"></a>[RAS-Gateway für SDN](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

RAS-Gateway, bei dem es sich um einen softwarebasierten, mehr \(Instanzen fähigen\) , Border Gateway Protocol BGP-fähigen Router in Windows Server 2016 handelt, \(ist für\) clouddienstanbieter-CSPs und Unternehmen konzipiert, die hosten mehrere virtuelle Mandanten Netzwerke, die Hyper-V-Netzwerkvirtualisierung verwenden. 

### <a name="network-function-virtualizationsdntechnologiesnetwork-function-virtualizationnetwork-function-virtualizationmd"></a>[Netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

In Software definierten Rechenzentren werden Netzwerkfunktionen, die von Hardware Geräten \(wie Load Balancer, Firewalls, Routern, Switches\) usw. ausgeführt werden, zunehmend als virtuelle Geräte virtualisiert. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung.

### <a name="datacenter-firewall-overviewsdntechnologiesnetwork-function-virtualizationdatacenter-firewall-overviewmd"></a>[Übersicht über Datacenter Firewall](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

Datacenter Firewall ist eine statusbehaftete, mehrinstanzenfähige 5-Tupel-Firewall (Protokoll, Portnummer von Quelle und Ziel sowie IP-Adresse von Quelle und Ziel), die auf der Vermittlungsschicht implementiert ist.

## <a name="bkmk_networking"></a>Netzwerktechnologien

Die folgende Tabelle enthält Links für einige der Netzwerktechnologien in Windows Server 2016.

### <a name="whats-new-in-networkingnetworkingwhat-s-new-in-networkingmd"></a>[Neues bei Netzwerken](../networking/What-s-New-in-Networking.md)

In den folgenden Abschnitten finden Sie neue Netzwerktechnologien und neue Features für vorhandene Technologien in Windows Server 2016.

### <a name="branchcachebranchcachebranchcachemd"></a>[BranchCache](branchcache/BranchCache.md)

BranchCache ist eine Technologie zur WAN \(\) -Bandbreitenoptimierung für Wide Area Network. Um die WAN-Bandbreite zu optimieren, wenn Benutzer auf Inhalte von Remoteservern zugreifen, ruft BranchCache Inhalte von Inhaltsservern in der Hauptniederlassung oder gehosteten Cloudinhaltsservern ab und speichert sie an Filialstandorten zwischen, sodass Clientcomputer in Filialen lokal und nicht über das WAN auf diese Inhalte zugreifen können.

### <a name="core-network-guide-for-windows-server-2016core-network-guidecore-network-guide-windows-servermd"></a>[Handbuch zum Hauptnetzwerk für Windows Server 2016](core-network-guide/core-network-guide-windows-server.md)

Erfahren Sie, wie Sie ein Windows Server-Netzwerk mit dem Handbuch für das Kernnetzwerk bereitstellen und Funktionen zur Netzwerkbereitstellung mit den Begleitanleitungen zum Handbuch für das Kernnetzwerk hinzufügen.

### <a name="directaccessremoteremote-accessdirectaccessdirectaccessmd"></a>[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess ermöglicht die Verbindung von Remotebenutzern mit Netzwerkressourcen der Organisation. 

Die DirectAccess-Dokumentation finden Sie nun im Windows Server 2016-Inhaltsverzeichnis im Abschnitt [Remote Access und Server-Management](https://docs.microsoft.com/windows-server/remote/) unter [Remote Access](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access). Weitere Informationen finden Sie unter [DirectAccess](../remote/remote-access/directaccess/DirectAccess.md).

### <a name="domain-name-system-40dns41dnsdns-topmd"></a>[DNS &#40;-Domain Name System&#41;](dns/dns-top.md)

Domain Name System \(DNS\) ist eine der branchenüblichen Suiten von Protokollen, die TCP/IP umfassen, und zusammen stellen DNS-Client und DNS-Server Computern und Benutzern einen Namensauflösungsdienst für die Zuordnung von Computername zu IP-Adresse bereit.

### <a name="dynamic-host-configuration-protocol-40dhcp41technologiesdhcpdhcp-topmd"></a>[DHCP für das Dynamic &#40;Host Configuration-Protokoll&#41;](technologies/dhcp/dhcp-top.md)

Dynamic Host Configuration-Protokoll \(DHCP\) ist ein Client/Server-Protokoll, das einem Internetprotokollhost \(IP\) automatisch seine IP-Adresse und andere Konfigurationsinformationen bereitstellt, z. B. die Subnetzmaske und das Standardgateway.

### <a name="hyper-v-network-virtualizationsdntechnologieshyper-v-network-virtualizationhyper-v-network-virtualizationmd"></a>[Hyper-V-Netzwerkvirtualisierung](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-V-Netzwerkvirtualisierung \(HNV\) ermöglicht die Virtualisierung von Kundennetzwerken auf der Basis einer gemeinsam genutzten physischen Netzwerkinfrastruktur.

### <a name="hyper-v-virtual-switchvirtualizationhyper-v-virtual-switchhyper-v-virtual-switchmd"></a>[Virtueller Hyper-V-Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Beim virtuellen Hyper-V-Switch handelt es sich um einen softwarebasierten Schicht-2-Ethernet-Netzwerkswitch, der im Hyper-V-Manager verfügbar ist, wenn Sie die Hyper-V-Serverrolle installieren. Der Switch umfasst programmgesteuert verwaltete und erweiterbare Funktionen zum Verbinden virtueller Computer mit virtuellen Netzwerken und dem physischen Netzwerk. Außerdem bietet der virtuelle Hyper-V-Switch Richtlinienerzwingung für Sicherheits-, Isolations- und Dienststufen. 

Die Hyper-V Virtual Switch-Dokumentation finden Sie nun im Abschnitt **Virtualisierung** des Windows Server 2016-Inhaltsverzeichnisses. Weitere Informationen finden Sie unter [Hyper-V Virtual Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).

### <a name="ip-address-management-40ipam41technologiesipamipam-topmd"></a>[IP-Adress &#40;Verwaltung (IPAM)&#41;](technologies/ipam/ipam-top.md)

Bei der IP-Adressverwaltung \(IPAM\) handelt es sich um eine integrierte Suite an Tools, die die durchgängige Planung, Bereitstellung, Verwaltung und Überwachung Ihrer IP-Adresseninfrastruktur mit einer umfassenden Benutzeroberfläche ermöglichen. IPAM ermittelt IP-Adress Infrastruktur Server und Domain Name System \(DNS\) -Server in Ihrem Netzwerk automatisch und ermöglicht die Verwaltung dieser Server über eine zentrale Schnittstelle.

### <a name="network-load-balancingtechnologiesnetwork-load-balancingmd"></a>[Netzwerklastenausgleich](technologies/Network-Load-Balancing.md)

Beim Netzwerklastenausgleich \(NLB\) wird der Datenverkehr mithilfe des TCP/IP-Netzwerkprotokolls über mehrere Server verteilt. Bei Nicht-SDN-Bereitstellungen stellt NLB sicher, dass statusfreie Anwendungen, beispielsweise Webserver, auf denen Internetinformationsdienste \(IIS\) ausgeführt werden, durch Hinzufügen zusätzlicher Server bei zunehmender Last skalierbar sind.

### <a name="high-performance-networkingtechnologieshpnhpn-topmd"></a>[Hochleistungs Netzwerke](technologies/hpn/hpn-top.md)

Netzwerk-Offload- und Optimierungstechnologien in Windows Server 2016 umfassen Software Only (SO)-Features und -Technologien, integrierte Software- und Hardware (SH)-Features und -Technologien sowie Hardware Only (HO)-Features und -Technologien.

Für Offload- und Optimierungstechnologien steht folgende Dokumentation zur Verfügung:

- [Konfigurations Handbuch für konvergierte Netzwerkschnittstellenkarten (NIC)](technologies/conv-nic/cnic-top.md)
- [Data Center Bridging (DCB)](technologies/dcb/dcb-top.md)
- [Virtual Receive Side Scaling (vRSS)](technologies/vrss/vrss-top.md)


### <a name="network-policy-servertechnologiesnpsnps-topmd"></a>[Netzwerk Richtlinien Server](technologies/nps/nps-top.md)

Mit einem Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie organisationsweite Netzwerkzugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen.

### <a name="network-shell-netshtechnologiesnetshnetshmd"></a>[Network Shell (Netsh)](technologies/netsh/netsh.md)

Zum Verwalten von Netzwerktechnologien in \(Windows Server\) 2016 und Windows 10 können Sie das Netsh Networking-Hilfsprogramm Network Shell verwenden.

### <a name="network-subsystem-performance-tuningtechnologiesnetwork-subsystemnet-sub-performance-topmd"></a>[Leistungsoptimierung des Netzwerk Subsystems](technologies/network-subsystem/net-sub-performance-top.md)

Dieses Thema enthält Informationen zum Auswählen des richtigen Netzwerkadapters für Ihre Server Arbeitsauslastung, zum Anordnen von Netzwerkschnittstellen, netzwerkbezogenen Leistungsindikatoren und zur Leistungsoptimierung von Netzwerkadaptern und zugehörigen Netzwerktechnologien, wie z. b. Empfangs seitige \(Skalierung\)(RSS), \(Empfangs seitige zusammen\)Fügung von RSC und anderen.

### <a name="nic-teamingtechnologiesnic-teamingnic-teamingmd"></a>[NIC-Teamvorgang](technologies/nic-teaming/NIC-Teaming.md)

NIC-Teaming ermöglicht Ihnen, physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter zu gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.

### <a name="quality-of-service-qos-policytechnologiesqosqos-policy-topmd"></a>[Quality of Service (QoS)-Richtlinie](technologies/qos/qos-policy-top.md)

Sie können die QoS-Richtlinie als zentralen Punkt für die Verwaltung der Netzwerkbandbreite in Ihrer gesamten Active Directory-Infrastruktur verwenden, indem Sie QoS-Profile erstellen, deren Einstellungen mit Gruppenrichtlinien verteilt werden.

### <a name="remote-accessremoteremote-accessremote-accessmd"></a>[Remotezugriff](../remote/remote-access/remote-access.md)

Sie können Remote Zugriffs Technologien wie DirectAccess und VPN-VPN \(\) (virtuelles privates Netzwerk) verwenden, um Remote Arbeitskräften Verbindungen mit internen Netzwerkressourcen zu ermöglichen. Außerdem können Sie den \(Remote Zugriff für LAN-Routing im LAN\) und für webanwendungsproxy verwenden. Dieser Proxy bietet Reverseproxyfunktion für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können.

Die Dokumentation für Remote Access finden Sie nun im Abschnitt [Remote Access und Serververwaltung](https://docs.microsoft.com/windows-server/remote/) des Windows Server 2016-Inhaltsverzeichnisses. Weitere Informationen finden Sie unter [Remote Access](../remote/remote-access/remote-access.md).

Weitere Informationen zu Web Application Proxy (ein Rollendienst der Remote Access-Serverrolle) finden Sie unter [Web Application Proxy in Windows Server 2016](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server).

### <a name="virtual-private-networking-vpnremoteremote-accessvpnvpn-topmd"></a>[Virtual Private Networking (VPN)](../remote/remote-access/vpn/vpn-top.md)

In Windows Server 2016 ist **DirectAccess und VPN**ein Rollendienst der **Remote Access**-Serverrolle.

Wenn Sie den Remote Zugriff als VPN-Server installieren, können Sie mithilfe des VPN \(-\) VPN (virtuelles privates Netzwerk) ihren Remote Mitarbeitern Verbindungen mit Ihrem Unternehmensnetzwerk über das Internet bereitstellen, während gleichzeitig Informationen verwaltet werden. Datenschutz mit verschlüsselten Verbindungen.

Mit Windows Server 2016 Remote Access VPN – und Windows 10-Clientcomputern – können Sie nun Always On VPN bereitstellen. Mit Always On VPN verwalten Sie Remote-VPN-Clients, die immer verbunden sind, um externen Mitarbeitern zusätzlichen Komfort bieten, weil sich diese nicht mehr manuell über VPN mit dem Netzwerk Ihres Unternehmens verbinden oder von diesem trennen müssen.

Weitere Informationen finden Sie unter [Remote Access Always On VPN Deployment Guide for Windows Server 2016 and Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

>[!NOTE]
>Die VPN-Dokumentation finden Sie nun im Windows Server 2016-Inhaltsverzeichnis im Abschnitt [Remote Access und Server-Management](https://docs.microsoft.com/windows-server/remote/) unter [Remote Access](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access).

Weitere Informationen über VPN finden Sie unter [Virtual Private Networking (VPN)](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-top).

### <a name="windows-container-networkinghttpsdocsmicrosoftcomvirtualizationwindowscontainersmanage-containerscontainer-networking"></a>[Windows-Container Netzwerk](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/container-networking)

Windows Container Networking ermöglicht das Erstellen und Verwalten von Netzwerken zum Verbinden von Containerendpunkten auf Windows 10- und Windows Server-Hosts mithilfe von standardmäßigen Branchentools und Workflows. Windows Container Networking unterstützt mehrere Topologien, z. B. private, flat-L2 und routed-L3.

Unterstützt werden auch Überlagerungen, die Sie lokal auf dem Host erstellen können, indem Sie Docker, Kubernetes oder Windows PowerShell über Plug-Ins verwenden, die \(mit\)dem Windows Host Network Service HNS kommunizieren. Sie können Cluster Netzwerke mit mehreren\-Knoten mithilfe von Orchestrierungs Systemen auf höherer Ebene erstellen und verwalten, indem Sie über einen lokalen Agent mit dem HNS eines Knotens kommunizieren.

### <a name="windows-internet-name-service-winstechnologieswinswins-topmd"></a>[Windows Internet Name Service (WINS)](technologies/wins/wins-top.md)

Windows Internet Name Service (WINS) ist ein älterer Registrierungs- und Auflösungsdienst für Computernamen, der einem Computer-NetBIOS-Namen eine IP-Adresse zuordnet. Es wird empfohlen, DNS statt WINS zu verwenden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

Networking-Ressourcen für Betriebssysteme vor Windows Server 2016 stehen unter den folgenden Links zur Verfügung:

- Windows Server 2012 und Windows Server 2012 R2 [Übersicht über Netzwerke](https://technet.microsoft.com/library/hh831357.aspx)
- Windows Server 2008 und Windows Server 2008 R2 [Netzwerke](https://technet.microsoft.com/library/cc753940)
- Windows Server 2003 [Windows Server 2003/2003 R2-deaktivierter Inhalt](https://www.microsoft.com/download/details.aspx?id=53314)
