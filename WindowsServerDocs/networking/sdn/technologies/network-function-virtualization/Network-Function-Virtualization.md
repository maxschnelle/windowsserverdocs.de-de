---
title: Netzwerkfunktionsvirtualisierung
description: Sie können in diesem Thema verwenden, erfahren Sie Netzwerkfunktionsvirtualisierung, dem Sie virtuelle Netzwerkgeräte wie Datacenter Firewall, mehrinstanzenfähige RAS-Gateway und Software Load Balancing (SLB) im Windows Server 2016 bereitstellen können.
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
ms.openlocfilehash: 59474a13d1cbce6a607f025caf3f6c1b839c7eed
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884551"
---
# <a name="network-function-virtualization"></a>Netzwerkfunktionsvirtualisierung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Können Sie in diesem Thema erfahren Sie Netzwerkfunktionsvirtualisierung, dem Sie bereitzustellende virtuelle Netzwerkgeräte wie Datacenter Firewall, mehrinstanzenfähige RAS-Gateway und den Softwarelastenausgleich können \(SLB\) multiplexer \(MUX\).
  
>[!NOTE]  
>Zusätzlich zu diesem Thema ist die folgende Dokumentation zum Netzwerkfunktionsvirtualisierung verfügbar.  
> - [Rechenzentrumsfirewall: Übersicht](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)  
> - [RAS-Gateway für SDN](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
> - [Softwarelastenausgleich (SLB) für SDN](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)  
  
Heutige Software werden definierte Rechenzentren, Netzwerkfunktionen, die von Hardware (z. B. Load balancer, Firewalls, Routern, Switches usw.) ausgeführt werden zunehmend als virtuelle Appliances virtualisiert wird. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung. Virtuelle Geräte sind schnell entwickelt und erstellen einen völlig neuen Markt. Generieren von Interesse sind und erhalten Momentum auf beiden Virtualisierungsplattformen und cloud-Dienste weiterhin.  
  
Microsoft enthalten einen eigenständiges-Gateway als virtuelles Gerät mit Windows Server 2012 R2 ab. Weitere Informationen finden Sie unter [Windows Server Gateway](https://technet.microsoft.com/library/dn313101.aspx). Nun weiterhin mit Windows Server 2016 Microsoft zu erweitern, und investieren Sie in der Netzwerk-Funktion Virtualisierung Markt.  
  
## <a name="virtual-appliance-benefits"></a>Virtuelle Appliance-Vorteile  
Ein virtuelles Gerät ist dynamisch und ändern, da es sich um einen vorab erstellten, benutzerdefinierten virtuellen Computer ist einfach. Es kann eine oder mehrere virtuelle Computer enthalten, als eine Einheit verwaltet und aktualisiert sein. Zusammen mit Software-defined Networking (SDN), erhalten Sie die Agilität und Flexibilität, die in der heutigen cloudbasierte Infrastruktur erforderlich sind. Zum Beispiel:  
  
-   SDN stellt das Netzwerk als eine Ressource in einem Pool zusammengefasste und dynamische.  
  
-   SDN ermöglicht die Trennung von Mandanten.  
  
-   SDN maximiert, Skalierung und Leistung.  
  
-   Virtuelle Appliances Mobilität nahtlose Kapazität Erweiterung und der arbeitsauslastung.  
  
-   Virtuelle Geräte verringern die Komplexität des Betriebs.  
  
-   Virtuelle Geräte können Kunden ganz einfach erwerben, bereitstellen und Verwalten von vorab integrierten Lösungen.  
  
    -   Kunden können das virtuelle Gerät ganz einfach eine beliebige Stelle in der Cloud wechseln.  
  
    -   Kunden können virtuelle Appliances vertikal skalieren, oder dynamisch Sie je nach Bedarf.  
  
Weitere Informationen zu Microsoft-SDN finden Sie unter [Software Defined Networking](https://technet.microsoft.com/windows-server-docs/networking/sdn/software-defined-networking--sdn-).  
  
### <a name="what-network-functions-are-being-virtualized"></a>Welche Netzwerkfunktionen virtualisiert werden?  
Marketplace für virtualisierte Netzwerkfunktionen wächst schnell. Die folgenden Netzwerkfunktionen werden virtualisiert wird:  
  
-   **Sicherheit**  
  
    -   Firewall  
  
    -   Antivirensoftware  
  
    -   DDoS (Distributed Denial of Service)  
  
    -   -IPS/IDS (Intrusion Prevention System/Angriffserkennungssystem)  
  
-   **Anwendung/WAN-Optimierer**  
  
-   **Edge**  
  
    -   Standort-zu-Standort-gateway  
  
    -   L3-gateways  
  
    -   Router  
  
    -   Switches  
  
    -   NAT  
  
    -   Load Balancer (nicht unbedingt auf Edge-Ebene)  
  
    -   HTTP-proxy  
  
## <a name="why-microsoft-is-a-great-platform-for-virtual-appliances"></a>Warum ist Microsoft eine hervorragende Plattform für virtuelle Geräte  
![Virtuelles Netzwerk-Stapel](../../../media/Network-Function-Virtualization/Microsoft-Network-Function-Virtualization.png)  
  
Die Microsoft-Plattform wurde so entwickelt, eine hervorragende Plattform zum Erstellen und Bereitstellen von virtuellen Geräten werden. Hier ist die Antwort:  
  
-   Microsoft bietet wichtige virtualisierten Netzwerk-Funktionen mit Windows Server 2016.  
  
-   Sie können ein virtuelles Gerät vom Hersteller Ihrer Wahl bereitstellen.  
  
-   Sie können bereitstellen, konfigurieren und verwalten Ihre virtuellen Geräte mit dem Microsoft-Netzwerkcontroller die in Windows Server 2016 enthalten ist. Weitere Informationen zu den Netzwerkcontroller, finden Sie unter [Netzwerkcontroller](../../../sdn/technologies/network-controller/Network-Controller.md).  
  
-   Hyper-V kann es sich um die obersten Gastbetriebssysteme hosten, die Sie benötigen.  
  
## <a name="network-function-virtualization-in-windows-server-2016"></a>Funktion-Netzwerkvirtualisierung unter Windows Server 2016  
  
### <a name="virtual-appliances-functions-provided-by-microsoft"></a>Virtuelle Geräte, von Microsoft bereitgestellten Funktionen  
Die folgenden virtuellen Geräte werden mit Windows Server 2016 bereitgestellt:  
  
**Softwarelastenausgleich**  
  
Ein Layer-4-Lastenausgleich, der bedarfsorientiert Datencenter betreiben. Dies ist eine ähnliche Version der Azure Lastenausgleich, die bedarfsabhängig in der Azure-Umgebung bereitgestellt wurde. Weitere Informationen zu den Microsoft Software Load Balancer, finden Sie unter [Software Load Balancing (SLB) für SDN](https://technet.microsoft.com/library/mt632286.aspx). Weitere Informationen zu Microsoft Azure Load Balancing Services, finden Sie unter [Microsoft Azure-Lastenausgleichsdienste](https://azure.microsoft.com/blog/2014/04/08/microsoft-azure-load-balancing-services/).  
  
**Gateway**. RAS-Gateway enthält alle Kombinationen der folgenden Gateway-Funktionen.  
  
-   **Standort-zu-Standort-gateway**  
  
    RAS-Gateway stellt eine Border Gateway Protocol (BGP)-fähig, mehrinstanzenfähigen Gateway Mandanten zugreifen auf und verwalten ihre Ressourcen über Standort-zu-Standort-VPN-Verbindungen von Remotestandorten und, mit der Fluss von Netzwerkdatenverkehr zwischen virtuellen Ressourcen in der Cloud und Mandanten physischen Netzwerken. Weitere Informationen zum RAS-Gateway finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](https://technet.microsoft.com/library/mt631692.aspx) und [RAS-Gateway](https://technet.microsoft.com/library/mt626650.aspx).  
  
-   **Weiterleitungs-gateway**  
  
    RAS-Gateway leitet den Datenverkehr zwischen virtuellen Netzwerken und dem physischen Netzwerk. Z. B. wenn Mandanten eine oder mehrere virtuelle Netzwerke erstellen und Zugriff auf freigegebene Ressourcen auf dem physischen Netzwerk auf dem Hostinganbieter benötigen, kann die weiterleitungs-Gateway Datenverkehr zwischen dem virtuellen Netzwerk und dem physischen Netzwerk zu Benutzer, weiterleiten das virtuelle Netzwerk mit den Diensten, die sie benötigen. Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](https://technet.microsoft.com/library/mt631692.aspx) und [RAS-Gateway](https://technet.microsoft.com/library/mt626650.aspx).  
  
-   **GRE-Tunnel-gateways**  
  
    GRE-basierte Tunnel ermöglichen Verbindungen zwischen virtuellen Mandantennetzwerken und externen Netzwerken. Da das GRE-Protokoll Lightweight und Support ist für GRE auf die meisten Netzwerkgeräte verfügbar ist, wird es eine ideale Option zum Tunneln, in dem die datenverschlüsselung nicht erforderlich ist. Bei S2S (Standort-zu-Standort)-Tunneln kann durch GRE-Unterstützung das Problem der Weiterleitung zwischen virtuellen Mandantennetzwerken und externen Mandantennetzwerken über ein mehrinstanzenfähiges Gateway gelöst werden. Weitere Informationen zu den GRE-Tunnel, finden Sie unter [GRE Tunneling in Windows Server 2016](https://technet.microsoft.com/library/dn765485.aspx).  
  
**Routing Steuerungsebene mit BGP**  
  
Hyper-V-Netzwerkvirtualisierung (HNV)-Routing-Steuerelement ist die logische, zentrale Entität Steuerungsebene, die alle-Ebene die Kundenadresse Routen enthält Features, die dynamisch und aktualisiert dann die verteilte RAS-Gateway-Router im virtuellen Netzwerk. Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](https://technet.microsoft.com/library/mt631692.aspx) und [RAS-Gateway](https://technet.microsoft.com/library/mt626650.aspx).  
  
**Verteilte mehrinstanzenfähige firewall**  
  
Die Firewall schützt die Ebene des Netzwerks der virtuellen Netzwerke. Die Richtlinien werden auf den SDN-vSwitch-Port, der jeden virtuellen mandantencomputer erzwungen. Es schützt alle datenverkehrsflüsse: OST-West "und" Nord-Süd. Die Richtlinien werden über das mandantenportal abgelegt, und den Netzwerkcontroller für alle anwendbaren Hosts verteilt. Weitere Informationen zur verteilten Firewall mit mehreren Mandanten finden Sie unter [Datacenter Firewall – Übersicht](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).  
  


