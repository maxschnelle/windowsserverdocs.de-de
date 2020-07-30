---
title: Netzwerk
description: Dieses Thema enthält eine Übersicht über die Software Defined Networking- und Netzwerkplattform-Technologien, die in Windows Server 2016 verfügbar sind.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: 05/08/2018
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: anpaul
author: AnirbanPaul
ms.localizationpriority: medium
ms.openlocfilehash: 39bda1ac3a8b3cbac61435b65baf538f2d71e20e
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87408909"
---
# <a name="networking"></a>Netzwerk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

> [!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows Server? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf „docs.microsoft.com“ an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> Das Netzwerk ist ein grundlegender Bestandteil der SDDC-Plattform für den Software-Defined Datacenter \( \) , und Windows Server 2016 bietet neue und verbesserte Software-Defined Networking- \( Sdn- \) Technologien, mit deren Hilfe Sie zu einer vollständig erkannten SDDC-Lösung für Ihre Organisation wechseln können.

Wenn Sie Netzwerke als softwaredefinierte Ressource verwalten, können Sie die Infrastrukturanforderungen einer Anwendung einmalig beschreiben und dann auswählen, wo die Anwendung ausgeführt wird (lokal oder in der Cloud).

Diese Konsistenz bedeutet, dass Ihre Anwendungen nun einfacher zu skalieren sind, und Sie können Anwendungen nahtlos mit gleichem Vertrauen in Bezug auf Sicherheit, Leistung, Dienst Qualität und Verfügbarkeit ausführen.

>[!Note]
> Informationen zum Herunterladen von Windows Server finden Sie unter [Windows Server-Auswertungen](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview).

Windows Server 2016 fügt die folgenden neuen Netzwerktechnologien ein:

- Software-Defined Networking: Netzwerkcontroller bieten eine zentrale, programmierbare Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum. Mit dem Netzwerk Controller können Sie die netzwerkfunktionsvirtualisierung verwenden, um virtuelle Computer auf einfache Weise \( \) für den Software Lastenausgleich \( -SLB \) bereitzustellen, um den Netzwerk Datenverkehr für Ihre Mandanten zu optimieren, und RAS-Gateways, um Mandanten die erforderlichen Konnektivitätsoptionen zwischen Internet, lokalen und cloudressourcen bereitzustellen. Mithilfe von Netzwerkcontrollern könne Sie zudem Datacenter Firewall auf virtuellen Computern und Hyper-V-Hosts verwalten.

- Netzwerkplattform: Verwenden von neuen Features für vorhandene Netzwerkplattform-Technologien mithilfe der DNS-Richtlinie können Sie Ihre DNS-Server Antworten an Abfragen anpassen, eine konvergierte NIC verwenden, die den kombinierten Remote Zugriff auf den direkten Speicher für \( RDMA \) -und Ethernet-Datenverkehr verarbeitet. verwenden Sie Switch Embedded Teaming \( Set, \) um virtuelle Hyper-V-Switches zu erstellen, die mit RDMA-NICs verbunden \( \) sind

Weitere Informationen finden Sie [unter von Windows Server unterstützte Netzwerkszenarien](windows-server-supported-networking-scenarios.md).

In den folgenden Abschnitten finden Sie Informationen zu Sdn-Technologien und Netzwerkplattform-Technologien.

## <a name="software-defined-networking-technologies"></a>Software-Defined Networking-Technologien

### <a name="software-defined-networking-40sdn41"></a>[Software-Defined Networking &#40;Sdn&#41;](sdn/software-defined-networking.md)

Dieses Thema enthält Informationen zu den SDN-Technologien, die in Windows Server, System Center und Microsoft Azure bereitgestellt werden.

>[!NOTE]
>Bei Hyper-V-Hosts und virtuellen Computern, \( \) die Sdn-Infrastruktur Server ausführen, wie z. b. Netzwerk Controller und Software Lastenausgleich-Knoten, muss Windows Server 2016 Datacenter Edition installiert werden. Für Hyper-V-Hosts, die nur Mandanten-Arbeits Auslastungs-VMS enthalten, die mit Sdn- \- kontrollierten Netzwerken verbunden sind, können Sie Windows Server 2016 Standard Edition ausführen.

### <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>[Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
Dieses Handbuch enthält Anweisungen zum Bereitstellen eines Netzwerkcontrollers mit virtuellen Netzwerken und Gateways in einer Testumgebung.

### <a name="network-controller"></a>[Netzwerkcontroller](sdn/technologies/network-controller/Network-Controller.md)

Netzwerkcontroller bietet die Möglichkeit einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum.

### <a name="software-load-balancing-40slb41-for-sdn"></a>[Software Lastenausgleich &#40;SLB-&#41; für Sdn](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

Clouddienstanbieter \( -CSPs \) und Unternehmen, die Software-Defined Networking (SDN) in Windows Server 2016 bereitstellen, können SLB für den Software Lastenausgleich verwenden \( \) , um den Netzwerk Datenverkehr von Mandanten und Mandanten Kunden gleichmäßig auf die virtuellen Netzwerk Windows Server-SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen.

### <a name="ras-gateway-for-sdn"></a>[RAS-Gateway für SDN](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

RAS-Gateway, bei dem es sich um einen softwarebasierten, mehr Instanzen \( fähigen Border Gateway Protocol BGP \) -fähigen Router in Windows Server 2016 handelt, ist für clouddienstanbieter \( -CSPs \) und Unternehmen konzipiert, die mehrere virtuelle Mandanten Netzwerke mithilfe der Hyper-V-Netzwerkvirtualisierung hosten.

### <a name="network-function-virtualization"></a>[Netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

In Software definierten Rechenzentren werden Netzwerkfunktionen, die von Hardware Geräten \( wie Load Balancer, Firewalls, Routern, Switches usw. ausgeführt werden, \) zunehmend als virtuelle Geräte virtualisiert. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung.

### <a name="datacenter-firewall-overview"></a>[Übersicht über Datacenter Firewall](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

Datacenter Firewall ist eine statusbehaftete, mehrinstanzenfähige 5-Tupel-Firewall (Protokoll, Portnummer von Quelle und Ziel sowie IP-Adresse von Quelle und Ziel), die auf der Vermittlungsschicht implementiert ist.

## <a name="networking-technologies"></a><a name="bkmk_networking"></a>Netzwerktechnologien

In der folgenden Tabelle finden Sie Links zu einigen Netzwerktechnologien in Windows Server 2016.

### <a name="whats-new-in-networking"></a>[Neues bei Netzwerken](../networking/What-s-New-in-Networking.md)

In den folgenden Abschnitten finden Sie Informationen zu neuen Netzwerktechnologien und neuen Features für vorhandene Technologien in Windows Server 2016.

### <a name="branchcache"></a>[BranchCache](branchcache/BranchCache.md)

BranchCache ist eine \( Technologie zur WAN- \) Bandbreitenoptimierung für Wide Area Network. Um die WAN-Bandbreite zu optimieren, wenn Benutzer auf Inhalte von Remoteservern zugreifen, ruft BranchCache Inhalte von Inhaltsservern in der Hauptniederlassung oder gehosteten Cloudinhaltsservern ab und speichert sie an Filialstandorten zwischen, sodass Clientcomputer in Filialen lokal und nicht über das WAN auf diese Inhalte zugreifen können.

### <a name="core-network-guide-for-windows-server-2016"></a>[Hauptnetzwerkhandbuch für Windows Server 2016](core-network-guide/core-network-guide-windows-server.md)

Informieren Sie sich über das Bereitstellen eines Windows Server-Netzwerks mithilfe des Handbuchs zum Hauptnetzwerk, und fügen Sie der Netzwerk Bereitstellung mit den Begleit Handbüchern des Haupt Netzwerks Features hinzu.

### <a name="directaccess"></a>[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess ermöglicht die Konnektivität von Remote Benutzern mit Netzwerkressourcen in der Organisation.

Die DirectAccess-Dokumentation befindet sich jetzt im Abschnitt [Remote Zugriff und Serververwaltung](https://docs.microsoft.com/windows-server/remote/) des Inhaltsverzeichnisses von Windows Server 2016 unter [Remote Zugriff](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access). Weitere Informationen finden Sie unter [DirectAccess](../remote/remote-access/directaccess/DirectAccess.md).

### <a name="domain-name-system-40dns41"></a>[Domain Name System &#40;DNS-&#41;](dns/dns-top.md)

Domain Name System \(DNS\) ist eine der branchenüblichen Suiten von Protokollen, die TCP/IP umfassen, und zusammen stellen DNS-Client und DNS-Server Computern und Benutzern einen Namensauflösungsdienst für die Zuordnung von Computername zu IP-Adresse bereit.

### <a name="dynamic-host-configuration-protocol-40dhcp41"></a>[Dynamic Host Configuration-Protokoll &#40;DHCP-&#41;](technologies/dhcp/dhcp-top.md)

Dynamic Host Configuration-Protokoll \(DHCP\) ist ein Client/Server-Protokoll, das einem Internetprotokollhost \(IP\) automatisch seine IP-Adresse und andere Konfigurationsinformationen bereitstellt, z. B. die Subnetzmaske und das Standardgateway.

### <a name="hyper-v-network-virtualization"></a>[Hyper-V-Netzwerkvirtualisierung](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-V-Netzwerkvirtualisierung- \( HNV \) ermöglicht die Virtualisierung von Kunden Netzwerken auf einer freigegebenen physischen Netzwerkinfrastruktur.

### <a name="hyper-v-virtual-switch"></a>[Virtueller Hyper-V-Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Beim virtuellen Hyper-V-Switch handelt es sich um einen softwarebasierten Schicht-2-Ethernet-Netzwerkswitch, der im Hyper-V-Manager verfügbar ist, wenn Sie die Hyper-V-Serverrolle installieren. Der Switch umfasst programmgesteuert verwaltete und erweiterbare Funktionen zum Verbinden virtueller Computer mit virtuellen Netzwerken und dem physischen Netzwerk. Außerdem bietet der virtuelle Hyper-V-Switch Richtlinienerzwingung für Sicherheits-, Isolations- und Dienststufen.

Die Dokumentation zum virtuellen Hyper-V-Switch befindet sich nun im Abschnitt **Virtualization** des Inhaltsverzeichnisses von Windows Server 2016. Weitere Informationen finden Sie unter [virtueller Hyper-V-Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).

### <a name="ip-address-management-40ipam41"></a>[IP-Adressverwaltung &#40;IPAM-&#41;](technologies/ipam/ipam-top.md)

Bei der IP-Adressverwaltung \(IPAM\) handelt es sich um eine integrierte Suite an Tools, die die durchgängige Planung, Bereitstellung, Verwaltung und Überwachung Ihrer IP-Adresseninfrastruktur mit einer umfassenden Benutzeroberfläche ermöglichen. IPAM ermittelt IP-Adress Infrastruktur Server und Domain Name System \( DNS- \) Server in Ihrem Netzwerk automatisch und ermöglicht die Verwaltung dieser Server über eine zentrale Schnittstelle.

### <a name="network-load-balancing"></a>[Netzwerklastenausgleich](technologies/Network-Load-Balancing.md)

Beim Netzwerklastenausgleich \(NLB\) wird der Datenverkehr mithilfe des TCP/IP-Netzwerkprotokolls über mehrere Server verteilt. Bei Nicht-SDN-Bereitstellungen stellt NLB sicher, dass statusfreie Anwendungen, beispielsweise Webserver, auf denen Internetinformationsdienste \(IIS\) ausgeführt werden, durch Hinzufügen zusätzlicher Server bei zunehmender Last skalierbar sind.

### <a name="high-performance-networking"></a>[High-Performance Networking](technologies/hpn/hpn-top.md)

Netzwerkablade-und-Optimierungstechnologien in Windows Server 2016 enthalten nur Software (also Features und Technologien), integrierte Features und Technologien für Software und Hardware (SH) und Technologien sowie Features und Technologien, die ausschließlich Hardware (Ho) enthalten.

Die folgende Dokumentation zur Auslagerungs-und Optimierungs Technologie ist ebenfalls verfügbar.

- [Konfigurations Handbuch für konvergierte Netzwerkschnittstellenkarten (NIC)](technologies/conv-nic/cnic-top.md)
- [Data Center Bridging (DCB)](technologies/dcb/dcb-top.md)
- [Virtual Receive Side Scaling (vRSS)](technologies/vrss/vrss-top.md)


### <a name="network-policy-server"></a>[Netzwerkrichtlinienserver](technologies/nps/nps-top.md)

Mit dem Netzwerk Richtlinien Server (Network Policy Server, NPS) können Sie Organisations weite Netzwerk Zugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen.

### <a name="network-shell-netsh"></a>[Network Shell (Netsh)](technologies/netsh/netsh.md)

\( \) Zum Verwalten von Netzwerktechnologien in Windows Server 2016 und Windows 10 können Sie das Netsh Networking-Hilfsprogramm Network Shell verwenden.

### <a name="network-subsystem-performance-tuning"></a>[Leistungsoptimierung für das Netzwerksubsystem](technologies/network-subsystem/net-sub-performance-top.md)

Dieses Thema enthält Informationen zum Auswählen des richtigen Netzwerkadapters für Ihre Server Arbeitsauslastung, zum Anordnen von Netzwerkschnittstellen, netzwerkbezogenen Leistungsindikatoren und zur Optimierung von Netzwerkadaptern und Netzwerktechnologien, wie z. b. RSS-seitige Skalierung, Empfangs seitige zusammen Fügung von \( \) \( RSC \) und anderen.

### <a name="nic-teaming"></a>[NIC-Teamvorgang](technologies/nic-teaming/NIC-Teaming.md)

NIC-Teaming ermöglicht Ihnen, physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter zu gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.

### <a name="quality-of-service-qos-policy"></a>[Quality of Service (QoS)-Richtlinie](technologies/qos/qos-policy-top.md)

Sie können die QoS-Richtlinie als zentralen Punkt für die Verwaltung der Netzwerkbandbreite in der gesamten Active Directory Infrastruktur verwenden, indem Sie QoS-Profile erstellen, deren Einstellungen mit Gruppenrichtlinie verteilt werden.

### <a name="remote-access"></a>[Remotezugriff](../remote/remote-access/remote-access.md)

Sie können Remote Zugriffs Technologien wie DirectAccess und VPN-VPN (virtuelles privates Netzwerk) verwenden, \( \) um Remote Arbeitskräften Verbindungen mit internen Netzwerkressourcen zu ermöglichen. Außerdem können Sie den Remote Zugriff für \( LAN \) -Routing im LAN und für webanwendungsproxy verwenden. Diese Funktion bietet Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer auf allen Geräten von außerhalb des Unternehmensnetzwerks darauf zugreifen können.

Die Dokumentation zum Remote Zugriff befindet sich nun im Abschnitt [Remote Zugriff und Serververwaltung](https://docs.microsoft.com/windows-server/remote/) des Inhaltsverzeichnisses von Windows Server 2016. Weitere Informationen finden Sie unter [Remote Zugriff](../remote/remote-access/remote-access.md).

Weitere Informationen zum webanwendungsproxy, einem Rollen Dienst der Remote Zugriffs-Server Rolle, finden Sie unter [webanwendungsproxy in Windows Server 2016](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server).

### <a name="virtual-private-networking-vpn"></a>[Virtual Private Networking (VPN)](../remote/remote-access/vpn/vpn-top.md)

In Windows Server 2016 ist **DirectAccess und VPN** ein Rollen Dienst der **Remote Zugriffs** -Server Rolle.

Wenn Sie den Remote Zugriff als VPN-Server installieren, können Sie \( mit dem VPN-VPN (virtuelles privates Netzwerk) \) ihren Remote Mitarbeitern Verbindungen mit Ihrem Unternehmensnetzwerk über das Internet bereitstellen, während gleichzeitig der Datenschutz mit verschlüsselten Verbindungen gewahrt bleibt.

Mit Windows Server 2016-RAS-VPN-und Windows 10-Client Computern können Sie jetzt Always on-VPN bereitstellen. Always on-VPN ermöglicht Ihnen die Verwaltung von Remote-VPN-Clients, die immer verbunden sind, und bietet gleichzeitig die Möglichkeit, Remote Arbeitsthreads zu verwalten, die nicht mehr manuell eine Verbindung mit dem VPN und Ihrem Organisations Netzwerk herstellen müssen.

Weitere Informationen finden Sie im [Bereitstellungs Handbuch für Remote Zugriff Always on VPN für Windows Server 2016 und Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

>[!NOTE]
>Die VPN-Dokumentation befindet sich nun im Abschnitt [Remote Zugriff und Serververwaltung](https://docs.microsoft.com/windows-server/remote/) des Inhaltsverzeichnisses von Windows Server 2016 unter [Remote Zugriff](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access).

Weitere Informationen zu VPN finden Sie unter [virtuelles privates Netzwerk (VPN)](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-top).

### <a name="windows-container-networking"></a>[Windows-Containernetzwerk](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/container-networking)

Mithilfe der Windows-Container Netzwerke können Sie Netzwerke zum Verbinden von Container Endpunkten auf Windows 10-und Windows Server-Hosts mithilfe von standardmäßigen Industrie Tools und-Workflows erstellen und verwalten. Windows-Container Netzwerke unterstützen mehrere Topologien, einschließlich Private, flache L2-und Routing-L3.

Unterstützt werden auch Überlagerungen, die Sie lokal auf dem Host erstellen können, indem Sie Docker, Kubernetes oder Windows PowerShell über Plug-Ins verwenden, die mit dem Windows Host Network Service \( HNS kommunizieren \) . Sie können Cluster Netzwerke mit mehreren \- Knoten mithilfe von Orchestrierungs Systemen auf höherer Ebene erstellen und verwalten, indem Sie über einen lokalen Agent mit dem HNS eines Knotens kommunizieren.

### <a name="windows-internet-name-service-wins"></a>[Windows Internet Name Service (WINS)](technologies/wins/wins-top.md)

Windows Internet Name Service (WINS) ist ein Legacy Dienst für die Registrierung und Auflösung von Computernamen, der NetBIOS-Namen von Computern IP-Adressen zuordnet. Die Verwendung von DNS wird bei Verwendung von WINS empfohlen.

## <a name="additional-resources"></a>Weitere Ressourcen

Netzwerkressourcen für ältere Betriebssysteme als Windows Server 2016 sind an den folgenden Orten verfügbar.

- Windows Server 2012 und Windows Server 2012 R2 [Übersicht über Netzwerke](https://technet.microsoft.com/library/hh831357.aspx)
- Windows Server 2008 und Windows Server 2008 R2 [Netzwerke](https://technet.microsoft.com/library/cc753940)
- Windows Server 2003 [Windows Server 2003/2003 R2-deaktivierter Inhalt](https://www.microsoft.com/download/details.aspx?id=53314)
