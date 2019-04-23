---
title: 'RAS-Gateway: Hohe Verfügbarkeit'
description: Sie können in diesem Thema verwenden, um hohe Verfügbarkeitskonfigurationen für das RAS-Multitenant Gateway für Software-Defined Networking (SDN) in Windows Server 2016 zu ermitteln.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 34d826c9-65bc-401f-889d-cf84e12f0144
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8ce515ceeb7ab6989ef18055f312983a6518a1a1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847761"
---
# <a name="ras-gateway-high-availability"></a>RAS-Gateway: Hohe Verfügbarkeit

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um mehr über Konfigurationen mit hochverfügbarkeit für das RAS-Multitenant Gateway für Software-Defined Networking (SDN) erfahren.  
  
Dieses Thema enthält die folgenden Abschnitte:  
  
-   [Übersicht über die RAS-Gateway](#bkmk_overview)  
  
-   [Übersicht über die Gateway-Pools](#bkmk_pools)  
  
-   [Übersicht über die Bereitstellung von RAS-Gateway](#bkmk_deployment)  
  
-   [RAS-Gateway-Integration mit dem Netzwerkcontroller](#bkmk_integration)  
  
## <a name="bkmk_overview"></a>Übersicht über die RAS-Gateway  
Wenn Ihre Organisation eine Cloud-Dienstanbieter (CSP) oder in einem Unternehmen mit mehreren Mandanten ist, können Sie die RAS-Gateway im mehrinstanzenfähigen Modus verwenden, geben Sie die Weiterleitung von Netzwerkdatenverkehr zu und von virtuellen und physischen Netzwerken, die auch über das Internet bereitstellen.  
  
Sie können die RAS-Gateway im mehrinstanzenmodus als ein Edge-Gateway zum Weiterleiten von Kunden mandantennetzwerk-Datenverkehr zu virtuellen Netzwerken und Ressourcen von Mandanten bereitstellen.  
  
Wenn Sie mehrere Instanzen von RAS-Gateway-VMs, die hohe Verfügbarkeit und Failover bereitstellen bereitstellen, stellen Sie einen gatewaypool. In Windows Server 2012 R2 gebildet alle das Gateway VMs einen einzelnen Pool, der eine logische Trennung zwischen der gatewaybereitstellung ein wenig schwierig gestellt.  Windows Server 2012 R2-Gateway bot es sich um eine 1:1-Redundanz Bereitstellung für das Gateway-VMs, die mangelhaft die verfügbare Kapazität für Standort-zu-Standort (S2S) VPN-Verbindungen geführt haben.  
  
Dieses Problem ist in Windows Server 2016 behoben, das unterschiedliche Typen für die logische Trennung aufweisen können mehrere Gatewaypools - bereitstellt. Der neue Modus des M + N-Redundanz ermöglicht eine effizientere Failoverkonfiguration.  
  
Übersicht die Übersichtsinformationen zum RAS-Gateway finden Sie unter [RAS-Gateway](../../../../remote/remote-access/ras-gateway/RAS-Gateway.md).  
  
## <a name="bkmk_pools"></a>Übersicht über die Gateway-Pools  
In Windows Server 2016 können Sie die Gateways in einen oder mehrere Pools bereitstellen.  
  
Die folgende Abbildung zeigt verschiedene Arten von gatewaypools, die ermöglichen, routing von Datenverkehr zwischen virtuellen Netzwerken.  
  
![RAS-Gateway-pools](../../../media/RAS-Gateway-High-Availability/ras_pools.png)  
  
Jeder Pool weist die folgenden Eigenschaften an.  
  
-   Jeder Pool ist M + N ist redundant. Dies bedeutet, dass ein bin "Anzahl der aktiven Gateway-VMs werden" n "die Anzahl der standby-Gateway-VMs gesichert. Der Wert von N (standby-Gateways) ist immer kleiner als oder gleich M (aktive Gateways).  
  
-   Die einzelne Gateway-Funktionen führen Sie ein Pool kann – Internet Key Exchange Version 2 (IKEv2) S2S, Layer-3 (L3), und Generic Routing Encapsulation (GRE)- oder des Pools kann all diese Funktionen ausführen.  
  
-   Sie können eine einzelne öffentliche IP-Adresse zuweisen, auf alle Speicherpools oder auf eine Teilmenge von Pools. Die Anzahl der öffentlichen IP-Adressen, die Sie verwenden müssen, dies so deutlich reduziert werden, da es möglich, dass alle Mandanten, die mit der Cloud auf eine einzelne IP-Adresse verbunden ist. Im Abschnitt unten für hohe Verfügbarkeit und Lastenausgleich wird beschrieben, wie dies funktioniert.  
  
-   Sie können ganz einfach einen gatewaypool nach oben oder unten skalieren durch Hinzufügen oder Entfernen der Gateway-VMs im Pool. Entfernen oder Hinzufügen des Gateways ist nicht die Dienste unterbrochen werden, die von einem Pool bereitgestellt werden. Sie können auch hinzufügen und entfernen die gesamte Pools von Gateways.  
  
-   Verbindungen von einem einzelnen Mandanten können auf mehreren Pools und mehrere Gateways in einem Pool beenden. Jedoch verfügt ein Mandant Verbindungen beendet wird, ein **alle** geben gatewaypool, es kann nicht abonniert werden in anderen **alle** Typ oder vom Typ gatewaypools.  
  
Gatewaypools bieten auch die Flexibilität, um zusätzliche Szenarien zu ermöglichen:  
  
-   Pools mit nur einem Mandanten – können Sie einen Pool für die Verwendung durch einen Mandanten erstellen.  
  
-   Wenn Sie Cloud-Diensten über (Reseller) Partnerkanäle verkauft werden sollen, können Sie separate Sätze von Pools für jede Wiederverkäufer erstellen.  
  
-   Mehrere Pools können auf die gleiche Gatewayfunktion, aber verschiedene Kapazitäten bereitstellen. Beispielsweise können Sie einen gatewaypool erstellen, der einen hohen Durchsatz und niedriger Durchsatz IKEv2-S2S-Verbindungen unterstützt.  
  
## <a name="bkmk_deployment"></a>Übersicht über die Bereitstellung von RAS-Gateway  
Die folgende Abbildung zeigt eine typische Bereitstellung von Cloud-Dienstanbieter (CSP) des RAS-Gateways.  
  
![Übersicht über die Bereitstellung von RAS-Gateway](../../../media/RAS-Gateway-High-Availability/ras_csp_deploy.png)  
  
Mit dieser Art der Bereitstellung sind die gatewaypools hinter einer Software Load Balancer (SLB) bereitgestellt, die der CSP eine einzelne öffentliche IP-Adresse für die gesamte Bereitstellung zuweisen können. Mehrere gatewayverbindungen eines Mandanten können auf mehrere gatewaypools - sowie auf mehrere Gateways innerhalb eines Pools beendet werden. Dies ist über IKEv2-S2S-Verbindungen in der obigen Abbildung dargestellt, aber dasselbe gilt für andere Gatewayfunktionen, z. B. L3 und GRE-Gateways.  
  
In der Abbildung ist das MT-BGP-Gerät-RAS-Mehrinstanzenfähiges Gateway mit BGP an. Mehrinstanzenfähige BGP wird für dynamisches routing verwendet. Das routing für einen Mandanten erfolgt zentral: einen einzelnen Punkt, dem Namen der Route-Reflector (RR), verarbeitet das BGP-peering für alle mandantenwebsites. Die RR selbst wird auf alle Gateways in einem Pool verteilt. Dies führt zu einer Konfiguration, in denen die Verbindungen eines Mandanten (Data-Pfad) auf mehrere Gateways zu beenden, aber der Ressourceneintrag für den Mandanten (BGP peering-Punkt - Pfad des Steuerelements) ist auf nur einem der Gateways.  
  
Der BGP-Router ist im Diagramm, um dieses zentrale routing-Konzept dargestellt aufgeteilt. Die Gateway-BGP-Implementierung hinaus-transitrouting, wodurch die Cloud, fungiert als transitpunkt für das routing zwischen den beiden mandantenschlüssel-Standorten. Diese BGP-Funktionen gelten für alle Gatewayfunktionen zur Verfügung.  
  
## <a name="bkmk_integration"></a>RAS-Gateway-Integration mit dem Netzwerkcontroller  
RAS-Gateway ist vollständig mit dem Netzwerkcontroller in Windows Server 2016 integriert. Wenn RAS-Gateway und dem Netzwerkcontroller bereitgestellt werden, führt den Netzwerkcontroller die folgenden Funktionen aus.  
  
-   Bereitstellung der Gateway-Pools  
  
-   Konfiguration der Mandanten-Verbindungen für jedes gateway  
  
-   Wechseln von Netzwerkdatenverkehr mit einem standby-Gateway im Fall eines Fehlers Gateway fließt  
  
Die folgenden Abschnitte enthalten ausführliche Informationen zu RAS-Gateway und dem Netzwerkcontroller.  
  
-   [Bereitstellung und den Lastenausgleich von Gateway-Verbindungen (IKEv2 L3 und GRE)](#bkmk_provisioning)  
  
-   [Hohe Verfügbarkeit für IKEv2 S2S](#bkmk_ike)  
  
-   [Hohe Verfügbarkeit für GRE](#bkmk_gre)  
  
-   [Hohe Verfügbarkeit für L3 Weiterleitung von Gateways](#bkmk_l3)  
  
### <a name="bkmk_provisioning"></a>Bereitstellung und den Lastenausgleich von Gateway-Verbindungen (IKEv2 L3 und GRE)  
Wenn ein Mandant eine Gateway-Verbindung anfordert, wird die Anforderung für den Netzwerkcontroller gesendet. Netzwerkcontroller ist mit Informationen über alle gatewaypools, einschließlich der Kapazität von jedem Pool und alle Gateways in jedem Pool konfiguriert. Netzwerkcontroller wählt das korrekte Pool und das Gateway für die Verbindung. Diese Auswahl wird basierend auf den Bedarf an Netzwerkbandbreite für die Verbindung. Netzwerkcontroller verwendet einen Algorithmus "best fit", Verbindungen effizient in einem Pool auswählen. Der BGP-peering-Punkt für die Verbindung wird auch zu diesem Zeitpunkt festgelegt, ist dies die erste Verbindung des Mandanten.  
  
Nach dem Netzwerkcontroller über eine RAS-Gateway für die Verbindung auswählt, wird dem Netzwerkcontroller die erforderliche Konfiguration für die Verbindung auf dem Gateway bereitgestellt. Wenn die Verbindung ein IKEv2-S2S-Verbindung ist, stellt Netzwerkcontroller auch eine Regel (Network Address Translation, NAT) für den SLB-Pool; Diese NAT-Regel für den Pool der SLB leitet verbindungsanforderungen aus dem Mandanten mit dem angegebenen Gateway. Mandanten unterscheiden sich von der Quell-IP, die erwartet wird, eindeutig sein.  
  
> [!NOTE]  
> L3 und GRE-Verbindungen SLB umgehen und direkt mit dem angegebenen RAS-Gateway herstellen.  Diese Verbindungen erfordern, die dem Remoteendpunkt Router (oder anderen Geräten von Drittanbietern) ordnungsgemäß konfiguriert sein, um eine Verbindung mit dem RAS-Gateway herzustellen.  
  
Wenn BGP-routing für die Verbindung aktiviert ist, und klicken Sie dann RAS-Gateway - BGP-peering wird initiiert, und Routen zwischen lokalen und Cloud ausgetauscht werden Gateways. Die Routen, die vom BGP erlernt werden (oder, die statisch konfigurierte Routen sind, wenn BGP nicht verwendet wird) werden in den Netzwerkcontroller gesendet. Netzwerkcontroller Verbindungsaufbau klicken Sie dann die Routen auf den Hyper-V-Hosts, auf dem die Mandanten-VMs installiert werden. An diesem Punkt kann mandantendatenverkehr an den richtigen lokalen Standort weitergeleitet werden. Netzwerkcontroller auch erstellt zugeordnete Hyper-V-Netzwerkvirtualisierung-Richtlinien, die Gateway-Standorte angeben und diese auf Hyper-V-Hosts Verbindungsaufbau.  
  
### <a name="bkmk_ike"></a>Hohe Verfügbarkeit für IKEv2 S2S  
Ein RAS-Gateway in einem Pool besteht aus Verbindungen und BGP-peerings mit anderen Mandanten. Jeder Pool weist bin ' aktiv-Gateways und "n" standby-Gateways.  
  
Netzwerkcontroller werden den Ausfall eines Gateways auf folgende Weise verarbeitet.  
  
-   Netzwerkcontroller ständig Pings die Gateways in allen Pools und kann einen Gateway zu erkennen, der ausgeführt wird bzw. ein Fehler auftritt. Netzwerkcontroller kann die folgenden Typen von RAS-Gateway-Fehler erkennen.  
  
    -   RAS-Gateway-VM-Fehler  
  
    -   Fehler bei der Hyper-V-Hosts, die auf dem das RAS-Gateway ausgeführt wird  
  
    -   Fehler bei einem RAS-Gateway-Dienst  
  
    Netzwerkcontroller speichert die Konfiguration der alle bereitgestellten aktiv-Gateways. Konfiguration besteht der Verbindungseinstellungen und Einstellungen für das routing aus.  
  
-   Wenn ein Gateway ein Fehler auftritt, wirkt sich auf sie Mandanten-Verbindungen auf dem Gateway als auch Verbindungen von Mandanten, deren RR, die auf das fehlerhafte Gateway befindet sich jedoch, die sich auf anderen Gateways. Die Zeit der letzten Verbindungen ist kleiner als die erste. Wenn Netzwerkcontroller ein Gateway des fehlgeschlagenen erkannt wird, führt er die folgenden Aufgaben aus.  
  
    -   Entfernt die Routen der betroffenen Verbindungen von den Compute-Hosts an.  
  
    -   Die Hyper-V-Netzwerkvirtualisierungs-Richtlinien auf diesen Hosts wird entfernt.  
  
    -   Wählt einen standby-Gateway, konvertiert es in einer aktiv-Gateway und das Gateway konfiguriert.  
  
    -   Ändert die NAT-Zuordnungen für den SLB-Pool, um Verbindungen mit dem neuen Gateway zu verweisen.  
  
-   Gleichzeitig, wie die Konfiguration auf das neue aktive Gateway angezeigt wird, sind die IKEv2-S2S-Verbindungen und BGP-peering wieder hergestellt. Die Verbindungen und BGP-peering können entweder durch das cloudgateway oder das lokale Gateway initiiert werden. Die Gateways aktualisieren ihre Routen ein und senden sie in den Netzwerkcontroller. Nachdem der Netzwerkcontroller die neuen Routen, die von den Gateways ermittelt lernt, sendet Netzwerkcontroller die Routen und der zugeordneten Richtlinien für die Hyper-V-Netzwerkvirtualisierung an Hyper-V-Hosts befinden, in dem die VMs des Mandanten Fehler betroffen. Diese Aktivität Netzwerkcontroller ist ähnlich für Ihr Betriebssystem von einer neuen verbindungseinrichtung, es tritt nur im größeren Maßstab.  
  
### <a name="bkmk_gre"></a>Hohe Verfügbarkeit für GRE  
Der Prozess der RAS-Gateway-Failover-Antwort vom Netzwerkcontroller – einschließlich der fehlererkennung und kopieren die Verbindung sowie die Weiterleitung von Konfiguration zum standby-Gateway Failover BGP/statische routing der betroffenen Verbindungen (einschließlich der Abbuchung und erneut plumbing von Routen für compute-Hosts und BGP-peering neu), und Neukonfiguration von Hyper-V-Netzwerkvirtualisierungs-Richtlinien auf Compute-Hosts – gilt für GRE-Gateways und Verbindungen. Die erneute Herstellung der GRE-Verbindungen erfolgt unterschiedlich, aber aus, und die Lösung für hohe Verfügbarkeit für GRE hat einige zusätzlichen Anforderungen.  
  
![Hohe Verfügbarkeit für GRE](../../../media/RAS-Gateway-High-Availability/ras_ha.png)  
  
Zum Zeitpunkt der Bereitstellung eines Gateways erhält jeder RAS-Gateway-VM eine dynamische IP-Adresse (DIP). Darüber hinaus wird jede Gateway-VM auch für hohe Verfügbarkeit von GRE eine virtuelle IP-Adresse (VIP) zugewiesen. VIPs werden nur für Gateways in Pools, die GRE-Verbindungen akzeptieren kann und nicht an nicht-GRE-Pools zugewiesen. Die virtuellen IP-Adressen zugewiesen werden, die Top-of Rack (TOR)-Switches, die Verwendung von BGP, die dann weitere VIPs in das physische Netzwerk der Cloud kündigt angekündigt. Dadurch wird die Gateways erreichbar aus dem remote-Routern oder Geräten von Drittanbietern, auf dem anderen Ende der GRE-Verbindung gespeichert. Diese BGP-peering ist anders als die auf Mandantenebene BGP-peering für den Austausch von Routen für Mandanten.  
  
Netzwerkcontroller zum Zeitpunkt der Bereitstellung von GRE-Verbindung wählt einen Gateway, einen GRE-Endpunkt auf dem ausgewählten Gateway konfiguriert und die VIP-Adresse des Gateways zugewiesenen zurückgegeben. Diese VIP-Adresse wird dann als Zieladresse GRE-Tunnel auf dem remote-Router konfiguriert werden.  
  
Wenn ein Gateway ein Fehler auftritt, kopiert Netzwerkcontroller die VIP-Adresse, der das fehlerhafte Gateway und andere Konfigurationsdaten zum standby-Gateway. Wenn das standby-Gateway aktiv wird, kündigt die VIP TOR-Switch und näher mit dem physischen Netzwerk. Remote-Routern weiterhin die gleiche VIP GRE-Tunnel herstellen und die Routinginfrastruktur wird sichergestellt, dass Pakete an das neue aktive Gateway weitergeleitet werden.  
  
### <a name="bkmk_l3"></a>Hohe Verfügbarkeit für L3 Weiterleitung von Gateways  
Hyper-V Network Virtualization L3-weiterleitungs-Gateway ist eine Brücke zwischen der physischen Infrastruktur im Rechenzentrum und der virtualisierten Infrastruktur in der Hyper-V-Netzwerkvirtualisierungs-Cloud. Auf eines mehrinstanzenfähigen L3-weiterleitungsgateways können Sie verwendet jeder Mandant ein eigenen markierte logische VLAN-Netzwerk für die Konnektivität mit physischen Netzwerk des Mandanten.  
  
Beim Erstellen ein neues Mandanten ein neues L3-Gateway, Network Controller Remotedesktopgateway-Dienst-Manager wählt ein Gateway-VM verfügbares und konfiguriert eine neue Schnittstelle für den Mandanten mit einer hoch verfügbaren Kundenadressraum (CA) Speicherplatz IP-Adresse (des Mandanten markierten logisches VLAN-Netzwerk ). Die IP-Adresse wird verwendet, die Peer-IP-Adresse auf dem Remotecomputer (physische Netzwerk)-Gateway und den nächsten Hop des Mandanten Hyper-V-Netzwerkvirtualisierung Netzwerk erreicht ist.  
  
Im Gegensatz zu IPsec oder GRE-Verbindungen Lernen der TOR-Switch nicht mit Tags des Mandanten VLAN-Netzwerk dynamisch. Das routing für markierte des Mandanten VLAN-Netzwerk muss auf dem TOR-Switch und allen intermediate-Switches und Router zwischen der physischen Infrastruktur als auch das Gateway, um sicherzustellen, dass End-to-End-Konnektivität konfiguriert werden.  Es folgt eine Beispielkonfiguration für den virtuellen CSP-Netzwerk wie in der Abbildung unten dargestellt.  
  
|Network|Subnetz|VLAN-ID|Standardgateway|  
|-----------|----------|-----------|-------------------|  
|Logisches Contoso L3-Netzwerk|10.127.134.0/24|1001|10.127.134.1|  
|Woodgrove L3 Logical Network|10.127.134.0/24|1002|10.127.134.1|  
  
Folgendes sind Beispielkonfigurationen für Mandanten-Gateway aus, wie in der Abbildung unten dargestellt.  
  
|Mandantenname|L3-Gateway-IP-Adresse|VLAN-ID|Peer-IP-Adresse|  
|---------------|-------------------------|-----------|-------------------|  
|Contoso|10.127.134.50|1001|10.127.134.55|  
|Woodgrove|10.127.134.60|1002|10.127.134.65|  
  
Im folgenden finden in der Abbildung dieser Konfigurationen in einem CSP-Datencenter.  
  
![Hohe Verfügbarkeit für L3 Weiterleitung von Gateways](../../../media/RAS-Gateway-High-Availability/ras_fwdgw.png)  
  
Die Prozesse für IKEv2 und GRE-RAS-Gateways ähnelt die Gateway-Fehler, bei der fehlererkennung und der Failover-Gatewayprozess im Kontext einer L3 weiterleitungs-Gateway. Die Unterschiede werden in der Art, die externe IP-Adressen behandelt werden.  
  
Wenn das Gateway-VM-Status "Fehler" aufweist, Netzwerkcontroller wählt eine die standby-Gateways aus dem Pool, und Sie werden erneut bereitgestellt werden, die Netzwerkverbindungen und routing auf der standby-Gateway. Während hoch bewegt, der Verbindungen, das Gateway L3-Weiterleitung des werden verfügbare Zertifizierungsstelle Speicherplatz IP-Adresse zu den neuen Gateway-VM zusammen mit den kundenadressraum BGP IP-Adresse des Mandanten ebenfalls verschoben.  
  
Da die L3-Peering-IP-Adresse in das neue Gateway-VM während des Failovers verschoben wird, kann die physische Infrastruktur der remote erneut eine Verbindung mit dieser IP-Adresse herstellen und anschließend die Hyper-V-Netzwerkvirtualisierung-Workload zu erreichen. Für das dynamische BGP-routing, wie die Zertifizierungsstelle, die BGP IP-Adresse zum neuen Gateway-VM verschoben wird der remote-BGP-Router erneut hergestellt peering, und erfahren Sie, alle Hyper-V-Netzwerkvirtualisierung Routen erneut ausführen.  
  
> [!NOTE]  
> Sie müssen die TOR-Switches und aller die Zwischenrouter separat konfigurieren, um die markierte logisches VLAN-Netzwerk für die Mandanten-Kommunikation verwenden. Darüber hinaus ist ein L3-Failover beschränkt, nur den Racks, die auf diese Weise konfiguriert werden. Aus diesem Grund der L3-Gateway-Pool muss sorgfältig konfiguriert werden, und die manuelle Konfiguration muss abgeschlossen werden.  
  


