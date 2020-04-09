---
title: Netzwerkfunktionsvirtualisierung
description: In diesem Thema erfahren Sie mehr über die netzwerkfunktionsvirtualisierung, mit der Sie virtuelle Netzwerkgeräte wie Datacenter Firewall, mehrinstanzfähiges RAS-Gateway und Software Lastenausgleich (Software Load Balancing, SLB) in Windows Server 2016 bereitstellen können.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 79df3bbe-48fd-4eff-8df6-35f6317566f3
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: aed1591756e7b491bd4c9ab325694dfb3e6fddb1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859623"
---
# <a name="network-function-virtualization"></a>Netzwerkfunktionsvirtualisierung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die netzwerkfunktionsvirtualisierung, mit der Sie virtuelle Netzwerkgeräte wie Datacenter Firewall, mehrinstanzfähiges RAS-Gateway und Software Lastenausgleich \(SLB\) Multiplexer \(MUX-\)bereitstellen können.
  
>[!NOTE]  
>Zusätzlich zu diesem Thema ist die folgende Dokumentation zur netzwerkfunktionsvirtualisierung verfügbar.  
> - [Übersicht über Datacenter Firewall](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)  
> - [RAS-Gateway für SDN](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)  
> - [Softwarelastenausgleich (SLB) für SDN](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)  
  
In den heutigen Software definierten Rechenzentren werden Netzwerkfunktionen, die von Hardware Geräten (z. b. Lasten Ausgleichs Module, Firewalls, Router, Switches usw.) ausgeführt werden, zunehmend als virtuelle Geräte virtualisiert. Diese „Netzwerkfunktionsvirtualisierung“ ist ein natürlicher Fortschritt der Server- und Netzwerkvirtualisierung. Virtuelle Geräte werden schnell neu entwickelt und erstellen einen neuen Markt. Sie generieren weiterhin Interessen und gewinnen Dynamik sowohl bei Virtualisierungsplattformen als auch bei Clouddiensten.  
  
Microsoft enthielt seit Windows Server 2012 R2 ein eigenständiges Gateway als virtuelles Gerät. Weitere Informationen finden Sie unter [Windows Server-Gateway](https://technet.microsoft.com/library/dn313101.aspx). Mit Windows Server 2016 erweitert und investiert Microsoft den Netzwerk Funktions-Virtualisierungsmarkt.  
  
## <a name="virtual-appliance-benefits"></a>Vorteile von virtuellen Geräten  
Ein virtuelles Gerät ist dynamisch und leicht zu ändern, da es sich um einen vordefinierten, angepassten virtuellen Computer handelt. Dabei kann es sich um einen oder mehrere virtuelle Computer handeln, die als Einheit verpackt, aktualisiert und verwaltet werden. In Verbindung mit Software-Defined Networking (SDN) erhalten Sie die Flexibilität und Flexibilität, die Sie in der heutigen cloudbasierten Infrastruktur benötigen. Beispiel:  
  
-   SDN stellt das Netzwerk als eine gepoolte und dynamische Ressource dar.  
  
-   SDN ermöglicht die Isolation von Mandanten.  
  
-   SDN maximiert die Skalierung und Leistung.  
  
-   Virtuelle Geräte ermöglichen eine nahtlose Kapazitätserweiterung und Arbeits Auslastungs Mobilität.  
  
-   Virtuelle Geräte minimieren die betriebliche Komplexität.  
  
-   Mit virtuellen Geräten können Kunden vorab integrierte Lösungen problemlos erwerben, bereitstellen und verwalten.  
  
    -   Kunden können das virtuelle Gerät problemlos an eine beliebige Stelle in der Cloud verschieben.  
  
    -   Kunden können virtuelle Geräte dynamisch nach Bedarf zentral hoch-oder Herunterskalieren.  
  
Weitere Informationen zu Microsoft Sdn finden Sie unter [Software-Defined Networking](https://technet.microsoft.com/windows-server-docs/networking/sdn/software-defined-networking--sdn-).  
  
### <a name="what-network-functions-are-being-virtualized"></a>Welche Netzwerkfunktionen werden virtualisiert?  
Der Marketplace für virtualisierte Netzwerkfunktionen wächst schnell. Die folgenden Netzwerkfunktionen werden virtualisiert:  
  
-   **Sicherheit**  
  
    -   Firewall  
  
    -   Antivirensoftware  
  
    -   DDoS (Verteilter Denial-of-Service)  
  
    -   IPS/IDs (Eindring Schutzsystem/Angriffs Erkennungssystem)  
  
-   **Anwendungs-/WAN-Optimierer**  
  
-   **Modernste**  
  
    -   Site-to-Site-Gateway  
  
    -   L3-Gateways  
  
    -   Router  
  
    -   Switches  
  
    -   NAT  
  
    -   Lasten Ausgleichs Module (nicht notwendigerweise an der Kante)  
  
    -   HTTP-Proxy  
  
## <a name="why-microsoft-is-a-great-platform-for-virtual-appliances"></a>Warum Microsoft eine gute Plattform für virtuelle Geräte ist  
![Virtueller Netzwerk Stapel](../../../media/Network-Function-Virtualization/Microsoft-Network-Function-Virtualization.png)  
  
Die Microsoft-Plattform ist so konzipiert, dass Sie eine gute Plattform zum Erstellen und Bereitstellen von virtuellen Geräten ist. Dies ist der Grund:  
  
-   Microsoft stellt wichtige virtualisierte Netzwerkfunktionen mit Windows Server 2016 bereit.  
  
-   Sie können ein virtuelles Gerät vom Hersteller Ihrer Wahl bereitstellen.  
  
-   Sie können Ihre virtuellen Geräte mit dem Microsoft-Netzwerk Controller bereitstellen, konfigurieren und verwalten, der in Windows Server 2016 verfügbar ist. Weitere Informationen zum Netzwerk Controller finden Sie unter [Netzwerk Controller](../../../sdn/technologies/network-controller/Network-Controller.md).  
  
-   Hyper-V kann die wichtigsten Gast Betriebssysteme hosten, die Sie benötigen.  
  
## <a name="network-function-virtualization-in-windows-server-2016"></a>Netzwerkfunktionsvirtualisierung in Windows Server 2016  
  
### <a name="virtual-appliances-functions-provided-by-microsoft"></a>Von Microsoft bereitgestellte Virtual Appliances-Funktionen  
Die folgenden virtuellen Geräte werden mit Windows Server 2016 bereitgestellt:  
  
**Software Load Balancer**  
  
Ein Layer-4-Lasten Ausgleichs Modul, das bei der Daten Center Skalierung ausgeführt wird. Dies ist eine ähnliche Version von Azure Load Balancer, die in der Azure-Umgebung skaliert bereitgestellt wurde. Weitere Informationen zum Microsoft-Software Load Balancer finden Sie unter [Software Lastenausgleich (Software Load Balancing, SLB) für Sdn](https://technet.microsoft.com/library/mt632286.aspx). Weitere Informationen zu Microsoft Azure Lasten Ausgleichs Diensten finden Sie unter [Microsoft Azure Load Balancing Services](https://azure.microsoft.com/blog/2014/04/08/microsoft-azure-load-balancing-services/).  
  
**Gateway**: RAS-Gateway stellt alle Kombinationen der folgenden Gatewayfunktionen bereit.  
  
-   **Site-to-Site-Gateway**  
  
    Das RAS-Gateway bietet ein Border Gateway Protocol (BGP)-fähiges, mehrinstanzfähiges Gateway, mit dem Ihre Mandanten über Standort-zu-Standort-VPN-Verbindungen von Remote Standorten aus auf Ihre Ressourcen zugreifen und diese verwalten können und den Netzwerk Datenverkehr zwischen virtuellen Ressourcen zulässt. in den physischen Cloud-und Mandanten Netzwerken. Weitere Informationen zum RAS-Gateway finden Sie unter [hohe Verfügbarkeit des RAS](https://technet.microsoft.com/library/mt631692.aspx) -Gateways und [RAS-Gateway](https://technet.microsoft.com/library/mt626650.aspx).  
  
-   **Weiterleitungs Gateway**  
  
    RAS-Gateway leitet Datenverkehr zwischen virtuellen Netzwerken und dem physischen Netzwerk des hostinganbieters weiter. Wenn Mandanten z. b. ein oder mehrere virtuelle Netzwerke erstellen und Zugriff auf freigegebene Ressourcen im physischen Netzwerk des hostinganbieters benötigen, kann das Weiterleitungs Gateway Datenverkehr zwischen dem virtuellen Netzwerk und dem physischen Netzwerk weiterleiten, um Benutzern die Arbeit zu ermöglichen. das virtuelle Netzwerk mit den Diensten, die Sie benötigen. Weitere Informationen finden Sie unter [hohe Verfügbarkeit des RAS-Gateways](https://technet.microsoft.com/library/mt631692.aspx) und [RAS-Gateway](https://technet.microsoft.com/library/mt626650.aspx).  
  
-   **GRE-Tunnel Gateways**  
  
    GRE-basierte Tunnel ermöglichen Verbindungen zwischen virtuellen Mandantennetzwerken und externen Netzwerken. Da das GRE-Protokoll einfach ist und die Unterstützung für GRE auf den meisten Netzwerkgeräten verfügbar ist, ist es eine ideale Wahl für das Tunnelingverfahren, bei dem keine Datenverschlüsselung erforderlich ist. Bei S2S (Standort-zu-Standort)-Tunneln kann durch GRE-Unterstützung das Problem der Weiterleitung zwischen virtuellen Mandantennetzwerken und externen Mandantennetzwerken über ein mehrinstanzenfähiges Gateway gelöst werden. Weitere Informationen zu GRE-Tunneln finden Sie unter [GRE tunnelingin Windows Server 2016](https://technet.microsoft.com/library/dn765485.aspx).  
  
**Routing Steuerungsebene mit BGP**  
  
Die Hyper-v-Netzwerkvirtualisierung (HNV) ist die logische, zentralisierte Entität auf der Steuerungsebene, die alle Routen der Kunden Adress Ebene enthält und die verteilten RAS-Gatewayrouter im virtuellen Netzwerk dynamisch erlernt und aktualisiert. Weitere Informationen finden Sie unter [hohe Verfügbarkeit des RAS-Gateways](https://technet.microsoft.com/library/mt631692.aspx) und [RAS-Gateway](https://technet.microsoft.com/library/mt626650.aspx).  
  
**Verteilte mehr Instanzen fähige Firewall**  
  
Die Firewall schützt die Netzwerkebene von virtuellen Netzwerken. Die Richtlinien werden auf dem SDN-Vswitch-Port der einzelnen Mandanten-VMS erzwungen. Sie schützt alle Daten Verkehrsflüsse: Ost-West und Nord-Süd. Die Richtlinien werden über das Mandanten Portal übermittelt, und der Netzwerk Controller verteilt Sie an alle anwendbaren Hosts. Weitere Informationen zur verteilten mehr Instanzen fähigen Firewall finden [Sie unter Übersicht über die Datacenter-Firewall](../../../sdn/technologies/network-function-virtualization/../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).  
  


