---
title: Netzwerk
description: Dieses Thema enthält eine Übersicht über die Software Defined Networking- und Netzwerkplattform-Technologien, die in Windows Server 2016 verfügbar sind.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: 05/08/2018
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 7caa99f1b6b9e25e5a6f2c4333b033fb3088195d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862591"
---
# <a name="networking"></a>Netzwerk

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf docs.microsoft.com an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> Netzwerke sind ein grundlegender Bestandteil der Software definiert Datencenter \(SDDC\) -Plattform und Windows Server 2016 bietet neue und verbesserte Software Defined Networking \(SDN\) Technologien können Sie das Verschieben in eine vollständig implementierten SDDC-Lösung für Ihre Organisation.

Wenn Sie Netzwerke als softwaredefinierte Ressource verwalten, brauchen Sie Anforderungen einer Anwendung an die Infrastruktur nur einmal zu beschreiben und können dann auswählen, wo die Anwendung ausgeführt wird – lokal oder in der Cloud. 

Diese Konsistenz bedeutet, dass die Anwendungen sich jetzt leichter skalieren und nahtlos überall mit der gleichen Zuverlässigkeit hinsichtlich Sicherheit, Leistung, Dienstqualität und Verfügbarkeit ausführen lassen.

>[!Note]
> Weitere Informationen zum Download von Windows Server finden Sie unter [Windows Server-Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview).

Windows Server 2016 fügt die folgenden neuen Netzwerktechnologien ein:

- Software-Defined Networking: Netzwerkcontroller bietet die Möglichkeit einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum. Netzwerkcontroller ermöglicht es Ihnen Netzwerkfunktionsvirtualisierung zur einfachen Bereitstellung von virtuellen Computern verwenden \(VMs\) für den Softwarelastenausgleich \(SLB\) zur Optimierung von Netzwerkverkehr lädt für Ihren Mandanten und RAS- Mandanten mit den Konnektivitätsoptionen zu erhalten zwischen dem Internet, lokalen und Cloud-Gateways Ressourcen. Mithilfe von Netzwerkcontrollern könne Sie zudem Datacenter Firewall auf virtuellen Computern und Hyper-V-Hosts verwalten.

- Netzwerkplattform: Neue Features für vorhandene Technologien für Network-Plattform verwenden, können Sie DNS-Richtlinie Ihre DNS-Serverantworten auf Abfragen anpassen, verwenden Sie eine zusammengeführte NIC, dass die kombinierte Remote Direct Memory Access \(RDMA\) und Ethernet-Datenverkehr , verwenden Sie Switch Embedded Teaming \(festgelegt\) zum Erstellen von virtuellen Hyper-V-Switches mit RDMA-NICs verbunden sind, und verwenden IP-Adressverwaltung \(IPAM\) zum Verwalten von DNS-Zonen und -Servern sowie DHCP- und IP-Adressen.

Weitere Informationen finden Sie unter [Von Windows Server unterstützte Netzwerkszenarien](windows-server-supported-networking-scenarios.md).

Die folgenden Abschnitte enthalten Informationen zu den SDN-Technologien und Netzwerkplattformtechnologien.

## <a name="software-defined-networking-technologies"></a>Software-Defined Networking-Technologien

### <a name="software-defined-networking-40sdn41sdnsoftware-defined-networkingmd"></a>[Software-Defined Networking &#40;SDN&#41;](sdn/software-defined-networking.md)

Dieses Thema enthält Informationen zu den SDN-Technologien, die in Windows Server, System Center und Microsoft Azure bereitgestellt werden.

>[!NOTE]
>Für Hyper-V-Hosts und virtuellen Maschinen \(VMs\) die SDN-Infrastrukturserver, z. B. dem Netzwerkcontroller und den Softwarelastenausgleich-Knoten führen, Sie Windows Server 2016 Datacenter-Edition installieren müssen. Für Hyper-V-Hosts, die nur arbeitsauslastungs-VMs, die mit SDN verbunden sind Mandanten\-gesteuert von Netzwerken, können Sie Windows Server 2016 Standard Edition ausführen.

### <a name="deploy-a-software-defined-network-infrastructure-using-scriptssdndeploydeploy-a-software-defined-network-infrastructure-using-scriptsmd"></a>[Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
Dieses Handbuch enthält Anweisungen zum Bereitstellen eines Netzwerkcontrollers mit virtuellen Netzwerken und Gateways in einer Testumgebung.

### <a name="network-controllersdntechnologiesnetwork-controllernetwork-controllermd"></a>[Netzwerkcontroller](sdn/technologies/network-controller/Network-Controller.md)

Netzwerkcontroller bietet die Möglichkeit einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum.

### <a name="software-load-balancing-40slb41-for-sdnsdntechnologiesnetwork-function-virtualizationsoftware-load-balancing-for-sdnmd"></a>[Softwarelastenausgleich &#40;SLB&#41; für SDN](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

Cloud-Dienstanbieter \(CSPs\) und Unternehmen, die Software-Defined Networking (SDN) in Windows Server 2016 bereitstellen können, den Softwarelastenausgleich \(SLB\) Mandanten und Mandanten gleichmäßig verteilen Kunden von Netzwerkdatenverkehr zwischen Ressourcen des virtuellen Netzwerks. Windows Server-SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen.

### <a name="ras-gateway-for-sdnsdntechnologiesnetwork-function-virtualizationras-gateway-for-sdnmd"></a>[RAS-Gateway für SDN](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

RAS-Gateway, eine softwarebasierte, mehrinstanzenfähige Border Gateway Protocol ist \(BGP\) fähiger Router in Windows Server 2016 ist für das Cloud-Dienstanbieter \(CSPs\) und Unternehmen, die hosten mehrinstanzenfähige virtuelle Netzwerke mithilfe der Hyper-V-Netzwerkvirtualisierung. 

### <a name="network-function-virtualizationsdntechnologiesnetwork-function-virtualizationnetwork-function-virtualizationmd"></a>[Netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

Netzwerk-Funktionen, die von Hardware ausgeführt wird, werden in softwaredefinierten Rechenzentren \(wie Load balancer, Firewalls, Routern, Switches und So weiter\) werden zunehmend als virtuelle Appliances virtualisiert wird. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung.

### <a name="datacenter-firewall-overviewsdntechnologiesnetwork-function-virtualizationdatacenter-firewall-overviewmd"></a>[Rechenzentrumsfirewall: Übersicht](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

Datacenter Firewall ist eine statusbehaftete, mehrinstanzenfähige 5-Tupel-Firewall (Protokoll, Portnummer von Quelle und Ziel sowie IP-Adresse von Quelle und Ziel), die auf der Vermittlungsschicht implementiert ist.

## <a name="bkmk_networking"></a>Networking-Technologien

Die folgende Tabelle enthält Links für einige der Netzwerktechnologien in Windows Server 2016.

### <a name="whats-new-in-networkingnetworkingwhat-s-new-in-networkingmd"></a>[Neues bei Netzwerken](../networking/What-s-New-in-Networking.md)

In den folgenden Abschnitten finden Sie neue Netzwerktechnologien und neue Features für vorhandene Technologien in Windows Server 2016.

### <a name="branchcachebranchcachebranchcachemd"></a>[BranchCache](branchcache/BranchCache.md)

BranchCache ist ein wide Area Network \(WAN\) Technologie zur Optimierung der Bandbreite. Um die WAN-Bandbreite zu optimieren, wenn Benutzer auf Inhalte von Remoteservern zugreifen, ruft BranchCache Inhalte von Inhaltsservern in der Hauptniederlassung oder gehosteten Cloudinhaltsservern ab und speichert sie an Filialstandorten zwischen, sodass Clientcomputer in Filialen lokal und nicht über das WAN auf diese Inhalte zugreifen können.

### <a name="core-network-guide-for-windows-server-2016core-network-guidecore-network-guide-windows-servermd"></a>[Kernnetzwerkhandbuch für WindowsServer 2016](core-network-guide/core-network-guide-windows-server.md)

Erfahren Sie, wie Sie ein Windows Server-Netzwerk mit dem Handbuch für das Kernnetzwerk bereitstellen und Funktionen zur Netzwerkbereitstellung mit den Begleitanleitungen zum Handbuch für das Kernnetzwerk hinzufügen.

### <a name="directaccessremoteremote-accessdirectaccessdirectaccessmd"></a>[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess ermöglicht die Verbindung von Remotebenutzern mit Netzwerkressourcen der Organisation. 

Die DirectAccess-Dokumentation finden Sie nun im Windows Server 2016-Inhaltsverzeichnis im Abschnitt [Remote Access und Server-Management](https://docs.microsoft.com/windows-server/remote/) unter [Remote Access](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access). Weitere Informationen finden Sie unter [DirectAccess](../remote/remote-access/directaccess/DirectAccess.md).

### <a name="domain-name-system-40dns41dnsdns-topmd"></a>[Domain Name System &#40;DNS&#41;](dns/dns-top.md)

Domain Name System \(DNS\) ist eine der branchenüblichen Suiten von Protokollen, die TCP/IP umfassen, und zusammen stellen DNS-Client und DNS-Server Computern und Benutzern einen Namensauflösungsdienst für die Zuordnung von Computername zu IP-Adresse bereit.

### <a name="dynamic-host-configuration-protocol-40dhcp41technologiesdhcpdhcp-topmd"></a>[Dynamic Host Configuration-Protokoll &#40;DHCP&#41;](technologies/dhcp/dhcp-top.md)

Dynamic Host Configuration-Protokoll \(DHCP\) ist ein Client/Server-Protokoll, das einem Internetprotokollhost \(IP\) automatisch seine IP-Adresse und andere Konfigurationsinformationen bereitstellt, z. B. die Subnetzmaske und das Standardgateway.

### <a name="hyper-v-network-virtualizationsdntechnologieshyper-v-network-virtualizationhyper-v-network-virtualizationmd"></a>[Hyper-V-Netzwerkvirtualisierung](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-V-Netzwerkvirtualisierung \(HNV\) ermöglicht die Virtualisierung von Kundennetzwerken auf der Basis einer gemeinsam genutzten physischen Netzwerkinfrastruktur.

### <a name="hyper-v-virtual-switchvirtualizationhyper-v-virtual-switchhyper-v-virtual-switchmd"></a>[Hyper-V-Switches](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Beim virtuellen Hyper-V-Switch handelt es sich um einen softwarebasierten Schicht-2-Ethernet-Netzwerkswitch, der im Hyper-V-Manager verfügbar ist, wenn Sie die Hyper-V-Serverrolle installieren. Der Switch umfasst programmgesteuert verwaltete und erweiterbare Funktionen zum Verbinden virtueller Computer mit virtuellen Netzwerken und dem physischen Netzwerk. Außerdem bietet der virtuelle Hyper-V-Switch Richtlinienerzwingung für Sicherheits-, Isolations- und Dienststufen. 

Die Hyper-V Virtual Switch-Dokumentation finden Sie nun im Abschnitt **Virtualisierung** des Windows Server 2016-Inhaltsverzeichnisses. Weitere Informationen finden Sie unter [Hyper-V Virtual Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).

### <a name="ip-address-management-40ipam41technologiesipamipam-topmd"></a>[IP-Adressverwaltung &#40;IPAM&#41;](technologies/ipam/ipam-top.md)

Bei der IP-Adressverwaltung \(IPAM\) handelt es sich um eine integrierte Suite an Tools, die die durchgängige Planung, Bereitstellung, Verwaltung und Überwachung Ihrer IP-Adresseninfrastruktur mit einer umfassenden Benutzeroberfläche ermöglichen. IPAM ermittelt IP-adresseninfrastrukturserver und DNS automatisch \(DNS\) Server in Ihrem Netzwerk und ermöglicht es Ihnen, die sie über eine zentrale Schnittstelle verwalten.

### <a name="network-load-balancingtechnologiesnetwork-load-balancingmd"></a>[Netzwerklastenausgleich](technologies/Network-Load-Balancing.md)

Beim Netzwerklastenausgleich \(NLB\) wird der Datenverkehr mithilfe des TCP/IP-Netzwerkprotokolls über mehrere Server verteilt. Bei Nicht-SDN-Bereitstellungen stellt NLB sicher, dass statusfreie Anwendungen, beispielsweise Webserver, auf denen Internetinformationsdienste \(IIS\) ausgeführt werden, durch Hinzufügen zusätzlicher Server bei zunehmender Last skalierbar sind.

### <a name="high-performance-networkingtechnologieshpnhpn-topmd"></a>[Hochleistungs-Netzwerk](technologies/hpn/hpn-top.md)

Netzwerk-Offload- und Optimierungstechnologien in Windows Server 2016 umfassen Software Only (SO)-Features und -Technologien, integrierte Software- und Hardware (SH)-Features und -Technologien sowie Hardware Only (HO)-Features und -Technologien.

Für Offload- und Optimierungstechnologien steht folgende Dokumentation zur Verfügung:

- [Konfigurationshandbuch für zusammengeführte Netzwerk Schnittstelle Netzwerkschnittstellenkarte (NIC)](technologies/conv-nic/cnic-top.md)
- [Für Data Center Bridging (DCB)](technologies/dcb/dcb-top.md)
- [Virtuelle empfangsseitige Skalierung (vRSS)](technologies/vrss/vrss-top.md)


### <a name="network-policy-servertechnologiesnpsnps-topmd"></a>[Netzwerkrichtlinienserver](technologies/nps/nps-top.md)

Mit einem Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie organisationsweite Netzwerkzugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen.

### <a name="network-shell-netshtechnologiesnetshnetshmd"></a>[Netzwerkshell (Netsh)](technologies/netsh/netsh.md)

Sie können die Netzwerk-Shell \(Netsh\) networking-Hilfsprogramm zum Verwalten der netzwerktechnologien in Windows Server 2016 und Windows 10.

### <a name="network-subsystem-performance-tuningtechnologiesnetwork-subsystemnet-sub-performance-topmd"></a>[Netzwerksubsystem optimieren](technologies/network-subsystem/net-sub-performance-top.md)

Dieses Thema enthält Informationen zum Auswählen des geeigneten Netzwerkadapters für Ihre serverarbeitsauslastung, netzwerkbezogenen Sortierung Netzwerkschnittstellen, Leistungsindikatoren und Optimieren der Leistung network Adapter und zugehörige netzwerktechnologien wie z. B. Empfangsseitige Skalierung \(RSS\), empfangen Side Coalescing \(RSC\), und andere.

### <a name="nic-teamingtechnologiesnic-teamingnic-teamingmd"></a>[NIC-Teamvorgang](technologies/nic-teaming/NIC-Teaming.md)

NIC-Teaming ermöglicht Ihnen, physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter zu gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.

### <a name="quality-of-service-qos-policytechnologiesqosqos-policy-topmd"></a>[Quality of Service (QoS)-Richtlinie](technologies/qos/qos-policy-top.md)

Sie können die QoS-Richtlinie als zentralen Punkt für die Verwaltung der Netzwerkbandbreite in Ihrer gesamten Active Directory-Infrastruktur verwenden, indem Sie QoS-Profile erstellen, deren Einstellungen mit Gruppenrichtlinien verteilt werden.

### <a name="remote-accessremoteremote-accessremote-accessmd"></a>[Remotezugriff](../remote/remote-access/remote-access.md)

Können Sie Remotezugriffstechnologien wie DirectAccess und Virtual Private Networking \(VPN\) für Verbindungen mit internen Netzwerkressourcen Remotemitarbeiter bereit. Darüber hinaus können Sie den Remotezugriff für lokale Netzwerke \(LAN\) routing, und für die Web Application Proxy. Dieser Proxy bietet Reverseproxyfunktion für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können.

Die Dokumentation für Remote Access finden Sie nun im Abschnitt [Remote Access und Serververwaltung](https://docs.microsoft.com/windows-server/remote/) des Windows Server 2016-Inhaltsverzeichnisses. Weitere Informationen finden Sie unter [Remote Access](../remote/remote-access/remote-access.md).

Weitere Informationen zu Web Application Proxy (ein Rollendienst der Remote Access-Serverrolle) finden Sie unter [Web Application Proxy in Windows Server 2016](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server).

### <a name="virtual-private-networking-vpnremoteremote-accessvpnvpn-topmd"></a>[Virtuelle Private Netzwerke (VPN)](../remote/remote-access/vpn/vpn-top.md)

In Windows Server 2016 ist **DirectAccess und VPN**ein Rollendienst der **Remote Access**-Serverrolle.

Wenn Sie Remotezugriff auf einen VPN-Server installieren, können Sie virtuelles privates Netzwerk \(VPN\) zu den Remotemitarbeitern mit Verbindungen mit Ihrem Organisationsnetzwerk über das Internet - Informationen auch beibehalten werden. Datenschutz für verschlüsselte Verbindungen.

Mit Windows Server 2016 Remote Access VPN – und Windows 10-Clientcomputern – können Sie nun Always On VPN bereitstellen. Mit Always On VPN verwalten Sie Remote-VPN-Clients, die immer verbunden sind, um externen Mitarbeitern zusätzlichen Komfort bieten, weil sich diese nicht mehr manuell über VPN mit dem Netzwerk Ihres Unternehmens verbinden oder von diesem trennen müssen.

Weitere Informationen finden Sie unter [Remote Access Always On VPN Deployment Guide for Windows Server 2016 and Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

>[!NOTE]
>Die VPN-Dokumentation finden Sie nun im Windows Server 2016-Inhaltsverzeichnis im Abschnitt [Remote Access und Server-Management](https://docs.microsoft.com/windows-server/remote/) unter [Remote Access](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access).

Weitere Informationen über VPN finden Sie unter [Virtual Private Networking (VPN)](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-top).

### <a name="windows-container-networkinghttpsdocsmicrosoftcomvirtualizationwindowscontainersmanage-containerscontainer-networking"></a>[Windows-Containernetzwerk-Funktionen](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/container-networking)

Windows Container Networking ermöglicht das Erstellen und Verwalten von Netzwerken zum Verbinden von Containerendpunkten auf Windows 10- und Windows Server-Hosts mithilfe von standardmäßigen Branchentools und Workflows. Windows Container Networking unterstützt mehrere Topologien, z. B. private, flat-L2 und routed-L3.

Ebenfalls unterstützt, sind Overlays, die Sie lokal auf dem Host erstellen können mithilfe von Docker, Kubernetes oder Windows PowerShell über Plug-Ins, die Kommunikation mit dem Netzwerk-Dienst von Windows-Host \(HNS\). Sie können das Erstellen und Verwalten von mehreren\-Knoten Clusternetzwerke, durch höhere Ebene orchestrierungssysteme durch Kommunikation über einen lokalen Agent auf jedem Knoten des HNS.

### <a name="windows-internet-name-service-winstechnologieswinswins-topmd"></a>[Windows Internet Name Service (WINS)](technologies/wins/wins-top.md)

Windows Internet Name Service (WINS) ist ein älterer Registrierungs- und Auflösungsdienst für Computernamen, der einem Computer-NetBIOS-Namen eine IP-Adresse zuordnet. Es wird empfohlen, DNS statt WINS zu verwenden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

Networking-Ressourcen für Betriebssysteme vor Windows Server 2016 stehen unter den folgenden Links zur Verfügung:

- Windows Server 2012 und Windows Server 2012 R2 [Übersicht über Netzwerke](https://technet.microsoft.com/library/hh831357.aspx)
- Windows Server 2008 und Windows Server 2008 R2 [Netzwerke](https://technet.microsoft.com/library/cc753940)
- Windows Server 2003 [Windows Server 2003/2003 R2 – veraltete Inhalte ](https://www.microsoft.com/download/details.aspx?id=53314)
