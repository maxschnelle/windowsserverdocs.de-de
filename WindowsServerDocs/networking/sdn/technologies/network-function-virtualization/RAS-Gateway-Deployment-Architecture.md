---
title: 'RAS-Gateway: Bereitstellungsarchitektur'
description: Sie können in diesem Thema verwenden, Informationen zu Cloud-Dienstanbieter (CSP)-Bereitstellung von RAS-Gateway in Windows Server 2016, einschließlich RAS-Gateway-Pools, Route Reflektoren, und mehrere Gateways für einzelne Mandanten bereitstellen.
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
ms.openlocfilehash: a3895e25a2af0437deb9eebe4ad89b110cfc9f2b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870271"
---
# <a name="ras-gateway-deployment-architecture"></a>RAS-Gateway: Bereitstellungsarchitektur

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, Informationen zu Cloud-Dienstanbieter (CSP) Bereitstellung von RAS-Gateway, einschließlich RAS-Gateway-Pools, Route Reflektoren, und mehrere Gateways für einzelne Mandanten bereitstellen.  
  
Die folgenden Abschnitte enthalten eine kurze Übersicht der neuen Features von RAS-Gateway, damit Sie verstehen können, wie Sie diese Funktionen in den Entwurf der gatewaybereitstellung verwenden.  
  
Darüber hinaus wird eine beispielbereitstellung bereitgestellt, einschließlich Informationen über den Prozess des Hinzufügens neuer Mandanten, Route-Synchronisierung und Daten auf Datenebene routing, Gateway und Route-Reflector-Failover und mehr.  
  
Dieses Thema enthält die folgenden Abschnitte:  
  
-   [Verwenden neue Features für RAS-Gateway zum Entwerfen von Ihrer Bereitstellung](#bkmk_new)  
  
-   [Beispiel für die Bereitstellung](#bkmk_example)  
  
-   [Hinzufügen neuer Mandanten und Kunden (CA) Adressbereich EBGP-Peering](#bkmk_tenant)  
  
-   [Route-Datensynchronisierung und -Verwaltungsebene Routing](#bkmk_route)  
  
-   [Reaktion von Netzwerkcontroller auf RAS-Gateway und das Failover der Route-Reflector](#bkmk_failover)  
  
-   [Vorteile der Verwendung der neuen Features von RAS-Gateway](#bkmk_advantages)  
  
## <a name="bkmk_new"></a>Verwenden neue Features für RAS-Gateway zum Entwerfen von Ihrer Bereitstellung  
RAS-Gateway enthält mehrere neue Features, die ändern und verbessern die Möglichkeit, in der Sie Ihre Gateway-Infrastruktur in Ihrem Datencenter bereitstellen.  
  
### <a name="bgp-route-reflector"></a>BGP-Route-Reflector  
Die Border Gateway Protocol (BGP)-Route-Reflector-Funktion ist jetzt mit der RAS-Gateway enthalten und stellt eine Alternative zur BGP-full-Mesh-Topologie, die normalerweise für die Route-Synchronisierung zwischen Routern erforderlich ist. Bei der Synchronisierung vollständig vermaschte müssen alle BGP-Router mit allen anderen Routern in die Routingtopologie verbinden. Bei Verwendung von Route-Reflector ist die Route-Reflector jedoch der einzige Router, der mit allen anderen Routern, BGP-Route-Reflector-Clients, um so Route Synchronisierung zu vereinfachen und Reduzierung des Netzwerkverkehrs wird aufgerufen, eine Verbindung herstellt. Die Route-Reflector lernt alle Routen, berechnet der beste Routen und die beste Routen zu den BGP-Clients verteilt.  
  
Weitere Informationen finden Sie unter [Neuigkeiten in der RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md).  
  
### <a name="bkmk_pools"></a>Gatewaypools  
In Windows Server 2016 können Sie viele gatewaypools verschiedener Typen erstellen. Gatewaypools enthalten viele Instanzen des RAS-Gateway und Weiterleiten von Netzwerkdatenverkehr zwischen physischen und virtuellen Netzwerken.  
  
Weitere Informationen finden Sie unter [Neuigkeiten in der RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) und [RAS-Gateway: hohe Verfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
### <a name="bkmk_gps"></a>Gateway-Pool-Skalierbarkeit  
Sie können ganz einfach einen gatewaypool nach oben oder unten skalieren durch Hinzufügen oder Entfernen der Gateway-VMs im Pool. Entfernen oder Hinzufügen des Gateways ist nicht die Dienste unterbrochen werden, die von einem Pool bereitgestellt werden. Sie können auch hinzufügen und entfernen die gesamte Pools von Gateways.  
  
Weitere Informationen finden Sie unter [Neuigkeiten in der RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) und [RAS-Gateway: hohe Verfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
### <a name="bkmk_m"></a>Gateway-Pool-Redundanz M + N  
Jede gatewaypool ist M + N ist redundant. Dies bedeutet, dass ein bin "Anzahl der aktiven Gateway-VMs werden" n "die Anzahl der standby-Gateway-VMs gesichert. M + N-Redundanz bietet mehr Flexibilität bei der Bestimmung der Grad an Zuverlässigkeit, die beim Bereitstellen des RAS-Gateways erforderlich sind.  
  
Weitere Informationen finden Sie unter [Neuigkeiten in der RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md) und [RAS-Gateway: hohe Verfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_example"></a>Beispiel für die Bereitstellung  
Die folgende Abbildung zeigt ein Beispiel mit eBGP-peering über Standort-zu-Standort-VPN-Verbindungen zwischen zwei Mandanten, Contoso und Fabrikam-CSP-Datencenter und Woodgrove konfiguriert.  
  
![eBGP-peering über Standort-zu-Standort-VPN](../../../media/RAS-Gateway-Deployment-Architecture/ras_gateway_architecture.png)  
  
In diesem Beispiel erfordert Contoso zusätzliche Bandbreite, zu der Gateway-Infrastruktur entwurfsentscheidung Standort Contoso Los Angeles auf GW3 statt GW2 beendet. Beenden Contoso-VPN-Clientverbindungen von verschiedenen Standorten aus diesem Grund in CSP-Datencenter zu zwei verschiedenen Gateways.  
  
Beide dieser Gateways, GW2 und GW3, Waren der erste RAS-Gateways, die vom Netzwerkcontroller konfiguriert werden, wenn der CSP die Mandanten von Contoso und Woodgrove für ihre Infrastruktur hinzugefügt. Aus diesem Grund werden diese zwei Gateways als Route Reflektoren für diesen entsprechenden Kunden (oder Mandanten) konfiguriert. GW2 ist die Contoso-Route-Reflector und GW3 ist das Woodgrove-Route-Reflector - abgesehen davon, dass der CSP-RAS-Gateway-Endpunkt für die VPN-Verbindung mit dem Contoso Los Angeles HQ-Standort.  
  
> [!NOTE]  
> Eine RAS-Gateways können virtuelle und physische Netzwerkdatenverkehr für bis zu 100 verschiedenen Mandanten, je nach den Anforderungen an die Netzwerkbandbreite der einzelnen Mandanten weiterleiten.  
  
Als Route Reflektoren GW2 sendet Contoso Kundenadressraum Routen für den Netzwerkcontroller und GW3 sendet Woodgrove-Kundenadressraum Routen für den Netzwerkcontroller.  
  
Netzwerkcontroller überträgt Hyper-V-Netzwerkvirtualisierungs-Richtlinien auf die Contoso und Woodgrove virtuelle Netzwerke als auch RAS-Richtlinien auf die RAS-Gateways und den Lastenausgleich von Richtlinien für die Multiplexers (/ MUX), die als Software Load Balancing konfiguriert sind Dieser Pool.  
  
## <a name="bkmk_tenant"></a>Hinzufügen neuer Mandanten und Kundenadressraum (CA) Speicherplatz eBGP Peering  
Melden Sie einen neuen Kunden und dem Hinzufügen des Kunden als einen neuen Mandanten in Ihrem Datencenter, können Sie den folgenden Prozess, der vieles von dem Netzwerkcontroller und RAS-Gateway eBGP-Router automatisch ausgeführt wird.  
  
1.  Stellen Sie ein neues virtuelles Netzwerk und arbeitsauslastungen entsprechend den Anforderungen der Ihres Mandanten bereit.  
  
2.  Konfigurieren Sie bei Bedarf remote-Konnektivität zwischen der remote-mandantenwebsite Enterprise und ihrem virtuellen Netzwerk in Ihrem Rechenzentrum. Wenn Sie eine Standort-zu-Standort-VPN-Verbindung für den Mandanten bereitstellen, wählt eine verfügbare RAS-Gateway-VM aus dem Pool der verfügbaren Gateway Netzwerkcontroller automatisch und konfiguriert die Verbindung.  
  
3.  Beim Konfigurieren der RAS-Gateway-VM für den neuen Mandanten, den Netzwerkcontroller außerdem das RAS-Gateway als BGP-Router konfiguriert und kennzeichnet es als die Route-Reflector für den Mandanten. Dies gilt auch in Situationen, in denen dient das RAS-Gateway als Gateway oder als ein Gateway und die Route-Reflector, für andere Mandanten.  
  
4.  Je nachdem, ob Zertifizierungsstelle Speicherplatz routing zu verwenden, die statisch konfiguriert-Netzwerken oder dynamische BGP-routing konfiguriert ist konfiguriert den Netzwerkcontroller an die entsprechenden statischen Routen, BGP-Nachbarn oder beides auf dem RAS-Gateway-VM und die Route-Reflector.  
  
    > [!NOTE]  
    > -   Nach dem Netzwerkcontroller einen RAS-Gateway und die Route-Reflector für den Mandanten konfiguriert hat, erfordert jedes Mal, wenn des gleichen Mandantenverwaltungs einer neuen Standort-zu-Standort-VPN-Verbindungs Netzwerkcontroller überprüft die verfügbare Kapazität auf diesem virtuellen Computer RAS-Gateway. Wenn das ursprüngliche-Gateway die erforderliche Kapazität bedienen kann, wird die neue Verbindung auch auf der gleichen RAS-Gateway-VM konfiguriert. Wenn der RAS-Gateway-VM zusätzlichen Kapazität nicht verarbeiten kann, wird dem Netzwerkcontroller wählt eine neue verfügbare RAS-Gateway-VM und konfiguriert die neue Verbindung auf. Diese neue RAS-Gateway-VM, dem Mandanten zugeordnet wird, der Route-Reflector-Client des ursprünglichen RAS-Gateway-Route-Reflector-Mandanten.  
    > -   Da RAS-Gateway-Pools hinter einem Load Balancer für die Software (SLBs) sind, bezeichnet der Mandanten-Standort-zu-Standort-VPN-Adressen, die jeweils eine einzelne öffentliche IP-Adresse wird aufgerufen, eine virtuelle IP-Adresse (VIP), die von der die SLBs in einer internen Datacenter-IP-Adresse übersetzt wird, verwenden Sie eine dynamische IP-Adresse (DIP), ein RAS-Gateway das Weiterleiten des Datenverkehrs für den Enterprise-Mandanten. Diese öffentliche, Private IP-Adresszuordnung von SLB wird sichergestellt, dass die Standort-zu-Standort-VPN-Tunnel zwischen den Enterprise-Standorten und CSP-RAS-Gateways und Route Reflektoren ordnungsgemäß eingerichtet werden.  
    >   
    >     Weitere Informationen zu den SLB-VIPs und DIPs finden Sie unter [Softwarelastenausgleich &#40;SLB&#41; für SDN](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).  
  
5.  Nach dem der Standort-zu-Standort-VPN-Tunnel zwischen der Enterprise-Website und dem CSP-Datencenter, die, das RAS-Gateway, für den neuen Mandanten hergestellt wird, werden die statischen Routen, die die Tunnel zugeordnet sind, automatisch auf sowohl die Unternehmens- und CSP-Seiten des Tunnels bereitgestellt .  
  
6.  Mit kundenadressraum BGP wird-routing, die eBGP-peering zwischen den Enterprise-Standorten und der CSP-RAS-Gateway-Route-Reflector auch hergestellt.  
  
## <a name="bkmk_route"></a>Route-Datensynchronisierung und -Verwaltungsebene Routing  
Nachdem eBGP-peering zwischen Enterprise-Standorten und der CSP-RAS-Gateway-Route-Reflector hergestellt wurde, lernt die Route-Reflector alle Routen Enterprise mithilfe von dynamischen BGP-routing. Die Route-Reflector synchronisiert diese Routen zwischen allen Clients Route-Reflector, sodass sie alle mit den gleichen Satz von Routen konfiguriert sind.  
  
Route-Reflector aktualisiert auch diese konsolidierten Routen, mit der Route Synchronisierung für den Netzwerkcontroller. Netzwerkcontroller klicken Sie dann die Routen in der Hyper-V-Netzwerkvirtualisierungs-Richtlinien übersetzt und konfiguriert das Netzwerk-Fabric, um sicherzustellen, dass die End-to-End-Datenpfad routing bereitgestellt wird. Dieser Prozess wird der Mandant virtuelle Netzwerk zugegriffen werden kann, aus dem Enterprise-Mandanten Websites.  
  
Für die Datenebene routing, werden die Pakete, die das RAS-Gateway-VMs zu erreichen direkt mit dem virtuellen mandantennetzwerk, weitergeleitet, da die erforderlichen Routen jetzt mit allen Beteiligten RAS-Gateway-VMs verfügbar sind.  
  
Auf ähnliche Weise mit den Hyper-V-Netzwerkvirtualisierung Richtlinien vorhanden, das virtuelle Netzwerk des Mandanten leitet die Pakete weiter direkt an den RAS-Gateway-VMs (ohne dass über die Route-Reflector wissen) und klicken Sie dann auf die Enterprise-Websites über die Standort-zu-Standort-VPN-Tunnel .  
  
Außerdem. der antwortdatenverkehr über das virtuelle Netzwerk des Mandanten, der remote-mandantenwebsite Enterprise umgeht die SLBs, einen Prozess namens Direct Server Return (DSR).  
  
## <a name="bkmk_failover"></a>Reaktion von Netzwerkcontroller auf RAS-Gateway und das Failover der Route-Reflector  
Es folgen zwei mögliche Failoverszenarien: einer für RAS-Gateway-Route-Reflector-Clients – und eine für RAS-Gateway Route Reflektoren einschließlich Informationen wie den Netzwerkcontroller Failover für virtuelle Computer in beiden Konfiguration behandelt.  
  
### <a name="vm-failure-of-a-ras-gateway-bgp-route-reflector-client"></a>VM-Ausfall, der eine RAS-Gateway-BGP-Route-Reflector-Client  
Netzwerkcontroller führt die folgenden Aktionen aus, wenn ein RAS-Gateway-Route-Reflector-Client ein Fehler auftritt.  
  
> [!NOTE]  
> Wenn ein RAS-Gateway nicht mit einer Route-Reflector für BGP-Infrastruktur eines Mandanten ist, ist es ein Route-Reflector-Client in der Mandanten-BGP-Infrastruktur.  
  
-   Netzwerkcontroller wählt eine verfügbare standby-RAS-Gateway-VM und die neue RAS-Gateway-VM mit der Konfiguration der fehlerhaften RAS-Gateway-VM bereitgestellt.  
  
-   Netzwerkcontroller aktualisiert die entsprechenden SLB-Konfiguration, um sicherzustellen, dass die Standort-zu-Standort-VPN-Tunnel von mandantenwebsites mit dem fehlerhaften RAS-Gateway mit dem neuen RAS-Gateway ordnungsgemäß eingerichtet werden.  
  
-   Netzwerkcontroller konfiguriert den BGP-Route-Reflector-Client auf dem neuen Gateway.  
  
-   Netzwerkcontroller wird den neuen RAS-Gateway BGP-Route-Reflector-Client als aktiv konfiguriert. Das RAS-Gateway startet sofort, peering mit der Mandanten-Route-Reflector zum Routinginformationen auch eBGP-peering für die entsprechenden Enterprise-Website zu aktivieren.  
  
### <a name="vm-failure-for-a-ras-gateway-bgp-route-reflector"></a>Fehler bei der virtuellen Computer für eine RAS-Gateway-BGP-Route-Reflector  
Netzwerkcontroller führt die folgenden Aktionen aus, wenn ein RAS-Gateway-BGP-Route-Reflector ein Fehler auftritt.  
  
-   Netzwerkcontroller wählt eine verfügbare standby-RAS-Gateway-VM und die neue RAS-Gateway-VM mit der Konfiguration der fehlerhaften RAS-Gateway-VM bereitgestellt.  
  
-   Netzwerkcontroller die Route-Reflector konfiguriert, auf die neue RAS-Gateway-VM und weist dem neuen virtuellen Computer die gleiche IP-Adresse, die von der fehlerhaften virtuellen Maschine, wodurch die Integrität der Route trotz des Fehlers VM verwendet wurde.  
  
-   Netzwerkcontroller aktualisiert die entsprechenden SLB-Konfiguration, um sicherzustellen, dass die Standort-zu-Standort-VPN-Tunnel von mandantenwebsites mit dem fehlerhaften RAS-Gateway mit dem neuen RAS-Gateway ordnungsgemäß eingerichtet werden.  
  
-   Netzwerkcontroller wird die neue RAS-Gateway BGP Route Reflector-VM als aktiv konfiguriert.  
  
-   Die Route-Reflector wird sofort aktiv. Der Standort-zu-Standort-VPN-Tunnel für das Unternehmen wird hergestellt, und die Route-Reflector verwendet eBGP-peering und tauscht Routen mit dem Enterprise-Standort-Routern.  
  
-   Nach Auswahl der BGP-Route die RAS-Gateway BGP-Route-Reflector-Updates Mandanten-Route-Reflector-Clients im Datencenter und Routen mit dem Netzwerkcontroller, Verfügbarmachen des End-to-End-Datenpfads für mandantendatenverkehr synchronisiert.  
  
## <a name="bkmk_advantages"></a>Vorteile der Verwendung der neuen Features von RAS-Gateway  
Nachfolgend sind einige der Vorteile der Verwendung dieser neuen Features für RAS-Gateway, beim Entwerfen der RAS-Gateway-Bereitstellung.  
  
**RAS-Gateway-Skalierbarkeit**  
  
Da Sie so viele RAS-Gateway-VMs als RAS-Gateway-Pools müssen hinzufügen können, können Sie die RAS-Gateway-Bereitstellung, um das Optimieren der Leistung und Kapazität ganz einfach skalieren. Wenn Sie virtuelle Computer zu einem Pool hinzufügen, können Sie diese RAS-Gateways mit Standort-zu-Standort-VPN-Verbindungen jeglicher Art (IKEv2, L3, GRE), entfernen Kapazitätsengpässen ohne Downtime zu konfigurieren.  
  
**Vereinfachte Enterprise Gateway Standortverwaltung**  
  
Wenn Ihr Mandant mehrere Unternehmensstandorte verfügt, kann Mandanten alle Standorte mit einer remote-Standort-zu-Standort-VPN IP-Adresse und einen einzelnen Remoteserver Nachbar-IP-Adresse - Ihrem CSP-Datencenter-RAS-Gateway-BGP-Route-Reflector VIP für den Mandanten konfigurieren. Dies vereinfacht das Verwalten des Gateways für Ihre Mandanten.  
  
**Schnelle Wiederherstellung der Gateway-Fehler**  
  
Um ein schnelles Failover-Antwort zu gewährleisten, können Sie die BGP-Keepalive Parameter Zeit zwischen den Edge-Routen und ein Intervall kurz, wie z. B. kleiner als oder gleich zehn Sekunden der Steuerelement-Router konfigurieren. Mit diesem kurzen Keep-alive-Intervall Wenn ein RAS-Gateway-BGP-edgerouter ein Fehler auftritt, der Fehler schnell erkannt und Netzwerkcontroller folgt den Schritten, die in den vorherigen Abschnitten bereitgestellt. Dieser Vorteil kann die Notwendigkeit, eine separate Fehler Erkennung-Protokoll, z. B. bidirektionale Weiterleitung Erkennung (BFD)-Protokoll reduzieren.  
  
 
  


