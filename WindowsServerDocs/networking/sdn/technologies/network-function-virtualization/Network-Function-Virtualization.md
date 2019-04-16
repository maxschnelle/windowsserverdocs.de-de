---
title: Netzwerkfunktionsvirtualisierung
description: In diesem Thema können Sie Informationen zu Netzwerkfunktionsvirtualisierung, dem Sie zur Bereitstellung von virtuellen Netzwerk Appliances wie Datacenter Firewall, mehrinstanzenfähige RAS-Gateway und Software Load Balancing (SLB) in Windows Server 2016 können.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79df3bbe-48fd-4eff-8df6-35f6317566f3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7caa9eef42cb7ab95a13d64c1dcd3639b1132eb3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-function-virtualization"></a>Netzwerkfunktionsvirtualisierung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema Netzwerkfunktionsvirtualisierung, Informationen zu dem Sie zur Bereitstellung von virtuellen Netzwerk Appliances wie Datacenter Firewall, mehrinstanzenfähige RAS-Gateway und den Softwarelastenausgleich \(SLB\) können zur Vereinheitlichung \(MUX\).
  
>[!NOTE]  
>Zusätzlich zu diesem Thema ist die folgende Dokumentation zum Netzwerkfunktionsvirtualisierung verfügbar.  
> - [Datacenter Firewall (Übersicht)](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)  
> - [RAS-Gateway für SDN](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
> - [Softwarelastenausgleich (SLB) für SDN](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)  
  
In der heutigen Software sind definierte Rechenzentren, Netzwerkfunktionen, die von Hardware (z. B. zum Lastenausgleich, Firewalls, Routern, Switches usw.) ausgeführt werden, zunehmend als virtuelle Appliances virtualisiert wird. Diese "netzwerkfunktionsvirtualisierung" ist ein natürlicher Fortschritt der Servervirtualisierung und Netzwerkvirtualisierung. Virtuelle Appliances sind schnell neu aufkommender und erstellen einen völlig neuen Markt. Generierung von Interesse und Dynamik in beiden Virtualisierungsplattformen und cloud-Dienste weiter.  
  
Microsoft hat ein eigenständiges Gateway als virtuelle Appliance ab Windows Server 2012 R2. Weitere Informationen finden Sie unter [Windows Server-Gateway](https://technet.microsoft.com/library/dn313101.aspx). Jetzt wird weiterhin mit Windows Server 2016 Microsoft erweitern und bei der Netzwerk-Funktion Virtualisierung investieren.  
  
## <a name="virtual-appliance-benefits"></a>Vorteile der virtuellen Anwendung  
Eine virtuelle Anwendung ist dynamisch und ändern, da es sich um eine virtuelle Maschine vorbereitete, benutzerdefinierte ist einfach. Es kann eine oder mehrere virtuelle Maschinen verpackt, aktualisiert und als Einheit verwaltet werden. Zusammen mit Software-defined Networking (SDN), erhalten Sie die Mobilität und Flexibilität, die in der heutigen cloudbasierten Infrastruktur erforderlich. Zum Beispiel:  
  
-   SDN zeigt das Netzwerk als Ressource in einem Pool zusammengefasste und dynamisch.  
  
-   SDN ermöglicht die Isolierung von Instanzen.  
  
-   SDN maximiert, Skalierung und Leistung.  
  
-   Virtuelle Appliances aktivieren Kapazität nahtlose Erweiterung und die Arbeitslast Mobilität.  
  
-   Virtuelle Appliances minimieren operative Komplexität.  
  
-   Virtuelle Appliances können Kunden einfach erwerben, bereitstellen und Verwalten von bereits integrierte Lösung.  
  
    -   Kunden können die virtuelle Anwendung ganz einfach an einer beliebigen Stelle in der Cloud verschieben.  
  
    -   Kunden können skalieren virtuelle Appliances oder nach unten dynamisch bei Bedarf.  
  
Weitere Informationen zu Microsoft-SDN finden Sie unter [Software Defined Networking](https://technet.microsoft.com/windows-server-docs/networking/sdn/software-defined-networking--sdn-).  
  
### <a name="what-network-functions-are-being-virtualized"></a>Welche Netzwerkfunktionen virtualisiert werden?  
Marketplace für virtualisierte Netzwerkfunktionen wächst schnell. Die folgenden Netzwerkfunktionen werden virtualisiert werden:  
  
-   **Sicherheit**  
  
    -   Firewall  
  
    -   Antivirus  
  
    -   DDoS (Distributed Denial of Service)  
  
    -   IP-Adressen/IDS (Erkennen von Eindringlingen Prevention System/Angriffserkennungssystem)  
  
-   **Anwendung/WAN-Optimierer**  
  
-   **Edge**  
  
    -   Standort-zu-Standort-gateway  
  
    -   L3-gateways  
  
    -   Router  
  
    -   Switches  
  
    -   NAT  
  
    -   Lastenausgleich (nicht unbedingt am Rand)  
  
    -   HTTP-proxy  
  
## <a name="why-microsoft-is-a-great-platform-for-virtual-appliances"></a>Warum ist Microsoft eine hervorragende Plattform für virtuelle appliances  
![Virtuelles Netzwerk-Stapel](../../../media/Network-Function-Virtualization/Microsoft-Network-Function-Virtualization.png)  
  
Die Microsoft-Plattform wurde so entwickelt, eine hervorragende Plattform zum Erstellen und Bereitstellen von virtuelle Appliances werden. Dies hat folgende Gründe:  
  
-   Microsoft bietet wichtige virtualisierten Netzwerk funktioniert mit Windows Server 2016.  
  
-   Sie können eine virtuelle Anwendung vom Anbieter Ihrer Wahl bereitstellen.  
  
-   Sie können bereitstellen, konfigurieren und verwalten Ihre virtuellen Geräte mit dem Microsoft-Netzwerk-Controller mit Windows Server 2016 enthalten. Weitere Informationen zu den Netzwerk-Controller, finden Sie unter [Netzwerkcontroller](../../../sdn/technologies/network-controller/Network-Controller.md).  
  
-   Hyper-V kann die Top-Gastbetriebssysteme gehostet werden, die Sie benötigen.  
  
## <a name="network-function-virtualization-in-windows-server-2016"></a>Netzwerkfunktionsvirtualisierung in Windows Server 2016  
  
### <a name="virtual-appliances-functions-provided-by-microsoft"></a>Virtuelle Appliances-Funktionen, die von Microsoft bereitgestellten  
Die folgenden virtuellen Geräte werden mit Windows Server 2016 bereitgestellt:  
  
**Softwarelastenausgleich**  
  
Ein Layer-4-Lastenausgleich bei einer Skalierung von Datacenter ausgeführt. Dies ist eine ähnliche Version des Azure-Lastenausgleichs, die bei einer Skalierung von in der Azure-Umgebung bereitgestellt wurde. Weitere Informationen zu den Microsoft Software Load Balancers, finden Sie unter [Software Load Balancing (SLB) für SDN](https://technet.microsoft.com/library/mt632286.aspx). Weitere Informationen zu Microsoft Azure Netzwerklastenausgleich-Dienste finden Sie unter [Microsoft Azure Netzwerklastenausgleich-Dienste](https://azure.microsoft.com/blog/2014/04/08/microsoft-azure-load-balancing-services/).  
  
**Gateway**. RAS-Gateway bietet alle Kombinationen der folgenden Gatewayfunktionen.  
  
-   **Standort-zu-Standort-gateway**  
  
    RAS-Gateway bietet einen Border Gateway Protocol (BGP)-fähig, mehrinstanzenfähigen Gateway Mandanten zugreifen und ihre Ressourcen über Standort-zu-Standort-VPN-Verbindungen von Remotestandorten verwalten und, mit der Fluss von Netzwerkdatenverkehr zwischen virtuellen Ressourcen in der Cloud und Mandanten physischen Netzwerken. Weitere Informationen zu den RAS-Gateway, finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](https://technet.microsoft.com/library/mt631692.aspx) und [RAS-Gateway](https://technet.microsoft.com/library/mt626650.aspx).  
  
-   **Weiterleitungsgateway**  
  
    RAS-Gateway leitet den Datenverkehr zwischen virtuellen Netzwerken und dem hostenden Anbieter physischen Netzwerk. Z. B. wenn Mandanten eine oder mehrere virtuelle Netzwerke erstellen und Zugriff auf freigegebene Ressourcen auf dem physischen Netzwerk an den Hostinganbieter benötigen, kann das weiterleitungsgateway weiterleiten Datenverkehr zwischen dem virtuellen Netzwerk und dem physischen Netzwerk ermöglichen Benutzern, auf dem virtuellen Netzwerk mit den Diensten, die sie benötigen. Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](https://technet.microsoft.com/library/mt631692.aspx) und [RAS-Gateway](https://technet.microsoft.com/library/mt626650.aspx).  
  
-   **GRE-Tunneling-gateways**  
  
    GRE-basierte Tunnel ermöglichen Verbindungen zwischen virtuellen mandantennetzwerken und externen Netzwerken. Da das GRE-Protokoll Lightweight und Unterstützung für GRE auf den meisten Netzwerkgeräten verfügbar ist, wird es zur idealen Lösung tunneling, in denen keine datenverschlüsselung erforderlich ist. GRE-Unterstützung für Standort-zu-Standort (S2S)-Tunnel behebt das Problem der Weiterleitung zwischen virtuellen mandantennetzwerken und externen mandantennetzwerken über ein mehrinstanzenfähiges Gateway. Weitere Informationen zu GRE-Tunnel, finden Sie unter [GRE-Tunneling in Windows Server 2016](https://technet.microsoft.com/library/dn765485.aspx).  
  
**Routing Steuerelement Ebene mit BGP**  
  
Hyper-V-Netzwerkvirtualisierung (HNV)-Routing-Steuerelement ist die logische, zentrale Entität in der Steuerelement-Ebene führt alle Kundenadresse Ebene Routen und dynamisch lernt und aktualisiert anschließend die verteilte RAS-Gateway-Router im virtuellen Netzwerk. Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](https://technet.microsoft.com/library/mt631692.aspx) und [RAS-Gateway](https://technet.microsoft.com/library/mt626650.aspx).  
  
**Verteilte Multi-Tenant-firewall**  
  
Die Firewall schützt die Netzwerkebene von virtuellen Netzwerken. Die Richtlinien werden zur SDN-vSwitch-Port für jeden Mandanten VM erzwungen. Sie schützt alle-Datenverkehr fließt: OST-West und Nord-Süd. Die Richtlinien werden über das mandantenportal abgelegt und Netzwerkcontroller sie für alle anwendbaren Hosts verteilt. Weitere Informationen über die verteilte Multi-Tenant-Firewall finden Sie unter [Datacenter Firewall (Übersicht)](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).  
  


