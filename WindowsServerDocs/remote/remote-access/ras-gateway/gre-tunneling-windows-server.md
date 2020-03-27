---
title: GRE-Tunneling in Windows Server 2016
description: Sie können dieses Thema verwenden, um ein Verständnis der Aktualisierungen der GRE-Tunnel Funktion (Generic Routing Kapselung) für das RAS-Gateway in Windows Server 2016 zu erhalten.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: df2023bf-ba64-481e-b222-6f709edaa5c1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d246f0e56681f75e4336ed225d1557a0e05c581b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308555"
---
# <a name="gre-tunneling-in-windows-server-2016"></a>GRE-Tunneling in Windows Server 2016

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Windows Server 2016 bietet Aktualisierungen der allgemeinen Routing Kapselung \(GRE-\) Tunnel Funktion für das RAS-Gateway.  
  
GRE ist ein einfaches Tunneling-Protokoll, das eine Vielzahl von Protokollen der Vermittlungsschicht in virtuellen Point-to-Point-Links über ein IP-Internetwork kapseln kann. Die Microsoft GRE-Implementierung kann IPv4 und IPv6 Kapseln.  
  
GRE-Tunnel sind in vielen Szenarien nützlich:  
  
-   Sie sind einfach und RFC 2890 kompatibel, sodass Sie mit verschiedenen Hersteller Geräten interoperabel sind.  
  
-   Sie können Border Gateway Protocol \(BGP-\) für dynamisches Routing verwenden.  
  
-   Sie können mehr Instanzen fähige GRE-RAS-Gateways für die Verwendung mit Software-Defined Networking \(Sdn konfigurieren\)
  
-   Sie können System Center Virtual Machine Manager zum Verwalten von GRE\-basierten RAS-Gateways verwenden.
  
-   Sie können einen Durchsatz von bis zu 2,0 Gbit/s auf einem virtuellen Computer mit 6 Kernen erzielen, der als GRE-RAS-Gateway konfiguriert ist.
  
-   Ein einzelnes Gateway unterstützt mehrere Verbindungs Modi.  
  
GRE-basierte Tunnel ermöglichen Verbindungen zwischen virtuellen Mandantennetzwerken und externen Netzwerken. Da das GRE-Protokoll einfach ist und die Unterstützung für GRE auf den meisten Netzwerkgeräten verfügbar ist, ist es eine ideale Wahl für das Tunnelingverfahren, bei dem keine Datenverschlüsselung erforderlich ist. 

Die GRE-Unterstützung in Standort-zu-Standort-Tunneln (S2S) löst das Problem der Weiterleitung zwischen virtuellen Mandanten Netzwerken und externen Mandanten Netzwerken mithilfe eines mehr Instanzen fähigen Gateways, wie weiter unten in diesem Thema beschrieben.  
  
Die GRE-Tunnel Funktion ist so konzipiert, dass Sie die folgenden Anforderungen erfüllt:  
  
-   Ein Hostinganbieter muss virtuelle Netzwerke für die Weiterleitung erstellen können, ohne die Konfiguration des physischen Switches zu ändern.  
  
-   Ein Hostinganbieter muss ihren extern ausgerichteten Netzwerken Subnetze hinzufügen können, ohne die Konfiguration der physischen Switches innerhalb der Infrastruktur zu ändern.  
Die GRE-Tunnel Funktion ermöglicht oder erweitert verschiedene wichtige Szenarien für das Hosten von Dienstanbietern mithilfe von Microsoft-Technologien zur Implementierung von Software-Defined Networking in ihren Dienst angeboten.  
  
Im folgenden finden Sie einige Beispielszenarien:  
  
-   [Zugriff von virtuellen Mandanten Netzwerken auf physische Mandanten Netzwerke](#BKMK_Access)  
  
-   [Hoch Geschwindigkeits Konnektivität](#BKMK_Speed)  
  
-   [Integration in VLAN-basierte Isolation](#BKMK_Integration)  
  
-   [Zugreifen auf freigegebene Ressourcen](#BKMK_Shared)  
  
-   [Dienste von Drittanbieter Geräten für Mandanten](#BKMK_thirdparty)  
  
## <a name="key-scenarios"></a>Wichtige Szenarien

Im folgenden finden Sie die wichtigsten Szenarien, die der GRE-Tunnel-Feature adressiert.  
  
### <a name="access-from-tenant-virtual-networks-to-tenant-physical-networks"></a><a name="BKMK_Access"></a>Zugriff von virtuellen Mandanten Netzwerken auf physische Mandanten Netzwerke

Dieses Szenario ermöglicht eine skalierbare Möglichkeit, den Zugriff von virtuellen Mandanten Netzwerken auf physische Mandanten Netzwerke auf dem lokalen hostingdienstanbieter bereitzustellen. Ein GRE-Tunnelendpunkt wird auf dem mehr Instanzen fähigen Gateway eingerichtet, der andere GRE-Tunnelendpunkt wird auf einem Drittanbieter Gerät im physischen Netzwerk eingerichtet. Layer-3-Datenverkehr wird zwischen den virtuellen Computern im virtuellen Netzwerk und dem Drittanbieter Gerät im physischen Netzwerk weitergeleitet.  
  
![GRE-Tunnel mit Verbindung zum physischen Host Netzwerk und zum virtuellen Mandanten Netzwerk](../../media/gre-tunneling-in-windows-server/GRE_.png)  
  
### <a name="high-speed-connectivity"></a><a name="BKMK_Speed"></a>Hoch Geschwindigkeits Konnektivität

Dieses Szenario ermöglicht eine skalierbare Möglichkeit, eine hoch Geschwindigkeits Konnektivität zwischen dem lokalen Netzwerk des Mandanten und dem virtuellen Netzwerk im hostingdienstanbieter-Netzwerk bereitzustellen. Ein Mandant stellt über MPLS (Multiprotocol Label Switching) eine Verbindung mit dem Dienstanbieter Netzwerk her, bei der zwischen dem edgerrouter des hostingdienstanbieters und dem mehr Instanzen fähigen Gateway und dem virtuellen Netzwerk des Mandanten ein GRE-Tunnel eingerichtet wird.  
  
![GRE-Tunnel mit Verbindung zwischen Mandanten-MPLS-Netzwerk und virtuellem Mandanten Netzwerk](../../media/gre-tunneling-in-windows-server/GRE-.png)  
  
### <a name="integration-with-vlan-based-isolation"></a><a name="BKMK_Integration"></a>Integration in VLAN-basierte Isolation

In diesem Szenario können Sie die VLAN-basierte Isolation mit der Hyper-V-Netzwerkvirtualisierung integrieren. Ein physisches Netzwerk im hostinganbietenetzwerk enthält ein Lasten Ausgleichs Modul, das die VLAN-basierte Isolation verwendet. Ein mehr Instanzen fähiges Gateway stellt GRE-Tunnel zwischen dem Load Balancer im physischen Netzwerk und dem mehr Instanzen fähigen Gateway im virtuellen Netzwerk her.  
  
Zwischen Quelle und Ziel können mehrere Tunnel eingerichtet werden, und der GRE-Schlüssel wird verwendet, um zwischen den Tunneln zu unterscheiden.  
  
![Mehrere GRE-Tunnel, die virtuelle Mandanten Netzwerke verbinden](../../media/gre-tunneling-in-windows-server/GRE-VLANIsolation.png)  
  
### <a name="access-shared-resources"></a><a name="BKMK_Shared"></a>Zugreifen auf freigegebene Ressourcen

In diesem Szenario können Sie auf freigegebene Ressourcen in einem physischen Netzwerk zugreifen, das sich im hostinganbietenetzwerk befindet.  
  
Sie verfügen möglicherweise über einen gemeinsamen Dienst, der sich auf einem Server in einem physischen Netzwerk im hostinganbieternetzwerk befindet, das Sie für mehrere virtuelle Mandanten Netzwerke freigeben möchten.  
  
Die Mandanten Netzwerke mit nicht überlappenden Subnetzen greifen über einen GRE-Tunnel auf das gemeinsame Netzwerk zu. Eine einzige Mandanten-Gatewayroute zwischen den GRE-Tunneln, sodass Pakete an die entsprechenden Mandanten Netzwerke weitergeleitet werden.  
  
In diesem Szenario kann das Gateway eines einzelnen Mandanten durch Hardware Geräte von Drittanbietern ersetzt werden.  
  
![Ein Gateway mit einem Mandanten, das mehrere Tunnel zum Verbinden mehrerer virtueller Netzwerke verwendet](../../media/gre-tunneling-in-windows-server/GRE-SharedResource.png)  
  
### <a name="services-of-third-party-devices-to-tenants"></a><a name="BKMK_thirdparty"></a>Dienste von Drittanbieter Geräten für Mandanten

Dieses Szenario kann verwendet werden, um Drittanbieter Geräte (z. b. Hardware-Lasten Ausgleichs Module) in den Daten Verkehrsfluss des virtuellen Mandanten Netzwerks zu integrieren. Beispielsweise wird der Datenverkehr von einem Unternehmens Standort über einen S2S-Tunnel an das mehr Instanzen fähige Gateway weitergeleitet. Der Datenverkehr wird über einen GRE-Tunnel an den Load Balancer weitergeleitet. Der Load Balancer leitet Datenverkehr an mehrere virtuelle Computer im virtuellen Netzwerk des Unternehmens weiter. Dasselbe geschieht für einen anderen Mandanten mit potenziell überlappenden IP-Adressen in den virtuellen Netzwerken. Der Netzwerk Datenverkehr wird mithilfe von VLANs auf dem Load Balancer isoliert und gilt für alle Layer 3-Geräte, von denen VLANs unterstützt werden.  
  
![Mehrere GRE-Tunnel, die virtuelle Netzwerke mit Geräten von Drittanbietern verbinden](../../media/gre-tunneling-in-windows-server/GREThirdParty.png)  
  
## <a name="configuration-and-deployment"></a>Konfiguration und Bereitstellung

Ein GRE-Tunnel wird als zusätzliches Protokoll innerhalb einer S2S-Schnittstelle verfügbar gemacht. Die Implementierung erfolgt auf ähnliche Weise wie ein IPSec-S2S-Tunnel, der im folgenden Netzwerk Blog beschrieben wird: mehr Instanzen fähige [Site-to-Site (S2S)-VPN Gateway mit Windows Server 2012 R2](https://blogs.technet.com/b/networking/archive/2013/09/29/multi-tenant-site-to-site-s2s-vpn-gateway-with-windows-server-2012-r2.aspx)  
  
Im folgenden Thema finden Sie ein Beispiel für die Bereitstellung von Gateways, einschließlich GRE-Tunnel Gateways:  
  
[Bereitstellen einer Software definierten Netzwerkinfrastruktur mithilfe von Skripts](../../../networking/sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
  
## <a name="more-information"></a>Weitere Informationen

Weitere Informationen zum Bereitstellen von S2S-Gateways finden Sie in den folgenden Themen:  
  
-   [RAS-Gateway](RAS-Gateway.md)  
  
-   [Border Gateway Protocol &#40;BGP&#41;](../bgp/Border-Gateway-Protocol-BGP.md)  
  
-   [Neu! Bereitstellungs Handbuch für das mehr Instanzen fähige Windows Server 2012 R2 RAS-Gateway](https://blogs.technet.com/b/wsnetdoc/archive/2014/03/26/new-windows-server-2012-r2-RAS-multitenant-gateway-deployment-guide.aspx)  
  
-   [Bereitstellen von Border Gateway Protocol (BGP) mit dem mehr Instanzen fähigen RAS-Gateway](https://blogs.technet.com/b/wsnetdoc/archive/2014/04/03/deploy-border-gateway-protocol-bgp-with-the-RAS-multitenant-gateway.aspx)  
  


