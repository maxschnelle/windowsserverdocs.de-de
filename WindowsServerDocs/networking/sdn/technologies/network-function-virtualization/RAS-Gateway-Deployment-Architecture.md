---
title: 'RAS-Gateway: Bereitstellungsarchitektur'
description: In diesem Thema können Sie die Informationen (Cloud Service Provider, CSP) Bereitstellung von RAS-Gateway in Windows Server2016, einschließlich der RAS-Gateway-Pools Route gilt, und mehrere Gateways für die einzelnen Mandanten bereitstellen.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d46e4e91-ece0-41da-a812-af8ab153edc4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 21b101e10dba3d3b9578d6804b4fd92fbbcd2167
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="ras-gateway-deployment-architecture"></a>RAS-Gateway: Bereitstellungsarchitektur

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie die Informationen (Cloud Service Provider, CSP) Bereitstellung von RAS-Gateway, einschließlich der RAS-Gateway-Pools Route gilt, und mehrere Gateways für die einzelnen Mandanten bereitstellen.  
  
Die folgenden Abschnitte enthalten eine kurze Übersicht über einige der neuen Features für RAS-Gateway, daher wissen, wie diese Features in das Design der gatewaybereitstellung verwenden können.  
  
Darüber hinaus wird eine beispielbereitstellung bereitgestellt, einschließlich Informationen zum Hinzufügen von neuen Mandanten, Route Synchronisierung und Daten Ebene Routing, Gateways und Route-Reflector Failover und mehr.  
  
Dieses Thema enthält die folgenden Abschnitte.  
  
-   [Verwenden neue Features für RAS-Gateway zum Entwerfen Ihrer Bereitstellung](#bkmk_new)  
  
-   [Beispiel für eine Bereitstellung](#bkmk_example)  
  
-   [Hinzufügen von neuen Mandanten und Kunden (CA) Adressraum EBGP-Peering](#bkmk_tenant)  
  
-   [Route-Synchronisierung und Daten-Ebene Routing](#bkmk_route)  
  
-   [Wie reagiert Netzwerkcontroller RAS-Gateway und Route-Reflector-Failover](#bkmk_failover)  
  
-   [Vorteile der Verwendung der neuen Features der RAS-Gateway](#bkmk_advantages)  
  
## <a name="bkmk_new"></a>Verwenden neue Features für RAS-Gateway zum Entwerfen Ihrer Bereitstellung  
RAS-Gateway enthält mehrere neue Features, die ändern und verbessern die Art und Weise, in der die Gateway-Infrastruktur in Ihrem Datencenter bereitstellen.  
  
### <a name="bgp-route-reflector"></a>BGP-Route-Reflector  
Das Border Gateway Protocol (BGP) Route-Reflector-Funktion ist jetzt mit RAS-Gateway enthalten und stellt eine Alternative zu BGP-full-Mesh-Topologie, die für die Route Synchronisierung zwischen Router normalerweise erforderlich ist. Mit full-Mesh-Synchronisierung müssen alle BGP-Router mit allen Routern in die Weiterleitungstopologie verbinden. Bei Verwendung der Route-Reflector ist die Route-Reflector jedoch nur Routers, der mit allen anderen Routern, BGP-Route-Reflector-Clients, dadurch vereinfacht Route Synchronisierung und Reduzierung des Netzwerkverkehrs bezeichnet eine Verbindung herstellt. Die Route-Reflector lernt alle Routen, berechnet der beste Routen und die besten Routen zu den BGP-Clients verteilt.  
  
Weitere Informationen finden Sie unter [What's New in RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md).  
  
### <a name="bkmk_pools"></a>Gateway-Pools  
In Windows Server2016 können Sie viele Gateway Pools verschiedener Typen erstellen. Gateway-Pools enthalten viele Instanzen des RAS-Gateway und Weiterleiten von Netzwerkdatenverkehr zwischen physischen und virtuellen Netzwerken.  
  
Weitere Informationen finden Sie unter [What's New in RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) und [RAS-Gateway: hohe Verfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
### <a name="bkmk_gps"></a>Gateway-Pool Skalierbarkeit  
Sie können ganz einfach einen Gateway-Pool nach oben oder unten skalieren durch Hinzufügen oder Entfernen der Gateway-VMs im Pool. Zum Entfernen oder Hinzufügen eines Gateways wird nicht die Dienste unterbrochen werden, die von einem Pool bereitgestellt werden. Sie können auch hinzufügen und entfernen ganze Pools von Gateways.  
  
Weitere Informationen finden Sie unter [What's New in RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) und [RAS-Gateway: hohe Verfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
### <a name="bkmk_m"></a>M + N Gateway-Pool-Redundanz  
Alle Gateway-Pool ist M + N redundant. Dies bedeutet, dass eine bin "Anzahl der aktiven Gateway-VMs" n "die Anzahl der Standby-Gateway-VMs gesichert werden. M + N Redundanz bietet Ihnen mehr Flexibilität bei der Bestimmung der Maß an Zuverlässigkeit, die Sie benötigen, wenn Sie RAS-Gateway bereitstellen.  
  
Weitere Informationen finden Sie unter [What's New in RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) und [RAS-Gateway: hohe Verfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_example"></a>Beispiel für eine Bereitstellung  
Die folgende Abbildungenthält ein Beispiel mit eBGP-Peering über Standort-zu-Standort-VPN-Verbindungen zwischen zwei Mandanten, Contoso und Fabrikam-CSP-Datencenter und Woodgrove konfiguriert.  
  
![eBGP-Peering über Standort-zu-Standort-VPN](../../../media/RAS-Gateway-Deployment-Architecture/ras_gateway_architecture.png)  
  
In diesem Beispiel erfordert Contoso zusätzliche Gateway Bandbreite, zu der Gateway-Infrastruktur Entscheidung Standort Contoso Los Angeles auf GW3 anstelle von GW2 beendet. Aus diesem Grund beendet werden Contoso VPN-Verbindungen von verschiedenen Standorten in der CSP-Datencenter auf zwei verschiedenen Gateways.  
  
Beide dieser Gateways, GW2 und GW3, wurden die erste RAS-Gateways von Netzwerkcontroller konfiguriert werden, wenn der CSP die Contoso und Woodgrove-Mandanten ihrer Infrastruktur hinzugefügt. Aus diesem Grund werden diese zwei Gateways als Route gilt für diesen jeweiligen Kunden (oder Mandanten) konfiguriert. GW2 der Contoso-Route-Reflector und GW3 der Woodgrove Route-Reflector - abgesehen davon, dass die CSP-RAS-Gateway-Endpunkt für die VPN-Verbindung mit dem Standort Contoso Los Angeles Hochwertiges.  
  
> [!NOTE]  
> Ein RAS-Gateway kann für bis zu 100 verschiedenen Mandanten, abhängig von den bandbreitenanforderungen für jeden Mandanten virtuelle und physische Netzwerkverkehr weiterleiten.  
  
Als Route trägt GW2 sendet Kundenadressraum Contoso-Routen an Netzwerkcontroller und GW3 Kundenadressraum Woodgrove-Routen an Netzwerkcontroller gesendet.  
  
Netzwerkcontroller wird Hyper-V-netzwerkvirtualisierungsrichtlinien an die Contoso und Woodgrove virtuelle Netzwerke sowie RAS-Richtlinien für die RAS-Gateways und Lastenausgleichsrichtlinien, die Multiplexers (MUXes), die als Netzwerklastenausgleich-Software-Pool konfiguriert sind.  
  
## <a name="bkmk_tenant"></a>Hinzufügen von neuen Mandanten und Kundenadressraum (CA) Speicherplatz eBGP Peering  
Melden Sie einen neuen Kunden und dem Hinzufügen der Kunde als einen neuen Mandanten im Rechenzentrum, können Sie das folgende Verfahren, von denen von Netzwerkcontroller und RAS-Gateway eBGP-Router automatisch ausgeführt wird.  
  
1.  Stellen Sie ein neues virtuelles Netzwerk und Workloads entsprechend Ihrem Mandanten Anforderungen bereit.  
  
2.  Konfigurieren Sie bei Bedarf Remote-Konnektivität zwischen dem Remote-Mandanten Enterprise-Standort und seinem virtuellen Netzwerk auf Ihrem Datencenter. Wenn Sie eine Standort-zu-Standort-VPN-Verbindung für den Mandanten bereitstellen, wählt einen verfügbaren RAS-Gateway-VM aus dem Pool verfügbares Gateway Netzwerkcontroller automatisch und konfiguriert die Verbindung.  
  
3.  Beim Konfigurieren der RAS-Gateway-VM für den neuen Mandanten, Netzwerkcontroller auch der RAS-Gateway als BGP-Router konfiguriert und wird als Route-Reflector für den Mandanten bestimmt. Dies gilt auch in Fällen, in denen dient der RAS-Gateway als Gateway oder als Gateway und Route-Reflector für andere Mandanten.  
  
4.  Je nachdem, ob Zertifizierungsstelle Speicherplatz Routing zu verwenden, die statisch konfigurierte Netzwerke oder dynamische BGP-Routing konfiguriert ist konfiguriert Netzwerkcontroller die entsprechenden statischen Routen, BGP Nachbarn oder sowohl auf dem RAS-Gateway-VM und Route-Reflector.  
  
    > [!NOTE]  
    > -   Nach dem Netzwerkcontroller konfiguriert hat einen RAS-Gateway und Route-Reflector für Mandanten, wenn die gleiche Mandanten eine neue Standort-zu-Standort-VPN-Verbindung benötigt Netzwerkcontroller überprüft, ob die verfügbare Kapazität dieses RAS-Gateway-VM. Wenn das ursprüngliche Gateway die erforderliche Kapazität bedienen kann, ist die neue Netzwerkverbindung auch auf dem gleichen RAS-Gateway-VM konfiguriert. Wenn der RAS-Gateway-VM zusätzlichen Kapazität nicht verarbeiten kann, wird Netzwerkcontroller wählt eine neue verfügbaren RAS-Gateway-VM und die neue Verbindung darauf konfiguriert. Diese neue RAS-Gateway-VM mit Mandanten verknüpft ist, wird die Route-Reflector-Client des ursprünglichen Mandanten RAS-Gateway-Route-Reflector.  
    > -   Da RAS-Gateway-Pools hinter Software Load Balancers (SLBs) befinden, Adressen des Mandanten-Standort-zu-Standort-VPN-jede Verwendung eine einzelne IP-Adresse, eine virtuelle IP-Adresse (VIP), die durch die SLBs in einer Datacenter-interne IP-Adresse, bezeichnet eine dynamische IP-Adresse (DIP), für das Weiterleiten des Datenverkehrs für die Enterprise-Mandanten RAS-Gateway übersetzt wird aufgerufen. Diese öffentliche, Private IP-Adresszuordnung von SLB wird sichergestellt, dass die Standort-zu-Standort-VPN-Tunnel zwischen der Enterprise-Websites und die CSP-RAS-Gateways und Route gilt ordnungsgemäß eingerichtet werden.  
    >   
    >     Weitere Informationen zu SLB VIPs und DIP, finden Sie unter [Lastenausgleich & 40; SLB & 41; für SDN](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).  
  
5.  Nachdem der Standort-zu-Standort-VPN-Tunnel zwischen dem Unternehmen und CSP-Datencenter, das für den neuen Mandanten RAS-Gateway hergestellt wird, werden die statischen Routen, die die IPsec-Tunnel zugeordnet sind auf die Enterprise und die CSP-Seiten des Tunnels automatisch bereitgestellt.  
  
6.  Kundenadressraum BGP ist-Routing, die eBGP-Peering zwischen der Enterprise-Websites und die CSP-RAS-Gateway-Route-Reflector auch hergestellt.  
  
## <a name="bkmk_route"></a>Route-Synchronisierung und Daten-Ebene Routing  
Nachdem eBGP-Peering zwischen Unternehmensstandorte und die CSP-RAS-Gateway-Route-Reflector eingerichtet ist, lernt Route-Reflector alle Enterprise-Routen mithilfe der dynamischen BGP-Routing. Die Route-Reflector synchronisiert diese Routen zwischen allen Clients Route-Reflector, damit sie alle mit den gleichen Satz von Routen konfiguriert werden.  
  
Route-Reflector aktualisiert auch diese konsolidierten Routen mit Route Synchronisierung Netzwerkcontroller. Netzwerkcontroller ist dann übersetzt die Routen in der Hyper-V-Netzwerkvirtualisierungs-Richtlinien und konfiguriert die Fabric-Netzwerk, um sicherzustellen, dass End-to-End Datenpfad Routing bereitgestellt wird. Dadurch wird der Mandant virtuelle Netzwerk des Mandanten Enterprise auf Websites.  
  
Für die Weiterleitung von Daten Ebene werden die Pakete, die das RAS-Gateway-VMs erreichen direkt mit der Mandant virtuellen Netzwerk, weitergeleitet, da die erforderlichen Routen jetzt mit allen teilnehmenden RAS-Gateway-VMs verfügbar sind.  
  
Auf ähnliche Weise Routen mit dem Hyper-V-Netzwerkvirtualisierung Richtlinien, das virtuelle Netzwerk des Mandanten Pakete direkt an den RAS-Gateway-VMs (ohne die Route-Reflector kennen) und klicken Sie dann auf die Enterprise-Websites über die Standort-zu-Standort-VPN-Tunnel.  
  
Außerdem. Rückgabe von Daten aus dem virtuellen Netzwerk des Mandanten auf den Remote-Mandanten Unternehmensstandort umgeht die SLBs, der so genannten direkte Server zurückgegeben (DSR).  
  
## <a name="bkmk_failover"></a>Wie reagiert Netzwerkcontroller RAS-Gateway und Route-Reflector-Failover  
Es folgen zwei mögliche Failover-Szenarien – eine für RAS-Gateway-Route-Reflector Clients- und eine für RAS-Gateway Route gilt einschließlich Informationen dazu, wie Netzwerkcontroller Failover für virtuelle Maschinen in der Konfiguration behandelt.  
  
### <a name="vm-failure-of-a-ras-gateway-bgp-route-reflector-client"></a>VM-Fehler von einem RAS-Gateway BGP-Route-Reflector-Client  
Netzwerkcontroller führt die folgenden Aktionen aus, wenn ein RAS-Gateway-Route-Reflector-Client ein Fehler auftritt.  
  
> [!NOTE]  
> Wenn ein RAS-Gateway nicht um eine Route-Reflector für einen Mandanten BGP-Infrastruktur ist, wird eine Route-Reflector-Client in der Mandant BGP-Infrastruktur.  
  
-   Netzwerkcontroller einen verfügbaren Standby-RAS-Gateway-VM wählt und stellt die neue RAS-Gateway-VM mit der fehlgeschlagenen RAS-Gateway-VM-Konfiguration.  
  
-   Netzwerkcontroller aktualisiert die entsprechende SLB-Konfiguration, um sicherzustellen, dass die Standort-zu-Standort-VPN-Tunnel von Mandanten Standorten mit dem fehlerhaften RAS-Gateway mit dem neuen RAS-Gateway ordnungsgemäß eingerichtet werden.  
  
-   Netzwerkcontroller konfiguriert den BGP-Route-Reflector-Client auf dem neuen Gateway.  
  
-   Netzwerkcontroller wird den neuen RAS-Gateway-BGP Route-Reflector-Client als aktiv konfiguriert. Der RAS-Gateway wird sofort gestartet, mit der Mandant Route-Reflector Routinginformationen freigeben und zum Aktivieren von eBGP-Peering für den entsprechenden Unternehmensstandort Peering.  
  
### <a name="vm-failure-for-a-ras-gateway-bgp-route-reflector"></a>VM-Fehler für einen RAS-Gateway-BGP-Route-Reflector  
Netzwerkcontroller führt die folgenden Aktionen aus, wenn ein RAS-Gateway-BGP-Route-Reflector fehlschlägt.  
  
-   Netzwerkcontroller einen verfügbaren Standby-RAS-Gateway-VM wählt und stellt die neue RAS-Gateway-VM mit der fehlgeschlagenen RAS-Gateway-VM-Konfiguration.  
  
-   Netzwerkcontroller konfiguriert die Route-Reflector auf die neue RAS-Gateway-VM, und weist der neuen virtuelle Maschine die gleiche IP-Adresse, die von der fehlerhaften virtuellen Maschine, wodurch Route Integrität trotz des VM-Fehlers verwendet wurde.  
  
-   Netzwerkcontroller aktualisiert die entsprechende SLB-Konfiguration, um sicherzustellen, dass die Standort-zu-Standort-VPN-Tunnel von Mandanten Standorten mit dem fehlerhaften RAS-Gateway mit dem neuen RAS-Gateway ordnungsgemäß eingerichtet werden.  
  
-   Netzwerkcontroller wird die neue RAS-Gateway BGP Route Reflector virtuelle Maschine als aktiv konfiguriert.  
  
-   Die Route-Reflector wird sofort verfügbar. Der Standort-zu-Standort-VPN-Tunnel für das Unternehmen eingerichtet wurde, und die Route-Reflector eBGP-Peering verwendet und tauscht Routen mit den Routern der Enterprise-Website.  
  
-   Nach Auswahl der BGP-Route die RAS-Gateway-BGP Route-Reflector-Updates für den Mandanten Route-Reflector-Clients im Datencenter, und synchronisiert die Routen mit Netzwerkcontroller, End-to-End Datenpfad für Mandantendatenverkehr verfügbar machen.  
  
## <a name="bkmk_advantages"></a>Vorteile der Verwendung der neuen Features der RAS-Gateway  
Nachfolgend sind einige der Vorteile der Verwendung dieser neuen Features für RAS-Gateway beim Entwerfen der RAS-Gateway-Bereitstellung.  
  
**RAS-Gateway Skalierbarkeit**  
  
Da Sie so viele RAS-Gateway-VMs als RAS-Gateway-Pools müssen hinzufügen können, können Sie einfach die RAS-Gateway-Bereitstellung, zur Optimierung der Leistung und Kapazität skalieren. Wenn Sie virtuelle Maschinen zu einem Pool hinzufügen, können Sie diese RAS-Gateways mit Standort-zu-Standort-VPN-Verbindungen jeglicher Art (IKEv2, L3, GRE), wobei Kapazität Engpässe ohne Ausfallzeiten konfigurieren.  
  
**Vereinfachte Enterprise Site-Gateway-Verwaltung**  
  
Wenn Ihre Mandanten mehrere Unternehmensstandorte verfügt, kann Mandanten alle Standorte mit einem Remote-Standort-zu-Standort-VPN-IP-Adresse und eine einzelne remote benachbarten IP-Adresse - Ihre CSP-Datencenter-RAS-Gateway BGP-Route-Reflector VIP für die Mandanten konfigurieren. Dies vereinfacht die Verwaltung der Gateway für Ihre Mandanten.  
  
**Schnelle Wiederherstellung der Gateway-Fehler**  
  
Um eine schnelle Failover-Antwort zu gewährleisten, können Sie die BGP-Keep-Alive-Parameter Zeit zwischen den Rand von Routen und der Steuerelement-Router mit einem Intervall von kurzer Zeit, z.B. kleiner als oder gleich zehn Sekunden konfigurieren. Mit diesem kurzen Keep-alive-Intervall, wenn ein Fehler auf ein RAS-Gateway-BGP-Edge-Router, der Fehler schnell erkannt und der Netzwerkcontroller folgt die Schrittein den vorherigen Abschnitten. Dieser Vorteil kann die Notwendigkeit für eine separate Fehler bei der Erkennung, z.B. bidirektionale weiterleiten Erkennung (BFD)-Protokoll reduzieren.  
  
 
  


