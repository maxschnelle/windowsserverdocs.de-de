---
title: 'RAS-Gateway: Bereitstellungsarchitektur'
description: In diesem Thema erfahren Sie mehr über die Bereitstellung von clouddienstanbietern (Cloud Service Provider, CSP) des RAS-Gateways in Windows Server 2016, einschließlich RAS-gatewaypools, Routen-Reflektoren und Bereitstellen mehrerer Gateways für einzelne Mandanten.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d46e4e91-ece0-41da-a812-af8ab153edc4
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 91d8081261d3cbc5e2da61cc2b5a9737e76a0dc7
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309805"
---
# <a name="ras-gateway-deployment-architecture"></a>RAS-Gateway: Bereitstellungsarchitektur

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die Bereitstellung von Cloud Service Provider (CSP) des RAS-Gateways, einschließlich der RAS-gatewaypools, Routen Reflektoren und der Bereitstellung mehrerer Gateways für einzelne Mandanten.  
  
In den folgenden Abschnitten finden Sie einen kurzen Überblick über einige der neuen Features des RAS-Gateways, damit Sie verstehen können, wie Sie diese Funktionen beim Entwerfen der Gatewaybereitstellung verwenden.  
  
Außerdem wird ein Beispiel für die Bereitstellung bereitgestellt, einschließlich Informationen zum Hinzufügen neuer Mandanten, Routen Synchronisierung und Daten Ebenen-Routing, Gateway-und Weiterleitungs reflektorfailover und mehr.  
  
Dieses Thema enthält folgende Abschnitte:  
  
-   [Verwenden der neuen Features des RAS-Gateways zum Entwerfen der Bereitstellung](#bkmk_new)  
  
-   [Beispiel Bereitstellung](#bkmk_example)  
  
-   [Hinzufügen neuer Mandanten und eines EBGP-Peerings für Kundenadressen (ca)](#bkmk_tenant)  
  
-   [Routen-und Daten Ebenen-Routing](#bkmk_route)  
  
-   [Reaktion des Netzwerk Controllers auf RAS-Gateway und Weiterleitungs reflektorfailover](#bkmk_failover)  
  
-   [Vorteile der Verwendung neuer Features des RAS-Gateways](#bkmk_advantages)  
  
## <a name="using-ras-gateway-new-features-to-design-your--deployment"></a><a name="bkmk_new"></a>Verwenden der neuen Features des RAS-Gateways zum Entwerfen der Bereitstellung  
RAS-Gateway umfasst mehrere neue Features, die sich ändern und die Art und Weise verbessern, wie Sie Ihre gatewayinfrastruktur in Ihrem Daten Center bereitstellen.  
  
### <a name="bgp-route-reflector"></a>BGP-Routen Reflektor  
Die BGP-Routen Reflektorfunktion (Border Gateway Protocol) ist jetzt im RAS-Gateway enthalten und bietet eine Alternative zur vollständigen BGP-Mesh-Topologie, die normalerweise für die Routen Synchronisierung zwischen Routern erforderlich ist. Bei der vollständigen Netzwerksynchronisierung müssen alle BGP-Router eine Verbindung mit allen anderen Routern in der Routing Topologie herstellen. Wenn Sie jedoch den Routen Reflektor verwenden, ist der Routen Reflektor der einzige Router, der mit allen anderen Routern verbunden ist, die als BGP-Routen reflektorclients bezeichnet werden, wodurch die Routen Synchronisierung vereinfacht und der Netzwerkverkehr reduziert wird. Der Routen Reflektor lernt alle Routen, berechnet die besten Routen und verteilt die besten Routen an seine BGP-Clients.  
  
Weitere Informationen finden Sie unter Neuigkeiten [beim RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md).  
  
### <a name="gateway-pools"></a><a name="bkmk_pools"></a>Gatewaypools  
In Windows Server 2016 können Sie viele gatewaypools mit unterschiedlichen Typen erstellen. Gatewaypools enthalten viele Instanzen des RAS-Gateways und leiten Netzwerk Datenverkehr zwischen physischen und virtuellen Netzwerken weiter.  
  
Weitere Informationen finden Sie unter [Neues beim RAS-Gateway und in der RAS-Gateway-](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) [Hochverfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
### <a name="gateway-pool-scalability"></a><a name="bkmk_gps"></a>Skalierbarkeit des gatewaypools  
Sie können einen gatewaypool problemlos zentral hoch-oder herunterskalieren, indem Sie Gateway-VMS im Pool hinzufügen oder entfernen. Das Entfernen oder Hinzufügen von Gateways beeinträchtigt nicht die Dienste, die von einem Pool bereitgestellt werden. Sie können auch die gesamten Pools von Gateways hinzufügen und entfernen.  
  
Weitere Informationen finden Sie unter [Neues beim RAS-Gateway und in der RAS-Gateway-](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) [Hochverfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
### <a name="mn-gateway-pool-redundancy"></a><a name="bkmk_m"></a>Mehr als die gatewaypoolpoolredundanz  
Jeder gatewaypool ist M + N redundant. Dies bedeutet, dass die Anzahl der aktiven Gateway-VMS durch eine N-Anzahl von standbygatewayvms gesichert wird. Die Redundanz von M + N bietet Ihnen mehr Flexibilität bei der Ermittlung des Zuverlässigkeits Niveaus, das Sie bei der Bereitstellung des RAS-Gateways benötigen.  
  
Weitere Informationen finden Sie unter [Neues beim RAS-Gateway und in der RAS-Gateway-](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) [Hochverfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
## <a name="example-deployment"></a><a name="bkmk_example"></a>Beispiel Bereitstellung  
Die folgende Abbildung zeigt ein Beispiel für das eBGP-Peering über Standort-zu-Standort-VPN-Verbindungen, die zwischen zwei Mandanten konfiguriert sind: "", "", "", "", "", "" und "fabrikam  
  
![eBGP-Peering über Site-to-Site-VPN](../../../media/RAS-Gateway-Deployment-Architecture/ras_gateway_architecture.png)  
  
In diesem Beispiel ist für "Configuration Manager" eine zusätzliche gatewaybandbreite erforderlich, was dazu führt, dass die gatewayinfrastructure-Entwurfs Entscheidung zum Beenden der Site "Site Los Angeles" auf GW3 anstelle von GW2 führt. Aus diesem Grund wird die Verbindung zwischen den Configuration Manager-VPN-Verbindungen von unterschiedlichen Standorten im CSP-Daten Center auf zwei verschiedenen Gateways beendet.  
  
Beide Gateways, GW2 und GW3, waren die ersten RAS-Gateways, die vom Netzwerk Controller konfiguriert wurden, als der CSP die Mandanten "Configuration" und "Woodgrove" der Infrastruktur hinzugefügt hat. Aus diesem Grund werden diese beiden Gateways als Routen Reflektoren für diese entsprechenden Kunden (oder Mandanten) konfiguriert. GW2 ist der Routen Reflektor von "", und "GW3" ist der Woodgrove-Routen Reflektor. er ist nicht nur der CSP-RAS-gatewaybeendigungs Punkt für die VPN-Verbindung mit der Site "Site-to-Site Los Angeles  
  
> [!NOTE]  
> Ein RAS-Gateway kann virtuellen und physischen Netzwerk Datenverkehr für bis zu 100 verschiedene Mandanten weiterleiten. Dies hängt von den Bandbreitenanforderungen der einzelnen Mandanten ab.  
  
Als Routen-Reflektoren sendet GW2 die Speicherplatz Routen von "ca" an den Netzwerk Controller, und GW3 sendet Woodgrove ca-Speicherplatz Routen an den Netzwerk Controller.  
  
Der Netzwerk Controller überträgt Hyper-V-netzwerkvirtualisierungsrichtlinien an die virtuellen Netzwerke "Configuration Manager" und "Woodgrove" sowie RAS-Richtlinien zu den RAS-Gateways und Lasten Ausgleichs Richtlinien an die Multiplexers (muxes), die als Software Lastenausgleich konfiguriert sind. Spool.  
  
## <a name="adding-new-tenants-and-customer-address-ca-space-ebgp-peering"></a><a name="bkmk_tenant"></a>Hinzufügen neuer Mandanten und eines EBGP-Peerings für Kundenadressen (ca)  
Wenn Sie einen neuen Kunden Signieren und den Kunden als neuen Mandanten in Ihrem Rechenzentrum hinzufügen, können Sie den folgenden Prozess verwenden, der von den meisten automatisch von Netzwerk Controllern und RAS-Gateway-EBGP-Routern ausgeführt wird.  
  
1.  Stellen Sie ein neues virtuelles Netzwerk und Arbeits Auslastungen gemäß den Anforderungen Ihres Mandanten bereit.  
  
2.  Konfigurieren Sie bei Bedarf die Remote Konnektivität zwischen dem Remote-Mandanten Unternehmens Standort und dem zugehörigen virtuellen Netzwerk in Ihrem Rechenzentrum. Wenn Sie eine Standort-zu-Standort-VPN-Verbindung für den Mandanten bereitstellen, wählt der Netzwerk Controller automatisch eine verfügbare RAS-Gateway-VM aus dem verfügbaren gatewaypool aus und konfiguriert die Verbindung.  
  
3.  Beim Konfigurieren der RAS-Gateway-VM für den neuen Mandanten konfiguriert der Netzwerk Controller auch das RAS-Gateway als BGP-Router und legt es als Routen Reflektor für den Mandanten fest. Dies gilt auch für Situationen, in denen das RAS-Gateway als Gateway oder als Gateway-und Routen Reflektor für andere Mandanten fungiert.  
  
4.  Abhängig davon, ob das Routing des Zertifizierungsstellen-Speicherplatzes für die Verwendung statisch konfigurierter Netzwerke oder dynamisches BGP-Routing konfiguriert ist, konfiguriert der Netzwerk Controller die entsprechenden statischen Routen, BGP-Nachbarn oder beides auf der RAS-Gateway-VM und dem Routen Reflektor.  
  
    > [!NOTE]  
    > -   Nachdem der Netzwerk Controller ein RAS-Gateway und einen Weiterleitungs Reflektor für den Mandanten konfiguriert hat, überprüft der Netzwerk Controller immer dann, wenn der gleiche Mandant eine neue Standort-zu-Standort-VPN-Verbindung erfordert, die verfügbare Kapazität auf diesem virtuellen RAS-Gatewaycomputer Wenn das ursprüngliche Gateway die erforderliche Kapazität bedienen kann, wird die neue Netzwerkverbindung auch auf demselben virtuellen RAS-Gateway-Computer konfiguriert. Wenn die VM des RAS-Gateways keine zusätzliche Kapazität verarbeiten kann, wählt der Netzwerk Controller eine neue verfügbare RAS-Gateway-VM aus und konfiguriert die neue Verbindung darauf. Diese neue RAS-Gateway-VM, die dem Mandanten zugeordnet ist, wird zum Routen Reflektor-Client des ursprünglichen RAS-gatewayserverweiterleitungs-  
    > -   Da sich RAS-gatewaypools hinter Software Lastenausgleich (SLB) befinden, verwenden die Site-to-Site-VPN-Adressen der Mandanten jeweils eine einzelne öffentliche IP-Adresse, die als virtuelle IP-Adresse (VIP) bezeichnet wird. diese wird von den SLAs in eine interne IP-Adresse des Rechenzentrums übersetzt. dynamische IP-Adresse (DIP) für ein RAS-Gateway, das den Datenverkehr für den Unternehmens Mandanten weiterleitet. Diese Zuordnung von "Public zu private IP Address" durch SLB stellt sicher, dass die Standort-zu-Standort-VPN-Tunnel zwischen den Unternehmensstandorten und den CSP-RAS-Gateways und Routen Reflektoren ordnungsgemäß eingerichtet werden.  
    >   
    >     Weitere Informationen zu SLB, VIPs und Dips finden Sie unter [Software Lastenausgleich &#40;SLB&#41; für Sdn](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).  
  
5.  Nachdem der Standort-zu-Standort-VPN-Tunnel zwischen dem Unternehmens Standort und dem Rechenzentrums-RAS-Gateway für den neuen Mandanten eingerichtet wurde, werden die statischen Routen, die den Tunneln zugeordnet sind, automatisch sowohl auf der Unternehmensseite als auch auf der CSP-Seite des Tunnels bereitgestellt. .  
  
6.  Mit dem BGP-Routing des Zertifizierungsstellen-Speicherplatzes wird auch das eBGP-Peering zwischen den Unternehmensstandorten und dem Routen Reflektor des CSP-RAS-Gateways eingerichtet  
  
## <a name="route-synchronization-and-data-plane-routing"></a><a name="bkmk_route"></a>Routen-und Daten Ebenen-Routing  
Nachdem das eBGP-Peering zwischen Unternehmensstandorten und dem CSP-gatewaygatewayweiterleitungs-Reflektor eingerichtet wurde, lernt der Routen Reflektor alle Unternehmens Routen mithilfe des dynamischen BGP-Routings. Der Routen Reflektor synchronisiert diese Routen zwischen allen Routen reflektorclients, sodass Sie alle mit demselben Satz von Routen konfiguriert sind.  
  
Der Routen Reflektor aktualisiert außerdem diese konsolidierten Routen mithilfe der Routen Synchronisierung an den Netzwerk Controller. Der Netzwerk Controller übersetzt die Routen dann in die Hyper-V-netzwerkvirtualisierungsrichtlinien und konfiguriert das Fabric-Netzwerk, um sicherzustellen, dass das End-to-End-Datenpfad Routing bereitgestellt wird. Durch diesen Vorgang wird das virtuelle Mandanten Netzwerk von den Mandanten Unternehmenswebsites zugänglich gemacht.  
  
Für das Routing auf Datenebene werden die Pakete, die die RAS-Gateway-VMS erreichen, direkt an das virtuelle Netzwerk des Mandanten weitergeleitet, da die erforderlichen Routen nun für alle teilnehmenden RAS-Gateway-VMS verfügbar sind.  
  
Ebenso leitet das virtuelle Mandanten Netzwerk mit den Richtlinien für die Hyper-V-Netzwerkvirtualisierung Pakete direkt an die virtuellen RAS-Gateway-Computer weiter (ohne den Routen Reflektor kennen zu müssen) und dann an die Unternehmensstandorte über die Standort-zu-Standort-VPN-Tunnel. .  
  
Außerdem. Rückgabe von Datenverkehr aus dem virtuellen Mandanten Netzwerk an die Remote-Mandanten Unternehmens Site umgeht die slsb, ein Prozess namens Direct Server Return (DSR).  
  
## <a name="how-network-controller-responds-to-ras-gateway-and-route-reflector-failover"></a><a name="bkmk_failover"></a>Reaktion des Netzwerk Controllers auf RAS-Gateway und Weiterleitungs reflektorfailover  
Es folgen zwei mögliche failoverszenarien: eine für RAS-Gatewayclients und eine für RAS-gatewayweiterleitungs-Reflektoren, einschließlich Informationen darüber, wie der Netzwerk Controller Failover für virtuelle Computer in einer der beiden Konfigurationen behandelt.  
  
### <a name="vm-failure-of-a-ras-gateway-bgp-route-reflector-client"></a>VM-Fehler eines RAS-Gateway-BGP-Routen reflektorclients  
Der Netzwerk Controller führt die folgenden Aktionen aus, wenn ein RAS-gatewayclientweiterleitungs-Client ausfällt.  
  
> [!NOTE]  
> Wenn ein RAS-Gateway kein Routen Reflektor für die BGP-Infrastruktur eines Mandanten ist, handelt es sich um einen Routen Reflektor-Client in der BGP-Infrastruktur des Mandanten.  
  
-   Der Netzwerk Controller wählt eine verfügbare Standby-RAS-gatewayvm aus und stellt die neue RAS-Gateway-VM mit der Konfiguration des virtuellen RAS-Gateway-VM bereit  
  
-   Der Netzwerk Controller aktualisiert die zugehörige SLB-Konfiguration, um sicherzustellen, dass die Standort-zu-Standort-VPN-Tunnel von Mandanten Standorten zum nicht erfolgreichen RAS-Gateway ordnungsgemäß mit dem neuen RAS-Gateway eingerichtet werden.  
  
-   Der Netzwerk Controller konfiguriert den BGP-Routen reflektorclient auf dem neuen Gateway.  
  
-   Der Netzwerk Controller konfiguriert den neuen RAS-Gateway-BGP-Routen reflektorclient als aktiv. Das RAS-Gateway startet sofort das Peering mit dem Routen Reflektor des Mandanten, um Routing Informationen freizugeben und das eBGP-Peering für den entsprechenden Unternehmens Standort zu aktivieren.  
  
### <a name="vm-failure-for-a-ras-gateway-bgp-route-reflector"></a>VM-Fehler bei einem RAS-Gateway-BGP-Routen Reflektor  
Der Netzwerk Controller führt folgende Aktionen aus, wenn ein RAS-Gateway-BGP-Routen Reflektor fehlschlägt.  
  
-   Der Netzwerk Controller wählt eine verfügbare Standby-RAS-gatewayvm aus und stellt die neue RAS-Gateway-VM mit der Konfiguration des virtuellen RAS-Gateway-VM bereit  
  
-   Der Netzwerk Controller konfiguriert den Routen Reflektor auf dem neuen virtuellen RAS-Gatewaycomputer und weist dem neuen virtuellen Computer die gleiche IP-Adresse zu, die von der ausgefallenen VM verwendet wurde. Dadurch wird die Routen Integrität trotz des VM-Fehlers bereitgestellt.  
  
-   Der Netzwerk Controller aktualisiert die zugehörige SLB-Konfiguration, um sicherzustellen, dass die Standort-zu-Standort-VPN-Tunnel von Mandanten Standorten zum nicht erfolgreichen RAS-Gateway ordnungsgemäß mit dem neuen RAS-Gateway eingerichtet werden.  
  
-   Der Netzwerk Controller konfiguriert den neuen virtuellen RAS-Gateway-BGP-Routen-reflektorcomputer als aktiv.  
  
-   Der Routen Reflektor wird sofort aktiv. Der Standort-zu-Standort-VPN-Tunnel für das Unternehmen wird eingerichtet, und der Routen Reflektor verwendet die eBGP-Peering-und-Austausch Routen mit den Routern des Unternehmens Standorts.  
  
-   Nach der BGP-Routenauswahl aktualisiert der RAS-Gateway-BGP-Routen Reflektor Mandanten Routen-reflektorclients im Rechenzentrum und synchronisiert Routen mit dem Netzwerk Controller, sodass der End-to-End-Daten Pfad für den Mandanten Datenverkehr verfügbar ist.  
  
## <a name="advantages-of-using-new-ras-gateway-features"></a><a name="bkmk_advantages"></a>Vorteile der Verwendung neuer Features des RAS-Gateways  
Im folgenden finden Sie einige der Vorteile der Verwendung dieser neuen Features des RAS-Gateways beim Entwerfen der RAS-Gatewaybereitstellung.  
  
**Skalierbarkeit des RAS-Gateways**  
  
Da Sie beliebig viele RAS-Gateway-VMS hinzufügen können, können Sie die Bereitstellung des RAS-Gateways problemlos skalieren, um die Leistung und Kapazität zu optimieren. Wenn Sie VMS zu einem Pool hinzufügen, können Sie diese RAS-Gateways mit Site-to-Site-VPN-Verbindungen beliebiger Art (IKEv2, L3, GRE) konfigurieren, sodass Kapazitätsengpässe ohne Downtime vermieden werden.  
  
**Vereinfachte Verwaltung von Enterprise Site Gateway**  
  
Wenn Ihr Mandant über mehrere Unternehmensstandorte verfügt, kann der Mandant alle Standorte mit einer Remote-Standort-zu-Standort-VPN-IP-Adresse und einer einzelnen Remote-Nachbar-IP-Adresse konfigurieren: Ihr CSP-Datacenter RAS-Gateway BGP-Routen Reflektor-VIP für diesen Mandanten. Dies vereinfacht die Gatewayverwaltung für Ihre Mandanten.  
  
**Schnelle Behebung von gatewayfehlern**  
  
Um eine schnelle Failoverantwort zu gewährleisten, können Sie die BGP KeepAlive-Parameter Zeit zwischen den Edge-Routen und dem Steuerelement Router in einem kurzen Zeitintervall (z. b. kleiner oder gleich zehn Sekunden) konfigurieren. Wenn bei diesem kurzen Keep-Alive-Intervall ein RAS-Gateway-BGP-edgerrouter fehlschlägt, wird der Fehler schnell erkannt, und der Netzwerk Controller führt die in den vorherigen Abschnitten beschriebenen Schritte aus. Dieser Vorteil kann die Notwendigkeit eines separaten Protokolls zur Fehlererkennung, wie z. b. das BFD-Protokoll (bidirektionale Weiterleitungs Erkennung), verringern.  
  
 
  


