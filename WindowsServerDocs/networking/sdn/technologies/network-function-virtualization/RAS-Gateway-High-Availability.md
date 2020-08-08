---
title: 'RAS-Gateway: Hohe Verfügbarkeit'
description: In diesem Thema erfahren Sie mehr über Konfigurationen für hohe Verfügbarkeit für das mehr Instanzen fähige RAS-Gateway für Software-Defined Networking (SDN) in Windows Server 2016.
manager: grcusanz
ms.topic: get-started-article
ms.assetid: 34d826c9-65bc-401f-889d-cf84e12f0144
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: 0bdf116aeb8f154290b528b9ba96fbb4a8b34426
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969557"
---
# <a name="ras-gateway-high-availability"></a>RAS-Gateway: Hohe Verfügbarkeit

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie mehr über Konfigurationen mit hoher Verfügbarkeit für das mehr Instanzen fähige RAS-Gateway für Software-Defined Networking (SDN).

Dieses Thema enthält folgende Abschnitte:

-   [Übersicht über RAS-Gateways](#bkmk_overview)

-   [Übersicht über gatewaypools](#bkmk_pools)

-   [RAS-Gatewaybereitstellung](#bkmk_deployment)

-   [Integration des RAS-Gateways in den Netzwerk Controller](#bkmk_integration)

## <a name="ras-gateway-overview"></a><a name="bkmk_overview"></a>Übersicht über RAS-Gateways
Wenn Ihre Organisation ein clouddienstanbieter (Cloud Service Provider, CSP) oder ein Unternehmen mit mehreren Mandanten ist, können Sie das RAS-Gateway im mehr Instanzen Modus bereitstellen, um Netzwerk Datenverkehr zu und von virtuellen und physischen Netzwerken, einschließlich des Internets, bereitzustellen.

Sie können das RAS-Gateway im mehr Instanzen Modus als edgegateway bereitstellen, um den Netzwerk Datenverkehr von Mandanten Kunden an virtuelle Mandanten Netzwerke und Ressourcen weiterzuleiten.

Wenn Sie mehrere Instanzen von RAS-Gateway-VMS bereitstellen, die Hochverfügbarkeit und Failover bereitstellen, stellen Sie einen gatewaypool bereit. In Windows Server 2012 R2 haben alle Gateway-VMS einen einzelnen Pool gebildet, wodurch eine logische Trennung der Gatewaybereitstellung ein wenig schwierig wurde.  Das Windows Server 2012 R2-Gateway bot eine 1:1-Redundanz Bereitstellung für die Gateway-VMS. Dies führte zu einer Auslastung der verfügbaren Kapazität für Site-to-Site-VPN-Verbindungen (S2S).

Dieses Problem ist in Windows Server 2016 behoben, das mehrere gatewaypools bereitstellt, die unterschiedliche Typen für die logische Trennung aufweisen können. Der neue Modus der Redundanz von M + N ermöglicht eine effizientere Failoverkonfiguration.

Weitere Informationen zum RAS-Gateway finden Sie unter [RAS-Gateway](../../../../remote/remote-access/ras-gateway/RAS-Gateway.md).

## <a name="gateway-pools-overview"></a><a name="bkmk_pools"></a>Übersicht über gatewaypools
In Windows Server 2016 können Sie Gateways in einem oder mehreren Pools bereitstellen.

Die folgende Abbildung zeigt verschiedene Typen von gatewaypools, die das Datenverkehrs Routing zwischen virtuellen Netzwerken bereitstellen.

![RAS-gatewaypools](../../../media/RAS-Gateway-High-Availability/ras_pools.png)

Jeder Pool verfügt über die folgenden Eigenschaften:

-   Jeder Pool ist M + N redundant. Dies bedeutet, dass die Anzahl der aktiven Gateway-VMS durch eine N-Anzahl von standbygatewayvms gesichert wird. Der Wert von N (Standby-Gateways) ist immer kleiner oder gleich M (aktive Gateways).

-   Ein Pool kann jede der einzelnen Gatewayfunktionen ausführen: Internetschlüsselaustausch Version 2 (IKEv2) S2S, Layer 3 (L3) und generische Routing Kapselung (GRE), oder der Pool kann alle diese Funktionen ausführen.

-   Sie können allen Pools oder einer Teilmenge von Pools eine einzelne öffentliche IP-Adresse zuweisen. Dadurch wird die Anzahl der öffentlichen IP-Adressen, die Sie verwenden müssen, erheblich reduziert, da alle Mandanten über eine einzige IP-Adresse eine Verbindung mit der Cloud herstellen können. Im folgenden Abschnitt zu Hochverfügbarkeit und Lastenausgleich wird beschrieben, wie dies funktioniert.

-   Sie können einen gatewaypool problemlos zentral hoch-oder herunterskalieren, indem Sie Gateway-VMS im Pool hinzufügen oder entfernen. Das Entfernen oder Hinzufügen von Gateways beeinträchtigt nicht die Dienste, die von einem Pool bereitgestellt werden. Sie können auch die gesamten Pools von Gateways hinzufügen und entfernen.

-   Verbindungen eines einzelnen Mandanten können auf mehreren Pools und mehreren Gateways in einem Pool beendet werden. Wenn für einen Mandanten jedoch Verbindungen in einem gatewaypool mit **allen** Typen beendet werden, kann er keine anderen gatewaypools für **alle** Typen oder einzelne Typen abonnieren.

Gatewaypools bieten außerdem die Flexibilität, zusätzliche Szenarios zu aktivieren:

-   Pools mit einem Mandanten: Sie können einen Pool für die Verwendung durch einen Mandanten erstellen.

-   Wenn Sie Clouddienste über Partner Kanäle (Reseller) verkaufen, können Sie für jeden Reseller separate Pools erstellen.

-   Mehrere Pools können die gleiche Gatewayfunktion, aber unterschiedliche Kapazitäten bereitstellen. Beispielsweise können Sie einen gatewaypool erstellen, der sowohl einen hohen Durchsatz als auch einen niedrigen Durchsatz IKEv2 S2S-Verbindungen unterstützt.

## <a name="ras-gateway-deployment-overview"></a><a name="bkmk_deployment"></a>RAS-Gatewaybereitstellung
In der folgenden Abbildung wird eine typische Bereitstellung des clouddienstanbieters (CSP) des RAS-Gateways veranschaulicht.

![RAS-Gatewaybereitstellung](../../../media/RAS-Gateway-High-Availability/ras_csp_deploy.png)

Bei dieser Art der Bereitstellung werden die gatewaypools hinter einer Software Load Balancer (SLB) bereitgestellt, die es dem CSP ermöglicht, eine einzelne öffentliche IP-Adresse für die gesamte Bereitstellung zuzuweisen. Mehrere Gatewayverbindungen eines Mandanten können auf mehreren gatewaypools und auch auf mehreren Gateways innerhalb eines Pools beendet werden. Dies wird über IKEv2 S2S-Verbindungen im obigen Diagramm veranschaulicht, das gleiche gilt jedoch auch für andere Gatewayfunktionen, wie z. b. L3-und GRE-Gateways.

In der Abbildung ist das MT BGP-Gerät ein mehr Instanzen fähiges RAS-Gateway mit BGP. Mehrinstanzfähiges BGP wird für dynamisches Routing verwendet. Das Routing für einen Mandanten ist zentral. ein einzelner Punkt, der als Routen Reflektor (RR) bezeichnet wird, verarbeitet das BGP-Peering für alle Mandanten Websites. Das RR selbst wird über alle Gateways in einem Pool verteilt. Dies führt zu einer Konfiguration, bei der die Verbindungen eines Mandanten (Datenpfad) auf mehreren Gateways enden, aber der RR für den Mandanten (BGP-peeringpunkt-Steuerungs Pfad) befindet sich nur auf einem der Gateways.

Der BGP-Router ist im Diagramm voneinander getrennt, um dieses zentralisierte Routing Konzept darzustellen. Die BGP-Implementierung des Gateways bietet auch Transit Routing, das es der Cloud ermöglicht, als Transitpunkt für das Routing zwischen zwei Mandanten Standorten zu fungieren. Diese BGP-Funktionen gelten für alle Gatewayfunktionen.

## <a name="ras-gateway-integration-with-network-controller"></a><a name="bkmk_integration"></a>Integration des RAS-Gateways in den Netzwerk Controller
RAS-Gateway ist vollständig in den Netzwerk Controller in Windows Server 2016 integriert. Wenn das RAS-Gateway und der Netzwerk Controller bereitgestellt werden, führt der Netzwerk Controller die folgenden Funktionen aus.

-   Bereitstellung der gatewaypools

-   Konfiguration von Mandanten Verbindungen auf jedem Gateway

-   Wechseln von Netzwerk Datenverkehr zu einem Standby-Gateway im Falle eines gatewayfehlers

Die folgenden Abschnitte enthalten ausführliche Informationen zum RAS-Gateway und Netzwerk Controller.

-   [Bereitstellung und Lastenausgleich von Gatewayverbindungen (IKEv2, L3 und GRE)](#bkmk_provisioning)

-   [Hohe Verfügbarkeit für IKEv2 S2S](#bkmk_ike)

-   [Hohe Verfügbarkeit für GRE](#bkmk_gre)

-   [Hohe Verfügbarkeit für L3-Weiterleitungs Gateways](#bkmk_l3)

### <a name="provisioning-and-load-balancing-of-gateway-connections-ikev2-l3-and-gre"></a><a name="bkmk_provisioning"></a>Bereitstellung und Lastenausgleich von Gatewayverbindungen (IKEv2, L3 und GRE)
Wenn ein Mandant eine Gatewayverbindung anfordert, wird die Anforderung an den Netzwerk Controller gesendet. Der Netzwerk Controller ist mit Informationen zu allen gatewaypools konfiguriert, einschließlich der Kapazität der einzelnen Pools und jedes Gateways in jedem Pool. Der Netzwerk Controller wählt den richtigen Pool und das richtige Gateway für die Verbindung aus. Diese Auswahl basiert auf der Bandbreiten Anforderung für die Verbindung. Der Netzwerk Controller verwendet einen "am besten geeigneten" Algorithmus, um Verbindungen effizient in einem Pool auszuwählen. Der BGP-peeringpunkt für die Verbindung wird auch zu diesem Zeitpunkt festgelegt, wenn es sich um die erste Verbindung des Mandanten handelt.

Nachdem der Netzwerk Controller ein RAS-Gateway für die Verbindung ausgewählt hat, stellt der Netzwerk Controller die erforderliche Konfiguration für die Verbindung auf dem Gateway bereit. Wenn es sich bei der Verbindung um eine IKEv2 S2S-Verbindung handelt, stellt der Netzwerk Controller auch eine NAT-Regel (Network Address Translation) für den SLB-Pool bereit. Diese NAT-Regel für den SLB-Pool leitet Verbindungsanforderungen vom Mandanten zum vorgesehenen Gateway. Mandanten unterscheiden sich anhand der Quell-IP-Adresse, die als eindeutig angesehen wird.

> [!NOTE]
> L3-und GRE-Verbindungen umgehen den SLB und stellen eine direkte Verbindung mit dem angegebenen RAS-Gateway her.  Diese Verbindungen erfordern, dass der remoteend Punkt Router (oder ein anderes Gerät von Drittanbietern) ordnungsgemäß für die Verbindung mit dem RAS-Gateway konfiguriert sein muss.

Wenn BGP-Routing für die Verbindung aktiviert ist, wird das BGP-Peering vom RAS-Gateway initiiert, und die Routen werden zwischen lokalen und cloudgateways ausgetauscht. Die Routen, die von BGP (oder statisch konfigurierte Routen, wenn BGP nicht verwendet wird) erlernt werden, werden an den Netzwerk Controller gesendet. Der Netzwerk Controller gibt dann die Routen auf die Hyper-V-Hosts aus, auf denen die Mandanten-VMS installiert sind. An diesem Punkt kann der Mandanten Datenverkehr an den richtigen lokalen Standort weitergeleitet werden. Der Netzwerk Controller erstellt außerdem zugeordnete Hyper-v-netzwerkvirtualisierungsrichtlinien, die gatewaystandorte angeben, und führt Sie auf die Hyper-v-Hosts aus.

### <a name="high-availability-for-ikev2-s2s"></a><a name="bkmk_ike"></a>Hohe Verfügbarkeit für IKEv2 S2S
Ein RAS-Gateway in einem Pool besteht aus sowohl Verbindungen als auch BGP-Peering verschiedener Mandanten. Jeder Pool verfügt über die aktiven Gateways und N-Standby-Gateways.

Der Netzwerk Controller verarbeitet den Ausfall von Gateways auf folgende Weise.

-   Der Netzwerk Controller sendet ständig die Gateways in allen Pools und kann ein Gateway erkennen, bei dem ein Fehler aufgetreten ist oder ein Fehler aufgetreten ist. Der Netzwerk Controller kann die folgenden Typen von RAS-gatewayfehlern erkennen.

    -   VM-Fehler beim RAS-Gateway

    -   Fehler des Hyper-V-Hosts, auf dem das RAS-Gateway ausgeführt wird

    -   RAS-Gateway-Dienst Fehler

    Der Netzwerk Controller speichert die Konfiguration aller bereitgestellten aktiven Gateways. Die Konfiguration besteht aus Verbindungseinstellungen und Routing Einstellungen.

-   Wenn ein Gateway ausfällt, wirkt es sich auf Mandanten Verbindungen auf dem Gateway sowie auf Mandanten Verbindungen aus, die sich auf anderen Gateways befinden, deren RR sich aber auf dem fehlerhaften Gateway befindet. Die Zeitdauer der letzten Verbindungen ist kleiner als die erste. Wenn der Netzwerk Controller ein fehlerhafter Gateway erkennt, werden die folgenden Aufgaben ausgeführt:

    -   Entfernt die Routen der betroffenen Verbindungen von den computehosts.

    -   Entfernt die Richtlinien für die Hyper-V-Netzwerkvirtualisierung auf diesen Hosts.

    -   Wählt ein Standby-Gateway aus, konvertiert es in ein aktives Gateway und konfiguriert das Gateway.

    -   Ändert die NAT-Zuordnungen im SLB-Pool so, dass Verbindungen mit dem neuen Gateway hergestellt werden.

-   Gleichzeitig werden die IKEv2 S2S-Verbindungen und das BGP-Peering wieder hergestellt, wenn die Konfiguration auf dem neuen aktiven Gateway verfügbar ist. Die Verbindungen und das BGP-Peering können entweder durch das cloudgateway oder das lokale Gateway initiiert werden. Die Gateways aktualisieren ihre Routen und senden Sie an den Netzwerk Controller. Nachdem der Netzwerk Controller die von den Gateways ermittelten neuen Routen erlernt hat, sendet der Netzwerk Controller die Routen und die zugeordneten Hyper-v-netzwerkvirtualisierungsrichtlinien an die Hyper-v-Hosts, auf denen sich die VMs der Fehler betroffenen Mandanten befinden. Diese Netzwerk Controller Aktivität ähnelt der Situation einer neuen Verbindungs Einrichtung, nur dass Sie in größerem Umfang auftritt.

### <a name="high-availability-for-gre"></a><a name="bkmk_gre"></a>Hohe Verfügbarkeit für GRE
Der Prozess der RAS-gatewayfailoverantwort durch den Netzwerk Controller (einschließlich der Fehlererkennung) Kopieren der Verbindungs-und Routing Konfiguration auf das standbygateway, Failover von BGP/statischem Routing der betroffenen Verbindungen (einschließlich des Abschlusses und der erneuten Bereitstellung von Routen auf computehosts und BGP-neupeering) und Neukonfiguration von Hyper-V-netzwerkvirtualisierungstechnologien auf computehosts: für GRE-Gateways und-Verbindungen identisch. Die erneute Einrichtung von GRE-Verbindungen erfolgt jedoch anders, und die hoch Verfügbarkeits Lösung für GRE hat einige zusätzliche Anforderungen.

![Hohe Verfügbarkeit für GRE](../../../media/RAS-Gateway-High-Availability/ras_ha.png)

Zum Zeitpunkt der Gatewaybereitstellung wird jedem virtuellen RAS-Gatewaycomputer eine dynamische IP-Adresse (DIP) zugewiesen. Außerdem wird jeder Gateway-VM eine virtuelle IP-Adresse (VIP) für die GRE-Hochverfügbarkeit zugewiesen. VIPs werden nur Gateways in Pools zugewiesen, die GRE-Verbindungen akzeptieren dürfen, nicht zu nicht-GRE-Pools. Die zugewiesenen VIPs werden mithilfe von BGP an die Tor-Switches (Top of Rack) angekündigt, wodurch die VIPs im physischen Netzwerk der Cloud weiter angekündigt werden. Dadurch sind die Gateways über die Remote Router oder Geräte von Drittanbietern erreichbar, wo sich das andere Ende der GRE-Verbindung befindet. Dieses BGP-Peering unterscheidet sich vom BGP-Peering auf Mandanten Ebene für den Austausch von Mandanten Routen.

Zum Zeitpunkt der GRE-Verbindungs Bereitstellung wählt der Netzwerk Controller ein Gateway aus, konfiguriert einen GRE-Endpunkt auf dem ausgewählten Gateway und gibt die VIP-Adresse des zugewiesenen Gateways zurück. Diese VIP-Adresse wird dann als Ziel-GRE-Tunnel Adresse auf dem Remote Router konfiguriert.

Wenn ein Gateway ausfällt, kopiert der Netzwerk Controller die VIP-Adresse des fehlerhaften Gateways und andere Konfigurationsdaten in das Standby-Gateway. Wenn das Standby-Gateway aktiv wird, wird die VIP-Adresse für den Tor-Switch und das physische Netzwerk angekündigt. Remote Router verbinden GRE-Tunnel weiterhin mit derselben VIP, und die Routing Infrastruktur stellt sicher, dass Pakete an das neue aktive Gateway weitergeleitet werden.

### <a name="high-availability-for-l3-forwarding-gateways"></a><a name="bkmk_l3"></a>Hohe Verfügbarkeit für L3-Weiterleitungs Gateways
Ein Hyper-v-netzwerkvirtualisierungs-L3-Weiterleitungs Gateway ist eine Brücke zwischen der physischen Infrastruktur im Rechenzentrum und der virtualisierten Infrastruktur in der Hyper-v-netzwerkvirtualisierungs-Cloud. Bei einem mehrinstanzfähigen L3-Weiterleitungs Gateway verwendet jeder Mandant sein eigenes logisches Netzwerk mit VLAN-Kennung für die Konnektivität mit dem physischen Netzwerk des Mandanten.

Wenn ein neuer Mandant ein neues L3-Gateway erstellt, wählt das Netzwerk Controller Gateway Service Manager einen verfügbaren Gatewaycomputer aus und konfiguriert eine neue Mandanten Schnittstelle mit einer hoch verfügbaren IP-Adresse (ca) für die IP-Adresse des Mandanten Adressraums (über das VLAN-markierte logische Netzwerk). Die IP-Adresse wird als Peer-IP-Adresse auf dem Remote Gateway (physischer Netzwerk) verwendet und ist der nächste Hop, um das Hyper-V-netzwerkvirtualisierungsnetzwerk des Mandanten zu erreichen.

Im Gegensatz zu IPSec-oder GRE-Netzwerkverbindungen lernt der Tor-Switch das VLAN-markierte Netzwerk des Mandanten nicht dynamisch. Das Routing für das mit dem VLAN markierte Netzwerk des Mandanten muss auf dem Tor-Switch und allen zwischen Schaltern und Routern zwischen physischer Infrastruktur und dem Gateway konfiguriert werden, um eine End-to-End-Konnektivität sicherzustellen.  Im folgenden finden Sie ein Beispiel für eine CSP-Virtual Network Konfiguration, wie in der folgenden Abbildung dargestellt.

|Netzwerk|Subnet|VLAN-ID|Standardgateway|
|-----------|----------|-----------|-------------------|
|Logisches Netzwerk von "Network to so L3"|10.127.134.0/24|1001|10.127.134.1|
|Logisches Netzwerk für Woodgrove L3|10.127.134.0/24|1002|10.127.134.1|

Im folgenden finden Sie Beispielkonfigurationen für Mandanten Gateways, wie in der folgenden Abbildung dargestellt.

|Mandantenname|IP-Adresse des L3-Gateways|VLAN-ID|Peer-IP-Adresse|
|---------------|-------------------------|-----------|-------------------|
|Contoso|10.127.134.50|1001|10.127.134.55|
|Brandenburg|10.127.134.60|1002|10.127.134.65|

Im folgenden finden Sie eine Abbildung dieser Konfigurationen in einem CSP-Rechenzentrum.

![Hohe Verfügbarkeit für L3-Weiterleitungs Gateways](../../../media/RAS-Gateway-High-Availability/ras_fwdgw.png)

Die Gatewayfehler, Fehlererkennung und der gatewayfailoverprozess im Kontext eines L3-Weiterleitungs Gateways ähneln den Prozessen für IKEv2-und GRE-RAS-Gateways. Die Unterschiede bestehen in der Art und Weise, wie die externen IP-Adressen behandelt werden.

Wenn der Status des Gatewaycomputers fehlerhaft wird, wählt der Netzwerk Controller eines der Standby-Gateways aus dem Pool aus und stellt die Netzwerkverbindungen und das Routing auf dem Standby-Gateway wieder her. Beim Verschieben der Verbindungen wird die IP-Adresse der hoch verfügbaren Zertifizierungsstellen-IP-Adresse des L3-Weiterleitungs Gateways ebenfalls auf den neuen Gateway-virtuellen Computer verschoben, zusammen mit der BGP-IP-Adresse des Mandanten.

Da die IP-Adresse des L3-Peerings während des Failovers auf den neuen Gateway-VM verschoben wird, kann die physische Remote Infrastruktur erneut eine Verbindung mit dieser IP-Adresse herstellen und dann die Hyper-V-netzwerkvirtualisierungsumgebung erreichen. Beim dynamischen BGP-Routing, da die BGP-IP-Adresse des ZS-Speicherplatzes auf den neuen Gateway-virtuellen Computer verschoben wird, kann der BGP-Remote Router das Peering erneut einrichten und alle Hyper-V-netzwerkvirtualisierungsrouten erneut erlernen.

> [!NOTE]
> Sie müssen die Tor-Switches und alle zwischen Router separat konfigurieren, damit das VLAN-markierte logische Netzwerk für die Mandanten Kommunikation verwendet wird. Außerdem ist das L3-Failover auf die Racks beschränkt, die auf diese Weise konfiguriert werden. Aus diesem Grund muss der L3-gatewaypool sorgfältig konfiguriert werden, und die manuelle Konfiguration muss separat abgeschlossen werden.



