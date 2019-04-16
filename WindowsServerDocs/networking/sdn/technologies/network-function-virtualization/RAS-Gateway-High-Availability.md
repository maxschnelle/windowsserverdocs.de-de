---
title: 'RAS-Gateway: hohe Verfügbarkeit'
description: In diesem Thema können Sie Informationen zu Konfigurationen für hohe Verfügbarkeit für den RAS-mehrinstanzenfähigen Gateway für Software Defined Networking (SDN) in Windows Server2016.
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
ms.openlocfilehash: 48794ff8312ca00eda25f6d8bdca9929fc47084f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="ras-gateway-high-availability"></a>RAS-Gateway: hohe Verfügbarkeit

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zu Konfigurationen für hohe Verfügbarkeit für den RAS-mehrinstanzenfähigen Gateway für Software Defined Networking (SDN).  
  
Dieses Thema enthält die folgenden Abschnitte.  
  
-   [RAS-Gateway (Übersicht)](#bkmk_overview)  
  
-   [Gateway-Pools (Übersicht)](#bkmk_pools)  
  
-   [Übersicht über die Bereitstellung von RAS-Gateway](#bkmk_deployment)  
  
-   [RAS-Gateway-Integration mit Netzwerkcontroller](#bkmk_integration)  
  
## <a name="bkmk_overview"></a>RAS-Gateway (Übersicht)  
Wenn Ihre Organisation (Cloud Service Provider, CSP) oder ein Unternehmen mit mehreren Mandanten ist, können Sie im mehrinstanzenmodus Nachrichtenrouting Netzwerkdatenverkehr zu und von virtuellen und physischen Netzwerken, einschließlich Internet RAS-Gateway bereitstellen.  
  
Sie können die RAS-Gateway im mehrinstanzenmodus als edgegateway zum Weiterleiten von Netzwerkdatenverkehr zu virtuellen Netzwerken und Ressourcen für den Mandanten bereitstellen.  
  
Wenn Sie mehrere Instanzen von RAS-Gateway-VMs, die hohe Verfügbarkeit und Failover bereitstellen bereitstellen, stellen Sie einen Pool Gateway bereit. In Windows Server2012 R2 gebildet, alle Gateway VMs einen einzigen Pool, der eine logische Trennung der gatewaybereitstellung ein wenig schwierig hergestellt wird.  Windows Server2012 R2-Gateway Angeboten für das Gateway-VMs, unzureichende Nutzung der verfügbaren Kapazität für die Standort-zu-Standort (S2S) VPN-Verbindungen wurde eine 1:1-Redundanz-Bereitstellung.  
  
Dieses Problem wird in Windows Server2016 behoben, die enthält mehrere Gateways Pools - verschiedener Typen, die für die logische Trennung werden kann. Der neue Modus M+N Redundanz ermöglicht eine effizientere Failoverkonfiguration.  
  
Weitere Informationen zu RAS-Gateway, finden Sie unter [RAS-Gateway](../../../../remote/remote-access/ras-gateway/RAS-Gateway.md).  
  
## <a name="bkmk_pools"></a>Gateway-Pools (Übersicht)  
In Windows Server2016 können Sie Gateways in einem oder mehreren Pools bereitstellen.  
  
Die folgende Abbildungzeigt die Typen der Gateway-Adresspools, die Datenverkehr Routing zwischen virtuellen Netzwerken bereitstellen.  
  
![RAS-Gateway-Pools](../../../media/RAS-Gateway-High-Availability/ras_pools.png)  
  
Jeder Pool hat die folgenden Eigenschaften.  
  
-   Jeder Pool ist M+N redundant. Dies bedeutet, dass eine bin "Anzahl der aktiven Gateway-VMs" n "die Anzahl der Standby-Gateway-VMs gesichert werden. Der Wert von N (Standby-Gateways) ist immer kleiner als oder gleich M (aktive Gateways).  
  
-   Die einzelnen Gatewayfunktionen führen Sie ein Pool kann – Internet Key Exchange Version 2 (IKEv2) S2S, Layer 3 (L3), und Generic Routing Encapsulation (GRE)- oder Pool kann alle diese Funktionen ausführen.  
  
-   Sie können eine einzelne, öffentliche IP-Adresse auf alle Pools oder auf eine Teilmenge der Pools zuweisen. Dies so erheblich reduziert die Anzahl der öffentlichen IP-Adressen, die Sie verwenden müssen, ist es möglich, dass alle Mandanten in der Cloud auf eine einzelne IP-Adresse eine Verbindung herstellen. Im Abschnittweiter unten auf hohe Verfügbarkeit und Lastenausgleich wird beschrieben, wie dies funktioniert.  
  
-   Sie können ganz einfach einen Gateway-Pool nach oben oder unten skalieren durch Hinzufügen oder Entfernen der Gateway-VMs im Pool. Zum Entfernen oder Hinzufügen eines Gateways wird nicht die Dienste unterbrochen werden, die von einem Pool bereitgestellt werden. Sie können auch hinzufügen und entfernen ganze Pools von Gateways.  
  
-   Verbindung mit einem einzelnen Mandanten können auf mehrere Pools und mehrere Gateways in einem Pool beenden. Jedoch weist ein Mandanten Verbindungen im ein **alle** geben Gateway-Pool, es kann keine anderen abonnieren **alle** Typ oder einzelne Typ Gateway-Pools.  
  
Gateway-Pools bieten auch die nötige Flexibilität, um zusätzliche Szenarien zu ermöglichen:  
  
-   Single-Mandanten-Pools - können Sie einen Pool für die Verwendung durch einen Mandanten erstellen.  
  
-   Wenn Sie Cloud-Diensten über (Händler) Partnerkanäle verkaufen, können Sie separate Sätze von Pools für jeden Fachhändler erstellen.  
  
-   Mehrere Pools können die gleiche Gatewayfunktion jedoch unterschiedliche Kapazitäten bereitstellen. Beispielsweise können Sie einen Gateway-Pool erstellen, der mit hohem Durchsatz und geringer Durchsatz IKEv2-S2S-Verbindungen unterstützt.  
  
## <a name="bkmk_deployment"></a>Übersicht über die Bereitstellung von RAS-Gateway  
Die folgende Abbildungzeigt eine typische (Cloud Service Provider, CSP) Bereitstellung von RAS-Gateway.  
  
![Übersicht über die Bereitstellung von RAS-Gateway](../../../media/RAS-Gateway-High-Availability/ras_csp_deploy.png)  
  
Mit dieser Art der Bereitstellung werden die Gateway-Pools hinter einer Software Load Balancer (SLB) bereitgestellt, CSP, weisen Sie eine einzelne öffentliche IP-Adresse für die gesamte Bereitstellung ermöglicht. Mehrere-Verbindungen von einem Mandanten können auf mehrere Gateways Pools - und auch auf mehrere Gateways in einem Pool beenden. Dies wird durch die IKEv2-S2S-Verbindungen in der obigen Abbildungveranschaulicht, aber dasselbe gilt für andere Gatewayfunktionen, z.B. L3 und GRE-Gateways.  
  
In der Abbildungist das MT-BGP-Gerät mehrinstanzenfähige RAS-Gateway mit BGP an. Mehrinstanzenfähige BGP wird für dynamisches Routing verwendet. Das Routing für einen Mandanten an einem zentralen - einen einzelnen Punkt, der Route-Reflector (RR) aufgerufen, behandelt das BGP-Peering für alle Mandanten Standorte. Der Eintrag selbst wird auf alle Gateways in einem Pool verteilt. Dies führt zu einer Konfiguration, in denen die Verbindungen von einem Mandanten (Datenpfad) beendet wird, auf mehrere Gateways, sondern der Ressourceneintrag für den Mandanten (BGP Peers Verwaltungspunkt - Pfad des Steuerelements) ist nur in einer der Gateways.  
  
Der BGP-Router ist im Diagramm, dieses zentrale Routing Konzept darzustellen getrennt. Die Gateway-BGP-Implementierung bietet auch transitrouting, wodurch die Cloud, die als Ausgangspunkt während der Übertragung für das Routing zwischen Standorten für zwei Mandanten fungieren. Diese BGP-Funktionen gelten für alle Gatewayfunktionen zur Verfügung.  
  
## <a name="bkmk_integration"></a>RAS-Gateway-Integration mit Netzwerkcontroller  
RAS-Gateway ist vollständig mit Netzwerkcontroller in Windows Server2016 integriert. Wenn RAS-Gateway und dem Netzwerkcontroller bereitgestellt werden, führt Netzwerkcontroller die folgenden Funktionen.  
  
-   Bereitstellung der Gateway-Pools  
  
-   Konfiguration von Mandanten-Verbindungen auf jedes Gateway  
  
-   Wechseln zwischen den Netzwerkverkehr zu einem Standby-Gateway bei einem Ausfall Gateway fließt  
  
Die folgenden Abschnitte enthalten ausführliche Informationen zum RAS-Gateway und dem Netzwerkcontroller.  
  
-   [Bereitstellung und Lastenausgleich der Gateway-Verbindungen (IKEv2, L3 und GRE)](#bkmk_provisioning)  
  
-   [Hohe Verfügbarkeit für IKEv2-S2S](#bkmk_ike)  
  
-   [Hohe Verfügbarkeit für GRE](#bkmk_gre)  
  
-   [Hohe Verfügbarkeit für L3-Weiterleitung Gateways](#bkmk_l3)  
  
### <a name="bkmk_provisioning"></a>Bereitstellung und Lastenausgleich der Gateway-Verbindungen (IKEv2, L3 und GRE)  
Wenn ein Mandant eine Gateway-Verbindung anfordert, wird die Anforderung an Netzwerkcontroller gesendet. Netzwerkcontroller wird mit Informationen zu allen von der Gateway-Pools, einschließlich der Kapazität von jedem Pool und jeden Gateway in jedem Pool konfiguriert. Netzwerkcontroller wählt das richtige Pool und das Gateway für die Verbindung. Diese Auswahl basiert auf den Bedarf an Bandbreite für die Verbindung. Netzwerkcontroller verwendet einen Algorithmus "am besten geeigneten", um Verbindungen effizient in einem Pool wählen. Der BGP-Peers Punkt für die Verbindung wird zu diesem Zeitpunkt auch festgelegt, ist dies die erste Verbindung des Mandanten.  
  
Nachdem Netzwerkcontroller einen RAS-Gateway für die Verbindung ausgewählt hat, stellt Netzwerkcontroller die erforderlichen Konfigurationsschritte für die Verbindung auf dem Gateway bereit. Wenn die Verbindung ein IKEv2-S2S-Verbindung ist, stellt Netzwerkcontroller auch eine Regel (Network Address Translation, NAT) für den Pool SLB; Diese Regel NAT SLB Pools weist Verbindungsanforderungen von Mandanten mit dem dafür vorgesehenen Gateway. Mandanten unterscheiden sich von der Quell-IP, was erwartet wird, eindeutig sein.  
  
> [!NOTE]  
> L3 und GRE-Verbindungen die SLB umgehen und direkt mit der dafür vorgesehenen RAS-Gateway.  Diese Verbindungen erforderlich, dass der Remote-Endpunkt-Router (oder anderen Geräten von Drittanbietern) ordnungsgemäß muss zum Herstellen einer Verbindung mit dem RAS-Gateway konfiguriert werden.  
  
Wenn BGP-Routing, für die Verbindung aktiviert ist dann von RAS-Gateway - BGP-Peering initiiert und Routen zwischen lokalen und Cloud ausgetauscht werden Gateways. Die Routen werden, die von BGP gelernt (oder sind statisch konfigurierten Routen BGP nicht verwendet wird) werden an Netzwerkcontroller gesendet. Netzwerkcontroller Verbindungsaufbau klicken Sie dann die Routen auf dem Hyper-V-Hosts, auf dem die Mandanten-VMs installiert sind. An diesem Punkt kann Mandantendatenverkehr an den richtigen lokalem Standort weitergeleitet werden. Netzwerkcontroller erstellt zugeordnete Hyper-V-Netzwerkvirtualisierung-Richtlinien, die Gateway Speicherorte angeben, und sie bis auf den Hyper-V-Hosts Verbindungsaufbau.  
  
### <a name="bkmk_ike"></a>Hohe Verfügbarkeit für IKEv2-S2S  
Ein RAS-Gateway in einem Pool besteht aus Verbindungen sowohl von anderen Mandanten BGP-Peering. Jeder Pool wurde bin "aktive Gateways und" n "Standby-Gateways.  
  
Netzwerkcontroller übernimmt den Ausfall eines Gateways auf folgende Weise.  
  
-   Netzwerkcontroller ständig Pings Gateways in alle Pools und kann ein Gateway erkennen, die fehlgeschlagen ist oder abgebrochen. Netzwerkcontroller erkennt die folgenden Arten von RAS-Gateway-Fehler.  
  
    -   Fehler bei der RAS-Gateway-VM  
  
    -   Fehler bei der Hyper-V-Hosts auf dem RAS-Gateway ausgeführt wird  
  
    -   Fehler bei einem RAS-Gateway-Dienst  
  
    Netzwerkcontroller speichert die Konfiguration der alle bereitgestellten aktive Gateways. Konfiguration umfasst Verbindungseinstellungen für die und Routing.  
  
-   Wenn ein Gateway ein Fehler auftritt, wirkt sich auf sie Mandanten-Verbindungen auf dem Gateway sowie Mandanten-Verbindungen, die auf anderen Gateways befinden sich jedoch, deren RR auf dem fehlerhaften Gateway. Die Zeit der letzteren Verbindungen ist kleiner als die erste. Beim Netzwerkcontroller einen fehlerhaften Gateway erkennt, die folgenden Aufgaben ausgeführt.  
  
    -   Entfernt die Routen der betroffenen Verbindungen von den Compute-Hosts.  
  
    -   Entfernt die Hyper-V-Netzwerkvirtualisierungs-Richtlinien auf diesen Hosts erlauben.  
  
    -   Wählt ein Standby-Gateway, konvertiert es in einer aktiven Gateway und das Gateway konfiguriert.  
  
    -   Ändert die NAT-Zuordnungen im Pool SLB Verbindungen mit dem neuen Gateway verweisen.  
  
-   Gleichzeitig, wie die Konfiguration auf dem neuen aktiven Gateway wird, sind die IKEv2-S2S-Verbindungen und BGP-Peering neu eingerichtet. Durch die Cloud-Gateway oder das lokale Gateway können die Verbindungen und BGP-Peering initiiert werden. Die Gateways aktualisieren ihre Routen und senden sie an dem Netzwerkcontroller. Nach dem Netzwerkcontroller die neue Routen von Gateways ermittelt lernt, sendet Netzwerkcontroller die Routen und die zugeordneten Richtlinien für die Hyper-V-Netzwerkvirtualisierung an Hyper-V-Hosts befinden, in dem die virtuellen Maschinen, die Mandanten Fehler betroffen. Diese Aktivität Netzwerkcontroller ist ähnlich für Ihr Betriebssystem von einer neuen Verbindung Setup, es tritt nur bei einem skalierbar.  
  
### <a name="bkmk_gre"></a>Hohe Verfügbarkeit für GRE  
Die Failover-Antwort von Netzwerkcontroller - einschließlich Erkennen eines Startfehlers, kopieren Verbindung und Routingkonfiguration in den Standby-Gateway, Failover des BGP oder statischer Routing des betroffenen Verbindungen (einschließlich der Entnahme und erneut auf der Routen Sanitär-berechnen Hosts und BGP-Peering neu) und Neukonfiguration der Hyper-V-Netzwerkvirtualisierungs-Richtlinien auf Compute-Hosts - RAS-Gateway ist gleich für GRE-Gateways und Verbindungen. Die erneute Einrichtung der GRE-Verbindungen erfolgt anders, jedoch, und der Lösung für hohe Verfügbarkeit für GRE verfügt über einige zusätzlichen Anforderungen erfüllen.  
  
![Hohe Verfügbarkeit für GRE](../../../media/RAS-Gateway-High-Availability/ras_ha.png)  
  
Zum Zeitpunkt der Gateway-Bereitstellung erhält jeder RAS-Gateway-VM eine dynamische IP-Adressen (DIP). Alle Gateway-VM ist darüber hinaus auch eine virtuelle IP-Adresse (VIP) für hohe Verfügbarkeit GRE zugewiesen. VIPs werden zugewiesen, nur für Gateways in Pools, die GRE-Verbindungen akzeptieren können, und nicht auf Nicht-GRE-Pools. VIPs zugewiesen werden an den Anfang Rack (TOR)-Switches, die mithilfe von BGP, die dann weitere VIPs mit dem physischen Netzwerk des Cloud kündigt angekündigt. Dadurch wird die Gateways erreichbar vom Remote-Router oder Geräten von Drittanbietern befindet, in dem das andere Ende der GRE-Verbindung. Diese BGP-Peering unterscheidet sich die Mandanten-Level-BGP-Peering für den Austausch von Mandanten Routen.  
  
Netzwerkcontroller zum Zeitpunkt der GRE-verbindungsbereitstellung wählt ein Gateway, einen GRE-Endpunkt auf dem ausgewählten Gateway konfiguriert und wieder VIP-Adresse des zugewiesenen Gateways zurück. Anschließend wird dieser VIP als Ziel GRE-Tunneladresse auf dem Remote-Router konfiguriert.  
  
Beim Ausfall eines Gateways kopiert Netzwerkcontroller VIP-Adresse von der fehlgeschlagenen Gateway und andere Konfigurationsdaten in den Standby-Gateway. Wird der Standby-Gateway aktiv, kündigt die VIP TOR-Switch und Weiter mit dem physischen Netzwerk. Remote-Router weiterhin im selben VIP GRE-Tunnel herstellen, und die Routinginfrastruktur wird sichergestellt, dass Pakete mit dem neuen aktiven Gateway weitergeleitet werden.  
  
### <a name="bkmk_l3"></a>Hohe Verfügbarkeit für L3-Weiterleitung Gateways  
Hyper-V Network Virtualization L3-weiterleitungsgateway ist eine Verbindung zwischen der physischen Infrastruktur im Datencenter und virtualisierten Infrastruktur in der Cloud Hyper-V-Netzwerkvirtualisierung. Auf einem mehrinstanzenfähigen L3-weiterleitungsgateway verwendet jeder Mandant eigene VLAN gekennzeichnete logische Netzwerk für die Konnektivität mit dem physischen Netzwerk des Mandanten.  
  
Beim Erstellen ein neuer Mandanten ein neues L3-Gateway, Network Controller Remotedesktopgateway-Dienst-Manager wählt ein verfügbares Gateway-VM und konfiguriert eine neue Mandanten-Schnittstelle mit einer hoch verfügbaren Kundenadressraum (CA) Speicherplatz IP-Adresse (aus der Mandant VLAN gekennzeichnete logischen Netzwerk). Die IP-Adresse wird als die Peer-IP-Adresse auf dem Remotedesktopgateway (Netzwerk) verwendet und ist der Next-Hop Hyper-V-Netzwerkvirtualisierung-Netzwerk des Mandanten zu erreichen.  
  
Im Gegensatz zu IPsec oder GRE-Verbindungen erfahren die TOR-Switch nicht gekennzeichnete Netzwerk für den Mandanten VLAN dynamisch. Das Routing für den Mandanten VLAN gekennzeichnete Netzwerk muss auf dem TOR-Switch und alle Zwischenzertifizierungsstellen Switches und Router zwischen physischen Infrastruktur und das Gateway, um sicherzustellen, dass End-to-End-Konnektivität konfiguriert werden.  Es folgt eine Beispielkonfiguration für CSP virtuelles Netzwerk wie in der folgenden Abbildungdargestellt.  
  
|Netzwerk|Subnetz|VLAN-ID|Standard-Gateway|  
|-----------|----------|-----------|-------------------|  
|Contoso L3-logisches Netzwerk|10.127.134.0/24|1001|10.127.134.1|  
|Woodgrove L3-logisches Netzwerk|10.127.134.0/24|1002|10.127.134.1|  
  
Folgendes Beispiel Tenant-Gateway-Konfigurationen sind, wie in der folgenden Abbildungdargestellt.  
  
|Mandantenname|L3-Gateway-IP-Adresse|VLAN-ID|Peer-IP-Adresse|  
|---------------|-------------------------|-----------|-------------------|  
|Contoso|10.127.134.50|1001|10.127.134.55|  
|Woodgrove|10.127.134.60|1002|10.127.134.65|  
  
Im folgenden finden in der AbbildungKonfigurationen in einem CSP-Datencenter.  
  
![Hohe Verfügbarkeit für L3-Weiterleitung Gateways](../../../media/RAS-Gateway-High-Availability/ras_fwdgw.png)  
  
Die Gateway-Fehler, Fehler bei der Erkennung und Gateway-Failover-Prozess im Kontext einer L3 forwarding Gateway ist vergleichbar mit den Prozessen für IKEv2 und GRE-RAS-Gateways. Die Unterschiede sind in die Art und Weise, dass Sie die externen IP-Adressen behandelt werden.  
  
Sobald Sie das Gateway-VM-Status fehlerhaft ist, Netzwerkcontroller wählt einen Standby-Gateways aus dem Pool, und Sie werden erneut bereitstellt, die Netzwerkverbindungen und das Routing auf dem Standbymodus Gateway. Während der Verbindungen, die Weiterleitung L3-Gateway hoch wird verfügbare IP-Adresse Zertifizierungsstelle Speicherplatz auch mit dem neuen Gateway-VM zusammen mit den kundenadressraum BGP-IP-Adresse des Mandanten verschoben.  
  
Da die L3-Peering IP-Adresse in das neue Gateway-VM während des Failovers verschoben wird, kann die remote physische Infrastruktur erneut diese IP-Adresse herstellen und anschließend die Hyper-V-Netzwerkvirtualisierung Arbeitslast erreichen. Der Remote-BGP-Router können wieder einrichten Peering und erfahren Sie, alle Hyper-V-Netzwerkvirtualisierung Routen erneut, für BGP dynamisches Routing, als den kundenadressraum, BGP-IP-Adresse in das neue Gateway-VM verschoben wird.  
  
> [!NOTE]  
> Sie müssen die TOR-Switches und alle Zwischenzertifizierungsstellen-Router separat konfigurieren, um das VLAN gekennzeichnete logisches Netzwerk für die Mandanten-Kommunikation verwendet. Darüber hinaus ist L3-Failover beschränkt, um nur den Racks die auf diese Weise konfiguriert werden. Aus diesem Grund L3-Gateway-Pool muss sorgfältig konfiguriert werden und die manuelle Konfiguration separat abgeschlossen werden muss.  
  


