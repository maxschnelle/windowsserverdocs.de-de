---
title: Networking
description: Dieses Thema enthält eine Übersicht über die Software Defined Networking- und Netzwerkplattform-Technologien, die in Windows Server2016 verfügbar sind.
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6066840"
---
# Networking

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere anderen [Windows Server-Bibliotheken](/previous-versions/windows/) auf docs.microsoft.com an. Sie können auch nach bestimmten Informationen auf [dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions) .

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> Networking ist ein wesentlicher Bestandteil der SDDC-Plattform (Software Defined Datacenter), und Windows Server 2016 stellt neue und verbesserte SDN-Technologien (Software Defined Networking) bereit, die Ihnen den Wechsel zu einer vollständig implementierten SDDC-Lösung für Ihre Organisation erleichtern.

Wenn Sie Netzwerke als softwaredefinierte Ressource verwalten, brauchen Sie Anforderungen einer Anwendung an die Infrastruktur nur einmal zu beschreiben und können dann auswählen, wo die Anwendung ausgeführt wird – lokal oder in der Cloud. 

Diese Konsistenz bedeutet, dass die Anwendungen sich jetzt leichter skalieren und nahtlos überall mit der gleichen Zuverlässigkeit hinsichtlich Sicherheit, Leistung, Dienstqualität und Verfügbarkeit ausführen lassen.

>[!Note]
> Weitere Informationen zum Download von Windows Server finden Sie unter [Windows Server-Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview).

Mit Windows Server 2016 werden die folgenden neuen Netzwerktechnologien bereitgestellt:

- Software-Defined Networking: Netzwerkcontroller bieten eine zentrale, programmierbare Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum. Netzwerkcontroller ermöglichen Ihnen, durch Virtualisierung von Netzwerkfunktionen mühelos virtuelle Computer \(VMs\) für den Softwarelastenausgleich \(SLB\) zur Optimierung von Datenverkehrslasten im Netzwerk für Ihre Mandanten bereitzustellen, sowie RAS-Gateways, um Mandanten die benötigten Verbindungsoptionen zwischen dem Internet, lokalen und Cloudressourcen an die Hand zu geben. Mithilfe von Netzwerkcontrollern könne Sie zudem Datacenter Firewall auf virtuellen Computern und Hyper-V-Hosts verwalten.

- Netzwerkplattform: Dank neuer Features für vorhandene Netzwerkplattform-Technologien können Sie mithilfe einer DNS-Richtlinie die DNS-Serverantworten auf Abfragen anpassen, eine konvergente NIC verwenden, die kombinierten Remote Direct Memory Access- \(RDMA\) und Ethernetverkehr unterstützt, Switch Embedded Teaming nutzen \(SET\), um virtuelle Hyper-V-Switches zu erstellen, die mit RDMA-NICs verbunden sind, und IP-Adressverwaltung \(IPAM\) einsetzen, um DNS-Zonen und -Server sowie DHCP- und IP-Adressen zu verwalten.

Weitere Informationen finden Sie unter [Von Windows Server unterstützte Netzwerkszenarien](windows-server-supported-networking-scenarios.md).

Die folgenden Abschnitte enthalten Informationen zu den SDN-Technologien und Netzwerkplattformtechnologien.

## Software Defined Networking-Technologien

### [Software Defined Networking &#40;SDN&#41;](sdn/software-defined-networking.md)

Dieses Thema enthält Informationen zu den SDN-Technologien, die in Windows Server, System Center und Microsoft Azure bereitgestellt werden.

>[!NOTE]
>Für Hyper-V-Hosts und virtuelle Computer \(VMs\), auf denen SDN-Infrastrukturserver ausgeführt werden, z.B. Netzwerkcontroller und Lastenausgleichsknoten, müssen Sie Windows Server2016 Datacenter Edition installieren. Für Hyper-V-Hosts, auf denen sich nur VMs für Mandantenarbeitslast befinden, die mit SDN\-gesteuerten Netzwerken verbunden sind, genügt die Standardedition von Windows Server2016.

### [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
Dieses Handbuch enthält Anweisungen zum Bereitstellen eines Netzwerkcontrollers mit virtuellen Netzwerken und Gateways in einer Testumgebung.

### [Netzwerkcontroller](sdn/technologies/network-controller/Network-Controller.md)

Netzwerkcontroller bietet die Möglichkeit einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum.

### [Software Load Balancing &#40;SLB&#41; für SDN](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

Clouddienstanbieter \(CSPs\) und Unternehmen, die Software Defined Networking (SDN) in Windows Server 2016 bereitstellen, können mithilfe von Softwarelastenausgleich \(SLB\) Netzwerkdatenverkehr von Mandanten und Mandantenkunden gleichmäßig auf Ressourcen im virtuellen Netzwerk verteilen. Windows Server-SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen.

### [RAS-Gateway für SDN](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

RAS-Gateway, ein softwarebasierter, mehrinstanzenfähiger, BGP-fähiger (Border Gateway Protocol) Router in Windows Server 2016, wurde für Clouddienstanbieter \(CSPs\) und Unternehmen entwickelt, die virtuelle Netzwerke mit mehreren Mandanten mithilfe von Hyper-V-Netzwerkvirtualisierung hosten. 

### [Netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

In softwaredefinierten Rechenzentren werden Netzwerkfunktionen, die von Hardware \(wie Komponenten für den Lastenausgleich, Firewalls, Routern, Switches usw.\) ausgeführt werden, zunehmend als virtuelle Appliances virtualisiert. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung.

### [Rechenzentrumsfirewall: Übersicht](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

Datacenter Firewall ist eine statusbehaftete, mehrinstanzenfähige 5-Tupel-Firewall (Protokoll, Portnummer von Quelle und Ziel sowie IP-Adresse von Quelle und Ziel), die auf der Vermittlungsschicht implementiert ist.

## <a name="bkmk_networking"></a>Netzwerktechnologien

Die folgende Tabelle enthält Links für einige der Netzwerktechnologien in Windows Server 2016.

### [Neues zu Networking](../networking/What-s-New-in-Networking.md)

In den folgenden Abschnitten finden Sie neue Netzwerktechnologien und neue Features für vorhandene Technologien in Windows Server 2016.

### [BranchCache](branchcache/BranchCache.md)

BranchCache ist eine Technologie zur \(WAN\)-Bandbreitenoptimierung. Um die WAN-Bandbreite zu optimieren, wenn Benutzer auf Inhalte von Remoteservern zugreifen, ruft BranchCache Inhalte von Inhaltsservern in der Hauptniederlassung oder gehosteten Cloudinhaltsservern ab und speichert sie an Filialstandorten zwischen, sodass Clientcomputer in Filialen lokal und nicht über das WAN auf diese Inhalte zugreifen können.

### [Handbuch für das Kernnetzwerk von Windows Server 2016](core-network-guide/core-network-guide-windows-server.md)

Erfahren Sie, wie Sie ein Windows Server-Netzwerk mit dem Handbuch für das Kernnetzwerk bereitstellen und Funktionen zur Netzwerkbereitstellung mit den Begleitanleitungen zum Handbuch für das Kernnetzwerk hinzufügen.

### [DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess ermöglicht die Verbindung von Remotebenutzern mit Netzwerkressourcen der Organisation. 

Die DirectAccess-Dokumentation finden Sie nun im Windows Server2016-Inhaltsverzeichnis im Abschnitt [Remote Access und Server-Management](https://docs.microsoft.com/windows-server/remote/) unter [Remote Access](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access). Weitere Informationen finden Sie unter [DirectAccess](../remote/remote-access/directaccess/DirectAccess.md).

### [Domain Name System &#40;DNS&#41;](dns/dns-top.md)

Domain Name System \(DNS\) ist eine der branchenüblichen Suiten von Protokollen, die TCP/IP umfassen. Zusammen stellen DNS-Client und DNS-Server den Computern und Benutzern einen Namensauflösungsdienst für die Zuordnung von Computernamen zu IP-Adressen bereit.

### [Dynamic Host Configuration Protocol &#40;DHCP&#41;](technologies/dhcp/dhcp-top.md)

Dynamic Host Configuration-Protokoll \(DHCP\) ist ein Client/Server-Protokoll, das einem Internetprotokollhost automatisch seine IP-Adresse und andere Konfigurationsinformationen bereitstellt, z.B. die Subnetzmaske und das Standardgateway.

### [Hyper-V-Netzwerkvirtualisierung](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

Hyper-V-Netzwerkvirtualisierung \(HNV\) ermöglicht die Virtualisierung von Kundennetzwerken auf der Basis einer gemeinsam genutzten physischen Netzwerkinfrastruktur.

### [Virtueller Hyper-V-Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Beim virtuellen Hyper-V-Switch handelt es sich um einen softwarebasierten Schicht-2-Ethernet-Netzwerkswitch, der im Hyper-V-Manager verfügbar ist, wenn Sie die Hyper-V-Serverrolle installieren. Der Switch umfasst programmgesteuert verwaltete und erweiterbare Funktionen zum Verbinden virtueller Computer mit virtuellen Netzwerken und dem physischen Netzwerk. Außerdem bietet Hyper-V Virtual Switch Richtlinienerzwingung für Sicherheits-, Isolations- und Dienststufen. 

Die Hyper-V Virtual Switch-Dokumentation finden Sie nun im Abschnitt **Virtualisierung** des Windows Server2016-Inhaltsverzeichnisses. Weitere Informationen finden Sie unter [Hyper-V Virtual Switch](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).

### [IP-Adressverwaltung &#40;IPAM&#41;](technologies/ipam/ipam-top.md)

Bei der IP-Adressverwaltung \(IPAM\) handelt es sich um eine integrierte Suite von Tools mit einer umfassenden Benutzeroberfläche für die durchgängige Planung, Bereitstellung, Verwaltung und Überwachung Ihrer IP-Adresseninfrastruktur. IPAM ermittelt IP-Adresseninfrastrukturserver- und Domain Name System \(DNS\)-Server in Ihrem Netzwerk automatisch und ermöglicht, sie über eine zentrale Oberfläche zu verwalten.

### [Netzwerklastenausgleich](technologies/Network-Load-Balancing.md)

Beim Netzwerklastenausgleich \(NLB\) wird der Datenverkehr mithilfe des TCP/IP-Netzwerkprotokolls über mehrere Server verteilt. Für Bereitstellungen ohne SDN stellt NLB sicher, dass statusfreie Anwendungen, beispielsweise Webserver, auf denen Internetinformationsdienste \(IIS\) ausgeführt werden, durch Hinzufügen zusätzlicher Server bei zunehmender Last skalierbar sind.

### [High-Performance Networking](technologies/hpn/hpn-top.md)

Netzwerk-Offload- und Optimierungstechnologien in Windows Server 2016 umfassen Software Only (SO)-Features und -Technologien, integrierte Software- und Hardware (SH)-Features und -Technologien sowie Hardware Only (HO)-Features und -Technologien.

Für Offload- und Optimierungstechnologien steht folgende Dokumentation zur Verfügung:

- [Converged Network Interface Card (NIC) Configuration Guide](technologies/conv-nic/cnic-top.md)
- [Data Center Bridging (DCB)](technologies/dcb/dcb-top.md)
- [Virtual Receive Side Scaling (vRSS)](technologies/vrss/vrss-top.md)


### [Netzwerkrichtlinienserver](technologies/nps/nps-top.md)

Mit einem Netzwerkrichtlinienserver (Network Policy Server, NPS) können Sie organisationsweite Netzwerkzugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen.

### [Network Shell (Netsh)](technologies/netsh/netsh.md)

Das Networking-Dienstprogramm Network Shell \(netsh\) dient zum Verwalten von Netzwerktechnologien in Windows Server2016 und Windows10.

### [Leistungsoptimierung für das Netzwerksubsystem](technologies/network-subsystem/net-sub-performance-top.md)

In diesem Thema finden Sie Informationen zur Auswahl des geeigneten Netzwerkadapters für Ihre Serverarbeitsauslastung, zu Netzwerkschnittstellen, Netzwerk-Leistungsindikatoren, Netzwerkadaptern zur Leistungsoptimierung und über zugehörige Netzwerktechnologien wie z.B. Receive Side Scaling \(RSS\) und Receive Side Coalescing \(RSC\).

### [NIC Teaming](technologies/nic-teaming/NIC-Teaming.md)

NIC Teaming ermöglicht, physische Ethernet-Netzwerkadapter in einem oder mehreren softwarebasierten virtuellen Netzwerkadaptern zusammenzufassen. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.

### [Quality of Service (QoS)-Richtlinie](technologies/qos/qos-policy-top.md)

Sie können die QoS-Richtlinie als zentralen Punkt für die Verwaltung der Netzwerkbandbreite in Ihrer gesamten Active Directory-Infrastruktur verwenden, indem Sie QoS-Profile erstellen, deren Einstellungen mit Gruppenrichtlinien verteilt werden.

### [Remote Access](../remote/remote-access/remote-access.md)

Sie können Remote Access-Technologien wie DirectAccess und Virtual Private Networking \(VPN \) verwenden, um externen Mitarbeitern Verbindungen zu internen Netzwerkressourcen bereitzustellen. Zudem können Sie Remote Access für LAN \(LAN\)-Routing und Web Application Proxy verwenden. Dieser Proxy bietet Reverseproxyfunktion für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können.

Die Dokumentation für Remote Access finden Sie nun im Abschnitt [Remote Access und Serververwaltung](https://docs.microsoft.com/windows-server/remote/) des Windows Server 2016-Inhaltsverzeichnisses. Weitere Informationen finden Sie unter [Remote Access](../remote/remote-access/remote-access.md).

Weitere Informationen zu Web Application Proxy (ein Rollendienst der Remote Access-Serverrolle) finden Sie unter [Web Application Proxy in Windows Server2016](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server).

### [Virtual Private Networking (VPN)](../remote/remote-access/vpn/vpn-top.md)

In Windows Server 2016 ist **DirectAccess und VPN**ein Rollendienst der **Remote Access**-Serverrolle.

Wenn Sie Remote Access als VPN-Server installieren, können Sie Virtual Private Networking \(VPN\) verwenden, um Ihren externen Mitarbeitern Verbindungen mit dem Netzwerk Ihrer Organisation über das Internet bereitzustellen, wobei die Informationen durch verschlüsselte Verbindungen geschützt sind.

Mit Windows Server 2016 Remote Access VPN – und Windows10-Clientcomputern – können Sie nun Always On VPN bereitstellen. Mit Always On VPN verwalten Sie Remote-VPN-Clients, die immer verbunden sind, um externen Mitarbeitern zusätzlichen Komfort bieten, weil sich diese nicht mehr manuell über VPN mit dem Netzwerk Ihres Unternehmens verbinden oder von diesem trennen müssen.

Weitere Informationen finden Sie unter [Remote Access Always On VPN Deployment Guide for Windows Server 2016 and Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

>[!NOTE]
>Die VPN-Dokumentation finden Sie nun im Windows Server2016-Inhaltsverzeichnis im Abschnitt [Remote Access und Server-Management](https://docs.microsoft.com/windows-server/remote/) unter [Remote Access](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access).

Weitere Informationen über VPN finden Sie unter [Virtual Private Networking (VPN)](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-top).

### [Windows Container Networking](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/container-networking)

Windows Container Networking ermöglicht das Erstellen und Verwalten von Netzwerken zum Verbinden von Containerendpunkten auf Windows 10- und Windows Server-Hosts mithilfe von standardmäßigen Branchentools und Workflows. Windows Container Networking unterstützt mehrere Topologien, z.B. private, flat-L2 und routed-L3.

Zudem werden Overlays unterstützt, die Sie lokal auf dem Host mithilfe von Docker, Kubernetes oder Windows PowerShell über Plug-Ins erstellen können, die mit dem Windows Host Networking Service \(HNS\) kommunizieren. Sie können Multiknoten-Clusternetzwerke über Orchestrierungssysteme höherer Ebene erstellen und verwalten, indem Sie über einen lokalen Agenten mit dem HNS jedes Knotens kommunizieren.

### [Windows Internet Name Service (WINS)](technologies/wins/wins-top.md)

Windows Internet Name Service (WINS) ist ein älterer Registrierungs- und Auflösungsdienst für Computernamen, der einem Computer-NetBIOS-Namen eine IP-Adresse zuordnet. Es wird empfohlen, DNS statt WINS zu verwenden.

## Weitere Ressourcen

Networking-Ressourcen für Betriebssysteme vor Windows Server 2016 stehen unter den folgenden Links zur Verfügung:

- Windows Server 2012 und Windows Server 2012 R2 [Übersicht über Netzwerke](https://technet.microsoft.com/library/hh831357.aspx)
- Windows Server 2008 und Windows Server 2008 R2 [Networking](https://technet.microsoft.com/library/cc753940)
- Windows Server 2003 [Windows Server2003/2003 R2 – veraltete Inhalte ](https://www.microsoft.com/download/details.aspx?id=53314)
