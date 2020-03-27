---
title: Netzwerk
description: Dieses Thema enthält eine Übersicht über die Software Defined Networking- und Netzwerkplattform-Technologien, die in Windows Server 2016 verfügbar sind.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: 05/08/2018
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: lizross
author: eross-msft
ms.localizationpriority: medium
ms.openlocfilehash: 833f1681af16b4e79a28383462a3471b3bc08f52
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319365"
---
# <a name="networking"></a>Netzwerk

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

       [!TIP]
        Looking for information about older versions of Windows Server? Check out our other [Windows Server libraries](/previous-versions/windows/) on docs.microsoft.com. You can also [search this site](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions) for specific information.

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> Das Netzwerk ist ein grundlegender Bestandteil des Software definierten Rechenzentrums \(SDDC\) Plattform, und Windows Server 2016 bietet neue und verbesserte Software-Defined Networking \(Sdn\)-Technologien, die Sie bei der Umstellung auf eine vollständig erkannte SDDC-Lösung für Ihre Organisation unterstützen.

Wenn Sie Netzwerke als softwaredefinierte Ressource verwalten, können Sie die Infrastrukturanforderungen einer Anwendung einmalig beschreiben und dann auswählen, wo die Anwendung ausgeführt wird (lokal oder in der Cloud). 

Diese Konsistenz bedeutet, dass die Anwendungen sich jetzt leichter skalieren und nahtlos überall mit der gleichen Zuverlässigkeit hinsichtlich Sicherheit, Leistung, Dienstqualität und Verfügbarkeit ausführen lassen.

>[!Note]
> Weitere Informationen zum Download von Windows Server finden Sie unter [Windows Server-Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview).

Windows Server 2016 fügt die folgenden neuen Netzwerktechnologien ein:

- Software-Defined Networking: Netzwerkcontroller bieten eine zentrale, programmierbare Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum. Mit dem Netzwerk Controller können Sie die netzwerkfunktionsvirtualisierung verwenden, um virtuelle Maschinen \(virtuellen Computern bereitzustellen\) für den Software Lastenausgleich \(SLB-\), um den Netzwerk Datenverkehr für Ihre Mandanten zu optimieren, und RAS-Gateways, um Mandanten die erforderlichen Konnektivitätsoptionen zwischen Internet-, lokalen und cloudressourcen zu Mithilfe von Netzwerkcontrollern könne Sie zudem Datacenter Firewall auf virtuellen Computern und Hyper-V-Hosts verwalten.

- Netzwerkplattform: mithilfe neuer Features für vorhandene Netzwerk Plattformtechnologien können Sie die DNS-Server Antworten mithilfe der DNS-Richtlinie an Abfragen anpassen. verwenden Sie eine konvergierte NIC, die den kombinierten Remote Zugriff auf den direkten Speicher \(RDMA-\) und Ethernet-Datenverkehr verarbeitet. verwenden Sie Switch Embedded Teaming \(\), um virtuelle Hyper-V-Switches zu erstellen, die mit RDMA-NICs verbunden sind, und verwenden Sie die IP-Adressverwaltung \(IPAM-\), um DNS-Zonen und-Server

Weitere Informationen finden Sie unter [Von Windows Server unterstützte Netzwerkszenarien](windows-server-supported-networking-scenarios.md).

Die folgenden Abschnitte enthalten Informationen zu den SDN-Technologien und Netzwerkplattformtechnologien.

## <a name="software-defined-networking-technologies"></a>Software-Defined Networking-Technologien

### <a name="software-defined-networking-40sdn41"></a>[SDN des &#40;Software-Defined Networking&#41;](sdn/software-defined-networking.md)

Dieses Thema enthält Informationen zu den SDN-Technologien, die in Windows Server, System Center und Microsoft Azure bereitgestellt werden.

>[!NOTE]
>Für Hyper-V-Hosts und virtuelle Computer \(VMS\), auf denen Sdn-Infrastruktur Server ausgeführt werden, z. b. Netzwerk Controller und Software Lastenausgleich-Knoten, müssen Sie Windows Server 2016 Datacenter Edition installieren. Für Hyper-V-Hosts, die nur Mandanten-Arbeits Auslastungs-VMS enthalten, die mit Sdn-\-kontrollierten Netzwerken verbunden sind, können Sie Windows Server 2016 Standard Edition ausführen.

### <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>[Bereitstellen einer Software definierten Netzwerkinfrastruktur mithilfe von Skripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
Dieses Handbuch enthält Anweisungen zum Bereitstellen eines Netzwerkcontrollers mit virtuellen Netzwerken und Gateways in einer Testumgebung.

### <a name="network-controller"></a>[Netzwerkcontroller](sdn/technologies/network-controller/Network-Controller.md)

Netzwerkcontroller bietet die Möglichkeit einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum.

### <a name="software-load-balancing-40slb41-for-sdn"></a>[Software Lastenausgleich &#40;-&#41; SLB für Sdn](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

Clouddienstanbieter \(CSPs\) und Unternehmen, die Software-Defined Networking (SDN) in Windows Server 2016 bereitstellen, können den Software Lastenausgleich \(SLB-\) verwenden, um den Netzwerk Datenverkehr von Mandanten und Mandanten Kunden gleichmäßig auf die Ressourcen des virtuellen Netzwerks Windows Server-SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen.

### <a name="ras-gateway-for-sdn"></a>[RAS-Gateway für SDN](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

RAS-Gateway, ein softwarebasierter, mehr Instanzen fähiger Border Gateway Protocol \(BGP\) fähigen Router in Windows Server 2016, ist für clouddienstanbieter \(CSPs\) und Unternehmen konzipiert, die mehrere virtuelle Mandanten Netzwerke mithilfe der Hyper-V-Netzwerkvirtualisierung hosten. 

### <a name="network-function-virtualization"></a>[Netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

In Software definierten Rechenzentren werden von Hardware Geräten ausgeführte Netzwerkfunktionen \(z. b. Lasten Ausgleichs Module, Firewalls, Router, Switches usw.\) zunehmend als virtuelle Geräte virtualisiert. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung.

### <a name="datacenter-firewall-overview"></a>[Übersicht über Datacenter Firewall](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

Datacenter Firewall ist eine statusbehaftete, mehrinstanzenfähige 5-Tupel-Firewall (Protokoll, Portnummer von Quelle und Ziel sowie IP-Adresse von Quelle und Ziel), die auf der Vermittlungsschicht implementiert ist.

## <a name="networking-technologies"></a><a name="bkmk_networking"></a>Netzwerktechnologien

Die folgende Tabelle enthält Links für einige der Netzwerktechnologien in Windows Server 2016.

### <a name="whats-new-in-networking"></a>[Neues bei Netzwerken](../networking/What-s-New-in-Networking.md)

In den folgenden Abschnitten finden Sie neue Netzwerktechnologien und neue Features für vorhandene Technologien in Windows Server 2016.

### <a name="branchcache"></a>[BranchCache](branchcache/BranchCache.md)

BranchCache ist ein Wide Area Network \(WAN\) Bandbreiten Optimierungs Technologie. Um die WAN-Bandbreite zu optimieren, wenn Benutzer auf Inhalte von Remoteservern zugreifen, ruft BranchCache Inhalte von Inhaltsservern in der Hauptniederlassung oder gehosteten Cloudinhaltsservern ab und speichert sie an Filialstandorten zwischen, sodass Clientcomputer in Filialen lokal und nicht über das WAN auf diese Inhalte zugreifen können.

### <a name="core-network-guide-for-windows-server-2016"></a>[Handbuch zum Hauptnetzwerk für Windows Server 2016](core-network-guide/core-network-guide-windows-server.md)

Erfahren Sie, wie Sie ein Windows Server-Netzwerk mit dem Handbuch für das Kernnetzwerk bereitstellen und Funktionen zur Netzwerkbereitstellung mit den Begleitanleitungen zum Handbuch für das Kernnetzwerk hinzufügen.

### <a name="directaccess"></a>[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess ermöglicht die Verbindung von Remotebenutzern mit Netzwerkressourcen der Organisation. 

Die DirectAccess-Dokumentation finden Sie nun im Windows Server 2016-Inhaltsverzeichnis im Abschnitt [Remote Access und Server-Management](https://docs.microsoft.com/windows-server/remote/) unter [Remote Access](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access). Weitere Informationen finden Sie unter [DirectAccess](../remote/remote-access/directaccess/DirectAccess.md).

### <a name="domain-name-system-40dns41"></a>[DNS &#40;-Domain Name System&#41;](dns/dns-top.md)

Domain Name System \(DNS\) ist eine der branchenüblichen Suiten von Protokollen, die TCP/IP umfassen, und zusammen stellen DNS-Client und DNS-Server Computern und Benutzern einen Namensauflösungsdienst für die Zuordnung von Computername zu IP-Adresse bereit.

### <a name="dynamic-host-configuration-protocol-40dhcp41"></a>[DHCP für das Dynamic &#40;Host Configuration-Protokoll&#41;](technologies/dhcp/dhcp-top.md)

Dynamic Host Configuration-Protokoll \(DHCP\) ist ein Client/Server-Protokoll, das einem Internetprotokollhost \(IP\) automatisch seine IP-Adresse und andere Konfigurationsinformationen bereitstellt, z. B. die Subnetzmaske und das Standardgateway.

### <a name="hyper-v-network-virtualization"></a>[Hyper-V-Netzwerkvirtualisierung](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-V-Netzwerkvirtualisierung \(HNV\) ermöglicht die Virtualisierung von Kunden Netzwerken über eine freigegebene physische Netzwerkinfrastruktur.

### <a name="hyper-v-virtual-switch"></a>[Virtueller Hyper-V-Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Beim virtuellen Hyper-V-Switch handelt es sich um einen softwarebasierten Schicht-2-Ethernet-Netzwerkswitch, der im Hyper-V-Manager verfügbar ist, wenn Sie die Hyper-V-Serverrolle installieren. Der Switch umfasst programmgesteuert verwaltete und erweiterbare Funktionen zum Verbinden virtueller Computer mit virtuellen Netzwerken und dem physischen Netzwerk. Außerdem bietet der virtuelle Hyper-V-Switch Richtlinienerzwingung für Sicherheits-, Isolations- und Dienststufen. 

Die Hyper-V Virtual Switch-Dokumentation finden Sie nun im Abschnitt **Virtualisierung** des Windows Server 2016-Inhaltsverzeichnisses. Weitere Informationen finden Sie unter [Hyper-V Virtual Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).

### <a name="ip-address-management-40ipam41"></a>[IP-Adress &#40;Verwaltung (IPAM)&#41;](technologies/ipam/ipam-top.md)

Bei der IP-Adressverwaltung \(IPAM\) handelt es sich um eine integrierte Suite an Tools, die die durchgängige Planung, Bereitstellung, Verwaltung und Überwachung Ihrer IP-Adresseninfrastruktur mit einer umfassenden Benutzeroberfläche ermöglichen. IPAM ermittelt IP-Adress Infrastruktur Server und Domain Name System \(DNS-\)-Server in Ihrem Netzwerk automatisch und ermöglicht es Ihnen, diese über eine zentrale Oberfläche zu verwalten.

### <a name="network-load-balancing"></a>[Netzwerklastenausgleich](technologies/Network-Load-Balancing.md)

Beim Netzwerklastenausgleich \(NLB\) wird der Datenverkehr mithilfe des TCP/IP-Netzwerkprotokolls über mehrere Server verteilt. Bei Nicht-SDN-Bereitstellungen stellt NLB sicher, dass statusfreie Anwendungen, beispielsweise Webserver, auf denen Internetinformationsdienste \(IIS\) ausgeführt werden, durch Hinzufügen zusätzlicher Server bei zunehmender Last skalierbar sind.

### <a name="high-performance-networking"></a>[Hochleistungs Netzwerke](technologies/hpn/hpn-top.md)

Netzwerk-Offload- und Optimierungstechnologien in Windows Server 2016 umfassen Software Only (SO)-Features und -Technologien, integrierte Software- und Hardware (SH)-Features und -Technologien sowie Hardware Only (HO)-Features und -Technologien.

Für Offload- und Optimierungstechnologien steht folgende Dokumentation zur Verfügung:

- [Konfigurations Handbuch für konvergierte Netzwerkschnittstellenkarten (NIC)](technologies/conv-nic/cnic-top.md)
- [Data Center Bridging (DCB)](technologies/dcb/dcb-top.md)
- [Virtual Receive Side Scaling (vRSS)](technologies/vrss/vrss-top.md)


### <a name="network-policy-server"></a>[Netzwerk Richtlinien Server](technologies/nps/nps-top.md)

Mit einem Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie organisationsweite Netzwerkzugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen.

### <a name="network-shell-netsh"></a>[Network Shell (Netsh)](technologies/netsh/netsh.md)

Sie können die Netzwerkshell \(Netsh\) Netzwerk Hilfsprogramm verwenden, um Netzwerktechnologien in Windows Server 2016 und Windows 10 zu verwalten.

### <a name="network-subsystem-performance-tuning"></a>[Leistungsoptimierung des Netzwerk Subsystems](technologies/network-subsystem/net-sub-performance-top.md)

Dieses Thema enthält Informationen zum Auswählen des richtigen Netzwerkadapters für Ihre Server Arbeitsauslastung, zum Anordnen von Netzwerkschnittstellen, netzwerkbezogenen Leistungsindikatoren und zur Leistungsoptimierung von Netzwerkadaptern und zugehörigen Netzwerktechnologien, wie z. b. Empfangs seitige Skalierung \(RSS-\), Empfang von parallelen Zusammenstellungen \(RSC\)und anderen.

### <a name="nic-teaming"></a>[NIC-Teamvorgang](technologies/nic-teaming/NIC-Teaming.md)

NIC-Teaming ermöglicht Ihnen, physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter zu gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.

### <a name="quality-of-service-qos-policy"></a>[Quality of Service (QoS)-Richtlinie](technologies/qos/qos-policy-top.md)

Sie können die QoS-Richtlinie als zentralen Punkt für die Verwaltung der Netzwerkbandbreite in Ihrer gesamten Active Directory-Infrastruktur verwenden, indem Sie QoS-Profile erstellen, deren Einstellungen mit Gruppenrichtlinien verteilt werden.

### <a name="remote-access"></a>[Remotezugriff](../remote/remote-access/remote-access.md)

Sie können Remote Zugriffs Technologien wie DirectAccess und virtuelle private Netzwerke \(VPN-\) verwenden, um Remote Arbeitsthreads Verbindungen mit internen Netzwerkressourcen zu bieten. Außerdem können Sie den Remote Zugriff für lokales Netzwerk \(LAN\) Routing und für webanwendungsproxy verwenden. Dieser Proxy bietet Reverseproxyfunktion für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können.

Die Dokumentation für Remote Access finden Sie nun im Abschnitt [Remote Access und Serververwaltung](https://docs.microsoft.com/windows-server/remote/) des Windows Server 2016-Inhaltsverzeichnisses. Weitere Informationen finden Sie unter [Remote Access](../remote/remote-access/remote-access.md).

Weitere Informationen zu Web Application Proxy (ein Rollendienst der Remote Access-Serverrolle) finden Sie unter [Web Application Proxy in Windows Server 2016](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server).

### <a name="virtual-private-networking-vpn"></a>[Virtual Private Networking (VPN)](../remote/remote-access/vpn/vpn-top.md)

In Windows Server 2016 ist **DirectAccess und VPN**ein Rollendienst der **Remote Access**-Serverrolle.

Wenn Sie den Remote Zugriff als VPN-Server installieren, können Sie virtuelle private Netzwerke \(VPN-\) verwenden, um ihren Remote Mitarbeitern Verbindungen mit Ihrem Unternehmensnetzwerk über das Internet bereitzustellen, während gleichzeitig der Datenschutz mit verschlüsselten Verbindungen gewahrt bleibt.

Mit Windows Server 2016 Remote Access VPN – und Windows 10-Clientcomputern – können Sie nun Always On VPN bereitstellen. Mit Always On VPN verwalten Sie Remote-VPN-Clients, die immer verbunden sind, um externen Mitarbeitern zusätzlichen Komfort bieten, weil sich diese nicht mehr manuell über VPN mit dem Netzwerk Ihres Unternehmens verbinden oder von diesem trennen müssen.

Weitere Informationen finden Sie unter [Remote Access Always On VPN Deployment Guide for Windows Server 2016 and Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

>[!NOTE]
>Die VPN-Dokumentation finden Sie nun im Windows Server 2016-Inhaltsverzeichnis im Abschnitt [Remote Access und Server-Management](https://docs.microsoft.com/windows-server/remote/) unter [Remote Access](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access).

Weitere Informationen über VPN finden Sie unter [Virtual Private Networking (VPN)](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-top).

### <a name="windows-container-networking"></a>[Windows-Containernetzwerk](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/container-networking)

Windows Container Networking ermöglicht das Erstellen und Verwalten von Netzwerken zum Verbinden von Containerendpunkten auf Windows 10- und Windows Server-Hosts mithilfe von standardmäßigen Branchentools und Workflows. Windows Container Networking unterstützt mehrere Topologien, z. B. private, flat-L2 und routed-L3.

Unterstützt werden auch Überlagerungen, die Sie lokal auf dem Host erstellen können, indem Sie Docker, Kubernetes oder Windows PowerShell über Plug-Ins verwenden, die mit dem Windows-Host Netzwerkdienst \(HNS\)kommunizieren. Sie können Cluster Netzwerke mit mehreren\-Knoten mithilfe von Orchestrierungs Systemen auf höherer Ebene erstellen und verwalten, indem Sie über einen lokalen Agent mit dem HNS eines Knotens kommunizieren.

### <a name="windows-internet-name-service-wins"></a>[Windows Internet Name Service (WINS)](technologies/wins/wins-top.md)

Windows Internet Name Service (WINS) ist ein älterer Registrierungs- und Auflösungsdienst für Computernamen, der einem Computer-NetBIOS-Namen eine IP-Adresse zuordnet. Es wird empfohlen, DNS statt WINS zu verwenden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

Networking-Ressourcen für Betriebssysteme vor Windows Server 2016 stehen unter den folgenden Links zur Verfügung:

- Windows Server 2012 und Windows Server 2012 R2 [Übersicht über Netzwerke](https://technet.microsoft.com/library/hh831357.aspx)
- Windows Server 2008 und Windows Server 2008 R2 [Netzwerke](https://technet.microsoft.com/library/cc753940)
- Windows Server 2003 [Windows Server 2003/2003 R2-deaktivierter Inhalt](https://www.microsoft.com/download/details.aspx?id=53314)
