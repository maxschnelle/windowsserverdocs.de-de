---
title: GRE-Tunneling in Windows Server 2016
description: Sie können in diesem Thema verwenden, um einen Überblick über die Updates für Generic Routing Encapsulation (GRE)-Tunnel-Funktion für RAS-Gateway unter Windows Server 2016 zu erhalten.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: df2023bf-ba64-481e-b222-6f709edaa5c1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e0ec077ad5e97edd3db7d1dc4e662bb191f7885b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887861"
---
# <a name="gre-tunneling-in-windows-server-2016"></a>GRE-Tunneling in Windows Server 2016

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Windows Server 2016 bietet Updates für Generic Routing Encapsulation \(GRE\) Tunneln Funktion für das RAS-Gateway.  
  
GRE ist ein einfaches Tunneling-Protokoll, das eine Vielzahl von Protokollen der Vermittlungsschicht in virtuellen Point-to-Point-Links über ein IP-Internetwork kapseln kann. Die Microsoft-GRE-Implementierung kann IPv4 und IPv6 kapseln.  
  
GRE-Tunnel sind in vielen Szenarien nützlich, da:  
  
-   Sie sind einfach und RFC 2890 kompatibel, somit Interoperabilität mit unterschiedlichen Geräten und Hersteller  
  
-   Sie können die Border Gateway Protocol \(BGP\) für dynamisches routing  
  
-   Sie können die GRE-Multitenant-RAS-Gateways für die Verwendung konfigurieren, mit der Software Defined Networking \(SDN\)
  
-   Sie können System Center Virtual Machine Manager zum Verwalten von GRE\-basierte RAS-Gateways
  
-   Sie können bis zu 2,0 Gbit/s Durchsatz auf einem virtuellen Computer von 6 Kerne erreichen, die als GRE-RAS-Gateway konfiguriert ist
  
-   Ein einzelnes Gateway unterstützt mehrere Verbindungsmodi  
  
GRE-basierte Tunnel ermöglichen Verbindungen zwischen virtuellen Mandantennetzwerken und externen Netzwerken. Da das GRE-Protokoll ist einfach und Unterstützung, für GRE auf die meisten Netzwerkgeräte verfügbar ist, wird es eine ideale Option zum Tunneln, in denen die Verschlüsselung von Daten nicht erforderlich ist. 

GRE-Unterstützung (S2S)-Standort-zu-Standort-Tunnel löst das Problem der Weiterleitung zwischen virtuellen mandantennetzwerken und externen mandantennetzwerken über ein Gateway mit mehreren Mandanten an, wie weiter unten in diesem Thema beschrieben.  
  
Das GRE-Tunnel-Feature wurde entwickelt, um folgende Anforderungen erfüllt sein:  
  
-   Ein hosting-Anbieter muss virtuelle Netzwerke für die Weiterleitung zu erstellen, ohne Ändern der Konfiguration der physischen Switch können.  
  
-   Ein hosting-Anbieter muss an ihre externe Netzwerke Subnetze hinzufügen, ohne Ändern der Konfiguration der physischen Switches in ihrer Infrastruktur können.  
Das GRE-Tunnel-Feature aktiviert oder mehrere wichtige Szenarien für das hosting-Anbietern, die mit Microsoft-Technologien zum Implementieren von Software Defined Networking in ihrer Dienstangebote verbessert.  
  
Es folgen einige Beispielszenarien:  
  
-   [Zugriff von Mandanten virtuelle Netzwerke zu physischen Netzwerke von Mandanten](#BKMK_Access)  
  
-   [Hochgeschwindigkeitskonnektivität](#BKMK_Speed)  
  
-   [Integration mit VLAN-basierte isolation](#BKMK_Integration)  
  
-   [Zugreifen auf freigegebene Ressourcen](#BKMK_Shared)  
  
-   [Dienste von Geräten von Drittanbietern für Mandanten](#BKMK_thirdparty)  
  
## <a name="key-scenarios"></a>Wichtige Szenarios

Im folgenden werden wichtige Szenarien, in denen die GRE-tunnel Feature Adressen.  
  
### <a name="BKMK_Access"></a>Zugriff von Mandanten virtuelle Netzwerke zu physischen Netzwerke von Mandanten

In diesem Szenario können eine skalierbare Möglichkeit, die Zugriff von virtuellen mandantennetzwerken zum physischen Netzwerke befindet sich im lokalen Host Service-Anbieter Mandanten bereitzustellen. Ein GRE-Tunnel-Endpunkt auf dem mehrinstanzenfähigen Gateway hergestellt ist, wird der anderen GRE-Tunnel-Endpunkt auf einem Gerät von Drittanbietern auf dem physischen Netzwerk hergestellt. Layer-3-Datenverkehr wird zwischen den virtuellen Computern im virtuellen Netzwerk und das Drittanbieter-Gerät auf dem physischen Netzwerk weitergeleitet.  
  
![Verbinden von physischen Netzwerk Hoster und virtuelle Netzwerk des Mandanten GRE-tunnel](../../media/gre-tunneling-in-windows-server/GRE_.png)  
  
### <a name="BKMK_Speed"></a>Hochgeschwindigkeitskonnektivität

In diesem Szenario können skalierbare Hochgeschwindigkeitskonnektivität aus dem lokalen Netzwerk des Mandanten mit dem virtuellen Netzwerk befindet sich im Netzwerk hostanbieters Dienst bereitstellen. Ein Mandant eine Verbindung mit dem Service Provider-Netzwerk über Multiprotokoll Label switching (MPLS), in ein GRE-Tunnel zwischen der hosting-Anbieter des Edge-Router und dem mehrinstanzenfähigen Gateway mit dem virtuellen mandantennetzwerk eingerichtet wird.  
  
![GRE-Tunnel Herstellen einer Verbindung MPLS-Unternehmensnetzwerk Mandanten und das virtuelle Netzwerk des Mandanten](../../media/gre-tunneling-in-windows-server/GRE-.png)  
  
### <a name="BKMK_Integration"></a>Integration mit VLAN-basierte isolation

Dieses Szenario ermöglicht es Ihnen die Integration von VLAN-basierte Isolation mit Hyper-V-Netzwerkvirtualisierung. Ein physisches Netzwerk auf das Netzwerk des hostanbieters enthält ein Load Balancers mit der VLAN-basierte Isolation. Ein mehrinstanzenfähigen Gateways wird die GRE-Tunnel zwischen dem Load Balancer im physischen Netzwerk und dem mehrinstanzenfähigen Gateway im virtuellen Netzwerk hergestellt.  
  
Mehrere Tunnel zwischen der Quell- und Zielserver hergestellt werden können, und der GRE-Schlüssel wird zur Unterscheidung zwischen den Tunneln verwendet.  
  
![Mehrere GRE-Tunnel verbinden virtueller Netzwerke von Mandanten](../../media/gre-tunneling-in-windows-server/GRE-VLANIsolation.png)  
  
### <a name="BKMK_Shared"></a>Zugreifen auf freigegebene Ressourcen

Dieses Szenario können Sie den Zugriff auf freigegebene Ressourcen in einem physischen Netzwerk, die sich auf das Netzwerk des hostanbieters befindet.  
  
Sie müssen möglicherweise einen freigegebenen Dienst befindet sich auf einem Server auf einem physischen Netzwerk befindet sich im Netzwerk hostanbieters, das Sie mit mehreren Mandanten und virtuellen Netzwerken freigeben möchten.  
  
Die mandantennetzwerke mit nicht überlappenden Subnetzen auf das allgemeine Netzwerk über einen GRE-Tunnel zugreifen. Ein Gateway für die einzelnen Mandanten Routen zwischen den GRE-Tunnel, daher routing von Paketen mit den entsprechenden mandantennetzwerken.  
  
In diesem Szenario kann das Gateway für die einzelnen Mandanten von Drittanbieter-Hardware ersetzt werden.  
  
![Ein einzelner Mandant Gateway mehrere Tunnel verwenden, um mehrere virtuelle Netzwerke verbinden](../../media/gre-tunneling-in-windows-server/GRE-SharedResource.png)  
  
### <a name="BKMK_thirdparty"></a>Dienste von Geräten von Drittanbietern für Mandanten

Dieses Szenario kann zum Integrieren von Geräten von Drittanbietern (z. B. hardwaremodule zum Lastenausgleich) verwendet werden, in der Mandant virtuelle Netzwerke den Datenfluss. Z. B. leitet Datenverkehr aus einem Enterprise-Website über eine S2S-Tunnel mit dem mehrinstanzenfähigen Gateway. Der Datenverkehr wird an den Load Balancer über einen GRE-Tunnel weitergeleitet. Der Load Balancer leitet Datenverkehr auf mehrere virtuelle Computer im virtuellen Netzwerk des Unternehmens. Dasselbe geschieht für einen anderen Mandanten mit sich überschneidenden potenziell die IP-Adressen in den virtuellen Netzwerken. Der Netzwerkdatenverkehr des Load Balancers mithilfe von VLANs isoliert ist, und gilt für alle Layer 3-Geräte, die VLANs zu unterstützen.  
  
![Mehrere GRE-Tunnel verbinden virtueller Netzwerke für Drittanbieter-Geräte](../../media/gre-tunneling-in-windows-server/GREThirdParty.png)  
  
## <a name="configuration-and-deployment"></a>Konfiguration und Bereitstellung

GRE-Tunnel wird als zusätzliche Protokolle innerhalb einer S2S-Schnittstelle verfügbar gemacht. Es wird auf ähnliche Weise wie einen IPSec-S2S-Tunnel, die im folgenden Blog Netzwerk beschrieben implementiert: [Mehrinstanzenfähige Standort-zu-Standort (S2S) VPN-Gateway mit Windows Server 2012 R2](https://blogs.technet.com/b/networking/archive/2013/09/29/multi-tenant-site-to-site-s2s-vpn-gateway-with-windows-server-2012-r2.aspx)  
  
Finden Sie ein Beispiel für die Gateways, einschließlich GRE-Tunnel Gateways bereitstellt:  
  
[Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](../../../networking/sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
  
## <a name="more-information"></a>Weitere Informationen

Weitere Informationen zum Bereitstellen von S2S-Gateways finden Sie unter den folgenden Themen:  
  
-   [RAS Gateway](RAS-Gateway.md)  
  
-   [Border Gateway Protocol &#40;BGP&#41;](../bgp/Border-Gateway-Protocol-BGP.md)  
  
-   [Neu! Windows Server 2012 R2-RAS-Multitenant Gateway Deployment Guide](https://blogs.technet.com/b/wsnetdoc/archive/2014/03/26/new-windows-server-2012-r2-RAS-multitenant-gateway-deployment-guide.aspx)  
  
-   [Bereitstellen von Border Gateway Protocol (BGP) mit dem mehrinstanzenfähigen RAS-Gateway](https://blogs.technet.com/b/wsnetdoc/archive/2014/04/03/deploy-border-gateway-protocol-bgp-with-the-RAS-multitenant-gateway.aspx)  
  


