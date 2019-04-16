---
title: Netzwerk für Hyper-V-Netzwerkvirtualisierung – technische Details in WindowsServer 2016
description: Dieses Thema enthält technische Informationen zu Hyper-V-Netzwerkvirtualisierung in Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: virtual-network
ms.suite: na
ms.technology:
- networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9efe0231-94c1-4de7-be8e-becc2af84e69
ms.author: pashort
author: shortpatti
ms.openlocfilehash: af2b2a0b151601124bb473c465e7d5a97f2b9150
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="hyper-v-network-virtualization-technical-details-in-windows-server-2016"></a>Netzwerk für Hyper-V-Netzwerkvirtualisierung – technische Details in WindowsServer 2016

>Gilt für: WindowsServer 2016

Servervirtualisierung kann mehrere Instanzen gleichzeitig auf einem physischen Host ausgeführt. voneinander isoliert werden. Jeder virtuelle Computer arbeitet im Prinzip der einzige Server, auf dem physischen Computer ausgeführt wird.  
  
Netzwerkvirtualisierung bietet eine ähnliche Funktionalität, in der mehrere virtuelle Netzwerke (u. u. mit überlappenden IP-Adressen) auf dem gleichen ausgeführt physischen Netzwerkinfrastruktur und jedes virtuelle Netzwerk arbeitet, als wäre es das einzige virtuelle Netzwerk auf den gemeinsam genutzten Netzwerkinfrastruktur ausgeführt wird. Abbildung 1 wird diese Beziehung gezeigt.  
  
![Servervirtualisierung im Vergleich zur Netzwerkvirtualisierung](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF1.gif)  
  
Abbildung 1: Servervirtualisierung im Vergleich zur Netzwerkvirtualisierung  
  
## <a name="hyper-v-network-virtualization-concepts"></a>Hyper-V-Netzwerkvirtualisierungskonzepten  
In Hyper-V-Netzwerkvirtualisierung (HNV), ist ein Kunde oder Mandanten definiert als der "Besitzer" einer Gruppe von IP-Subnetze, die in einem Unternehmen oder Datencenter bereitgestellt werden. Ein Kunde kann eine Organisation oder ein Unternehmen mehrere Abteilungen oder Geschäftseinheiten in einem privaten Datencenter die Netzwerkisolation erfordern oder eines Mandanten in einem öffentlichen Rechenzentrum, die durch einen Dienstanbieter gehostet wird. Jeder Kunde kann über eine oder mehrere verfügen [virtuelle Netzwerke](#VirtualNetworks) im Datencenter, und jedes virtuelle Netzwerk besteht aus mindestens [virtuelle Subnetze](#VirtualSubnets).  
  
Es gibt zwei Hyper-v-Implementierungen der in Windows Server 2016 verfügbar sein sollen: HNVv1 und HNVv2.  
  
-   **HNVv1**  
  
    HNVv1 ist kompatibel mit Windows Server 2012 R2 und System Center 2012 R2 Virtual Machine Manager (VMM). Konfiguration für HNVv1 basiert auf WMI-Verwaltung und Windows PowerShell-Cmdlets (erleichtert über System Center VMM) zum Definieren von isolationseinstellungen und Kundenadressraum (CA) - virtuelles Netzwerk - Zuordnungen physischen Adresse (AA) und routing. Keine zusätzlichen Features in Windows Server 2016 HNVv1 hinzugefügt wurden und keine neuen Features geplant werden.  
    
    • Festlegen Teaming und Hyper-v-V1 sind nicht kompatibel-Plattform.
    
    O mit hoher Verfügbarkeit NVGRE-Gateways Benutzer verwenden muss entweder LBFO Team oder keine Team verwenden. Oder
    
    O mit Network Controller bereitgestellten Gateways mit zusammengeschlossen wechseln.

  
-   **HNVv2**  
  
    Eine Reihe neuer Features sind in HNVv2 enthalten, die mit der Azure virtuellen Filterung Plattform (VFP) Markuperweiterung im Hyper-V-Switch implementiert wird. HNVv2 ist vollständig mit Microsoft Azure Stack integriert, einschließlich der neuen Netzwerkcontroller im Stapel Software Defined Networking (SDN).  Virtuelles Netzwerk-Richtlinie definiert ist, über das Microsoft [Netzwerkcontroller](../../../sdn/technologies/network-controller/Network-Controller.md) eine RESTful NorthBound (NB) API verwenden und auf einem Host-Agent über mehrere SouthBound Intefaces (SBI) einschließlich OVSDB angewandten. Die Richtlinie für Server-Agent Programme in der VFP-Erweiterung des Hyper-V-Switches, in dem sie erzwungen wird.  
  
    > [!IMPORTANT]  
    > In diesem Thema geht es HNVv2.  
  
### <a name="VirtualNetworks"></a>Virtuelles Netzwerk  
  
-   Jedes virtuelles Netzwerk besteht aus einem oder mehreren virtuellen Subnetzen. Ein virtuelles Netzwerk bildet eine isolationsbegrenzung, in denen können die virtuellen Computer in einem virtuellen Netzwerk nur miteinander kommunizieren. Bisher wurde diese Isolation Verwendung von VLANs mit einem getrennten IP-Adressbereich und 802. 1Q erzwungen Tags oder VLAN-ID. Mit Hyper-v-, Isolation wird jedoch erzwungen mithilfe von NVGRE oder VXLAN Kapselung überlagerungsnetzwerke mit überlappenden IP-Subnetze zwischen Kunden oder Mandanten die Möglichkeit zu erstellen.  
  
-   Jedes virtuelles Netzwerk ist ein eindeutiger Routing Domain ID (RDID) auf dem Host. Diese RDID ordnet ungefähr eine Ressourcen-ID, um das virtuelle Netzwerk REST-Ressourcen im Netzwerkcontroller zu identifizieren. Das virtuelle Netzwerk REST-Ressource enthält einen Verweis auf einen Uniform Resource Identifier (URI)-Namespace mit der hinzugefügten Ressource-ID.  
  
### <a name="VirtualSubnets"></a>Virtuelle Subnetze  
  
-   Ein virtuelles Subnetz implementiert die Layer-3-IP-Subnet-Semantik für die virtuellen Computer im gleichen virtuellen Subnetz. Das virtuelle Subnetz bildet eine Übertragungsdomäne (vergleichbar mit einem VLAN) und Isolation wird mithilfe von NVGRE-Mandanten Netzwerk-ID (TNI) oder VXLAN Netzwerk-ID (VNI7D) Feld erzwungen.  
  
-   Jedes virtuelle Subnetz gehört zu einem einzelnen virtuellen Netzwerk (RDID), und es wird eine eindeutige VSID Virtual Subnet ID () mit den TNI oder VNI7D Schlüssel im gekapselte Paket-Header zugewiesen. Die VSID muss im Datencenter eindeutig sein und liegt im Bereich von 4096 bis 2 ^ 24-2.  
  
Ein wichtiger Vorteil der virtuellen Netzwerk und Routingdomäne besteht, dass Kunden Sie eigene Netzwerktopologien (z. B. IP-Subnetze) umstellen können in der Cloud. Abbildung 2 zeigt ein Beispiel, in dem das Unternehmen Contoso Corp. zwei separate Netzwerke, R & D Net und dem Verkauf Net verfügt. Da diese Netzwerke unterschiedliche Routingdomänen-IDs verfügen, können nicht sie miteinander interagieren. Das heißt, ist Contoso R & D Net vom "Contoso-Vertriebsnetzwerk" isoliert, obwohl beide Subnetze mit Contoso Corp. Contoso R & D Net enthält drei virtuelle Subnetze. Beachten Sie, dass sowohl die RDID als auch VSID innerhalb eines Datencenters eindeutig sind.  
  
![Kundennetzwerke und virtuelle Subnetze](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF6.gif)  
  
Abbildung 2: Kundennetzwerke und virtuelle Subnetze  
  
**Layer 2-Weiterleitung**  
  
In Abbildung 2 können die virtuellen Computer in der VSID 5001 ihre Pakete für virtuelle Maschinen, die auch in der VSID 5001 über den Hyper-V-Switch weitergeleitet. Die eingehenden Pakete von einem virtuellen Computer in der VSID 5001 werden an einem bestimmten VPort auf dem Hyper-V-Switch gesendet. Eingehende Regeln (z. B. Encap) und Zuordnungen (z. B. Kapselung Header) werden durch die Hyper-V-Switch für diese Pakete angewendet. Die Pakete werden dann weitergeleitet entweder zu einem anderen VPort auf Hyper-V-Switch (sofern virtuellen Zielcomputers mit dem gleichen Host verbunden ist) oder mit einem anderen Hyper-V-Switch auf einem anderen Host (wenn die Ziel-virtuelle Maschine auf einem anderen Host befindet).  
  
**Layer-3-Routing**  
  
Ebenso können die virtuellen Computer in der VSID 5001 müssen Sie ihre Pakete mit virtuellen Computern in der VSID 5002 oder 5003 weitergeleitet, vom Hyper-v-verteilten Router der in jedem Hyper-V-Host VSwitch vorhanden ist. Bei der Übergabe des Pakets an den Hyper-V-switch, HNV die VSID des eingehenden Pakets mit der VSID des virtuellen Zielcomputers aktualisiert. Dies geschieht nur, wenn sich beide VSIDs in der gleichen RDID befinden.  Aus diesem Grund können nicht virtuelle Netzwerkadapter mit der rdid 1 keine Pakete an virtuelle Netzwerkadapter mit der rdid 2 senden, ohne ein Gateway zu durchlaufen.  
  
> [!NOTE]  
> In dem Paket oben aufgeführten Beschreibung bedeutet, dass der Begriff "virtueller Computer" tatsächlich den virtuellen Netzwerkadapter auf dem virtuellen Computer. Meistens ist, dass eine virtuelle Maschine nur einen einzigen virtuellen Netzwerkadapter verfügt. In diesem Fall können die Wörter "virtueller Computer" und "Netzwerkadapter" im Prinzip das gleiche gemeint.  
  
Jedes virtuelle Subnetz legt ein Layer 3-IP-Subnetz und eine Schicht 2 (L2) Übertragungsdomäne Grenze ähnlich einem VLAN. Wenn Sie ein virtuellen Computer ein Paket überträgt, verwendet Hyper-v-Unicast-Replikation (UR), erstellen Sie eine Kopie des ursprünglichen Pakets und der IP- und MAC durch die Adressen der einzelnen virtuellen Maschinen in der gleichen VSID.  
  
> [!NOTE]  
> Bei Windows Server 2016 enthalten ist, werden mithilfe von unicastreplikation Broadcasts und Subnetz Multicasts implementiert werden. Multicast-subnetzübergreifende routing und IGMP werden nicht unterstützt.  
  
Abgesehen davon, dass eine Broadcastdomäne, enthält die VSID Isolation. Ein virtuellen Netzwerkadapter in Hyper-v-ist mit einem Hyper-V-Switchport verbunden, die ACL-Regeln angewendet werden, entweder direkt mit dem Port (VirtualNetworkInterface REST Ressource) oder das virtuelle Subnetz (VSID), von dem er gehört.  
  
Der Hyper-V-Switchport benötigen Sie ein ACL-Regeln angewendet. Diese ACL konnte kann können alle, alle verweigern oder spezifische um nur bestimmte Arten von Datenverkehr basierend auf den Abgleich von 5-Tupel (Quell-IP, Ziel-IP, Quellport, Zielport, Protokoll) zuzulassen.  
  
> [!NOTE]  
> Hyper-V-Switcherweiterungen funktioniert nicht mit HNVv2 in die neue Software Defined Networking (SDN)-Stapel. HNVv2 wird implementiert, mit der Azure Virtual Filtering Platform (VFP) Switcherweiterung die in Verbindung mit jedem anderen 3rd Party Switcherweiterung verwendet werden kann.  
  
## <a name="switching-and-routing-in-hyper-v-network-virtualization"></a>Wechseln und das Routing im Hyper-V-Netzwerkvirtualisierung  
HNVv2 implementiert die richtige Ebene 2 (L2) wechseln und Layer 3 (L3) routing Semantik funktioniert genauso wie einen physischen Schalter oder Router funktioniert. Wenn mit eine virtuellen Maschine verbunden versucht ein virtuelles Hyper-v-Netzwerk herstellen eine Verbindung mit einem anderen virtuellen Computer im gleichen virtuellen Subnetz (VSID) sie zunächst die CA-MAC-Adresse des Remotecomputers an virtuellen lernen muss. Wenn ein ARP-Eintrag für das Ziel des virtuellen Computers IP-Adresse in der Datenquelle des virtuellen Computers ARP-Tabelle vorhanden ist, wird die MAC-Adresse aus dieser Eintrag verwendet. Wenn ein Eintrag nicht vorhanden ist, sendet die virtuelle Quellmaschine ein ARP-broadcast, mit einer Anforderung für die MAC-Adresse, IP-Adresse für das Ziel des virtuellen Computers entspricht, die zurückgegeben werden. Hyper-V-Switch wird diese Anforderung abfangen und senden Sie ihn an den Server-Agent. Der Server-Agent sucht in der lokalen Datenbank für die entsprechende MAC-Adresse für die IP-Adresse der angeforderten Ziel des virtuellen Computers.  
  
> [!NOTE]  
> Der Server-Agent als des Servers OVSDB verwendet eine Variante des Schemas VTEP zum Speichern von CA-PA-Zuordnungen, MAC-Tabelle und So weiter.  
  
Wenn eine MAC-Adresse verfügbar ist, wird der Agent-Host fügt eine ARP-Antwort und sendet wieder mit dem virtuellen Computer. Nachdem die VM-Netzwerkstapel alle erforderlichen L2-Headerinformationen verfügt, wird die an den entsprechenden Hyper-V-Port auf dem V-Switch gesendet. Intern, Hyper-V-Switch diesen Frame vor dem V-Anschluss N-Tupel-Zuordnungsregeln testet und bestimmte Transformationen auf den Frame basierend auf diesen Regeln angewendet. Vor allem ist eine Reihe von Kapselung Transformationen angewendet, um die Kapselung Kopfzeile mithilfe von NVGRE oder VXLAN, je nach der Richtlinie definiert den Netzwerk-Controller zu erstellen. Basierend auf der Richtlinie, die vom Host-Agent so programmiert, eine CA-PA-Zuordnung dient zum Ermitteln der IP-Adresse des Hyper-V-Host befindet, in dem die virtuellen Zielcomputer. Hyper-V-Switch wird sichergestellt, die richtigen Verteilerregeln und VLAN-Tags werden auf der äußeren Paket angewendet, sodass es die PA-Remoteadresse erreicht.  
  
Wenn eine virtuelle Maschine mit einem virtuellen Hyper-v-Netzwerk verbunden eine Verbindung mit einem virtuellen Computer in einem anderen virtuellen Subnetz (VSID) zu erstellen möchte, muss das Paket entsprechend weitergeleitet werden. Hyper-v-wird angenommen, eine Stern-Topologie mit nur einer IP-Adresse in den kundenadressraum, die als Nächster Hop verwendet, um alle IP-Adresspräfixe (Bedeutung einer Route/Standardgateway) zu erreichen. Aktuell Dies erzwingt eine Einschränkung für eine einzelne Standardroute und nicht standardmäßige Routen werden nicht unterstützt.  
  
### <a name="routing-between-virtual-subnets"></a>Routing zwischen virtuellen Subnetzen  
In einem physischen Netzwerk ist ein IP-Subnetz eine Schicht 2 (L2)-Domäne, in denen Computer (virtuelle und physische) direkt miteinander kommunizieren können. Die L2-Domäne ist eine Broadcastdomäne, in dem ARP-Einträge (IP:MAC Adresse Map) werden durch ARP-Anfragen, die auf allen Schnittstellen übermittelt werden ausfindig gemacht und ARP-Antworten an den anfordernden Host gesendet werden. Der Computer verwendet die MAC-Informationen über die der ARP-Antwort des L2-Frames einschließlich Ethernet-Header vollständig zu erstellen. Allerdings werden ist eine IP-Adresse in einem anderen L3-Subnetz, in die ARP-Anforderung nicht diese L3-Grenze überschreiten. In diesem Fall muss ein L3-Routerschnittstelle (Nächster Hop oder ein Standardgateway) die IP-Adresse im Subnetz Quelle auf diese ARP-Anfragen mit seiner eigenen MAC-Adresse reagieren.  
  
Im standard-Windows-Netzwerk, ein Administrator erstellen statische Routen und weisen Sie diesen Konstanten eine Netzwerkschnittstelle. Darüber hinaus ist "Standard-Gateway" in der Regel konfiguriert den nächsten Hop IP-Adresse für eine Schnittstelle, in denen Pakete an, für die Standardroute (0.0.0.0/0) gesendet werden. Pakete werden an das Standardgateway gesendet, wenn keine bestimmte Route vorhanden sind. Dies ist normalerweise der Router für das physische Netzwerk.  Hyper-v-verwendet den integrierten Router, der Bestandteil jedes Hosts und verfügt über eine Schnittstelle in jeder VSID einen verteilten Router für die virtuellen Netzwerke zu erstellen.  
  
Da Hyper-v-eine Sterne-Topologie wird davon ausgegangen, fungiert der Hyper-v-verteilte Router als einzelne Standard-Gateway für den gesamten Datenverkehr, die zwischen virtuellen Subnetzen, die Teil der gleichen VSID Netzwerk werden soll. Die Adresse als der Standard-Gateway ist die niedrigste IP-Adresse in die VSID und der Hyper-v-verteilten Router zugewiesen ist. Diese verteilte Router ermöglicht eine sehr effiziente Möglichkeit für den gesamten Datenverkehr in einem Netzwerk VSID entsprechend weitergeleitet werden, da jeder Host direkt den Datenverkehr an den geeigneten Host weiterleiten kann ohne Einbeziehung einer zwischengeschalteten Instanz.  Dies gilt insbesondere, wenn auf dem gleichen physischen Host zwei virtuelle Computer im gleichen VM-Netzwerk, aber verschiedene virtuelle Subnetze vorhanden sind.  Wie Sie weiter unten in diesem Abschnitt sehen werden, dass das Paket nie auf den physischen Host zu lassen.  
  
### <a name="routing-between-pa-subnets"></a>Routing zwischen PA-Subnetzen  
Im Gegensatz zu HNVv1, der eine PA-IP-Adresse für die einzelnen VSID (Virtual Subnet) zugeordnet, verwendet HNVv2 jetzt eine PA-IP-Adresse pro Switch-Embedded Teaming (SET) NIC-Team Member. Die Standard-Bereitstellung wird davon ausgegangen ein zwei-NIC-Team und weist zwei PA-IP-Adressen pro Host. Ein einzelner Host hat PA-IP-Adressen vom gleichen Anbieter (PA) logischen Subnetz auf demselben VLAN zugewiesen. Zwei Mandanten-VMs im gleichen virtuellen Subnetz kann tatsächlich auf zwei unterschiedlichen Hosts befinden, der mit zwei anderen Anbieter logischen Subnetzen verbunden sind. Hyper-v-wird die äußere IP-Header für das gekapselte Paket basierend auf der CA-PA-Zuordnung erstellen. Allerdings werden basiert auf dem Host TCP/IP-Stapel an ARP für das Standardgateway PA und erstellt dann die äußere Ethernet-Header basierend auf der ARP-Antwort. In der Regel enthält diese ARP-Antwort der SVI-Schnittstelle am physischen Switch oder Router L3-, in dem der Host verbunden ist. Hyper-v-stützt sich daher auf den L3-Router für die Weiterleitung der gekapselte Pakete zwischen logischen Subnetzen Anbieter / VLANs.  
  
### <a name="routing-outside-a-virtual-network"></a>Routing außerhalb eines virtuellen Netzwerks  
Bei den meisten kundenbereitstellungen benötigen Kommunikation zwischen dem Hyper-v-Umgebung und Ressourcen, die nicht Teil der Hyper-v-Umgebung sind. Kommunikation zwischen den beiden Umgebungen möglich sind netzwerkvirtualisierungsgateways erforderlich. Anfordern eines Gateways für Hyper-v-Infrastrukturen enthalten Private Cloud und Hybrid-Cloud. Im Grunde genommen sind hnv-Gateways erforderlich Layer 3-routing zwischen internen und externen (physische) Netzwerken (einschließlich NAT) oder zwischen unterschiedlichen Standorten bzw. Clouds (private oder öffentliche), die einen IPSec-VPN oder GRE-Tunnel verwenden.  
  
Gateways sind in verschiedenen Formfaktoren erhältlich. Sie können unter Windows Server 2016, in einer oberen von Rack (TOR) Switch fungiert, VXLAN Gateway über eine virtuelle IP (VIP) von einem Lastenausgleichsmodul angekündigte zugegriffen kann ein neues eigenständiges Netzwerkgerät vorliegen oder anderen vorhandenen Netzwerkgeräten integriert erstellt werden.  
  
Weitere Informationen zu Windows RAS-Gateway-Optionen finden Sie unter [RAS-Gateway](../../../../remote/remote-access/ras-gateway/RAS-Gateway.md).  
  
## <a name="packet-encapsulation"></a>-Paketkapselung  
Jedem virtuellen Netzwerkadapter in Hyper-v-ist zwei IP-Adressen zugeordnet:  
  
-   **Kundenadresse** (CA) die IP-Adresse, die vom Kunden basierend auf der Intranetinfrastruktur zugewiesen. Diese Adresse ermöglicht es den Kunden, Netzwerkdatenverkehr mit dem virtuellen Computer auszutauschen, als ob es nicht in einer öffentlichen oder privaten Cloud verlagert worden wäre. Die Zertifizierungsstelle ist für den virtuellen Computer sichtbar und für den Kunden erreichbar.  
  
-   **Anbieteradresse** (PA) die zugewiesene IP-Adresse vom Hostinganbieter oder die Datacenter-Administratoren, die basierend auf ihren physischen Netzwerkinfrastruktur. Die AA steht in den Netzwerkpaketen im Netzwerk, die ausgetauscht werden, mit dem Server mit Hyper-V, die der virtuelle Computer gehostet wird. Die PA ist sichtbar auf dem physischen Netzwerk, aber nicht auf dem virtuellen Computer.  
  
Mit den CAS Netzwerktopologie des Kunden, die virtualisiert und entkoppelt aus dem tatsächlichen zugrunde liegenden physischen Netzwerktopologie und Adressen entsprechend der Implementierung der PAs. Das folgende Diagramm zeigt die konzeptionelle Beziehung zwischen den CAs des virtuellen Computers und den PAs der Netzwerkinfrastruktur einer Netzwerkvirtualisierung.  
  
![Konzeptionelle Darstellung der Netzwerkvirtualisierung über eine physische Infrastruktur](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF2.gif)  
  
Abbildung 6: Konzeptionelle Darstellung der Netzwerkvirtualisierung über eine physische Infrastruktur  
  
Im Diagramm senden virtuellen Computer der Kunden Datenpakete in den kundenadressraum, die die physische Netzwerkinfrastruktur über ihre eigenen virtuellen Netzwerke oder "Tunnel" durchlaufen. Im obigen Beispiel können die IPSec-Tunnel als "Briefumschläge" um die Contoso und Fabrikam-Datenpakete mit grünen Adressaufklebern (PA-Adressen) vom Quellhost auf der linken Seite an den Zielhost rechts übermittelt werden vorstellen. Der Schlüssel ist wie die Hosts "Lieferadressen" feststellen (PA) entsprechend der Contoso und Fabrikam-Zertifizierungsstelle, wie die Pakete "Umschläge" eingepackt werden und wie die Zielhosts die Pakete entpacken und ordnungsgemäß an den Contoso und Fabrikam virtuellen Zielcomputer übermitteln können.  
  
Diese einfache Analogie verdeutlicht die wichtigsten Aspekte bei der Netzwerkvirtualisierung:  
  
-   Jede KA eines virtuellen Computers wird PA eines physischen Hosts zugeordnet. Es können mehrere CAs derselben PA zugeordnet werden  
  
-   Virtuelle Computer senden Datenpakete in die CA-Räume, die in "Umschläge" mit einem PA-Quelle und Ziel-Paar basierend auf der Zuordnung positioniert werden.  
  
-   Die CA-PA-Zuordnungen müssen die Hosts unterscheiden-Pakete für die virtuellen Computer der verschiedenen Kunden ermöglichen.  
  
Daher ist Mechanismus zum Virtualisieren der im Netzwerks von den virtuellen Computern verwendeten Netzwerkadressen virtualisiert. Netzwerkcontroller ist verantwortlich für die Adresszuordnung und der Server-Agent verwaltet die Datenbank mithilfe des Schemas MS_VTEP. Im nächsten Abschnitt beschrieben die eigentlichen Mechanismus für die adressvirtualisierung.  
  
## <a name="network-virtualization-through-address-virtualization"></a>Netzwerkvirtualisierung durch adressvirtualisierung  
Hyper-v-implementiert überlagern mandantennetzwerke mit Network Virtualization Generic Routing Encapsulation (NVGRE) oder Virtual eXtensible Local Area Network (VXLAN).  VXLAN ist die Standardeinstellung.  
  
### <a name="virtual-extensible-local-area-network-vxlan"></a>Virtual eXtensible Local Area Network (VXLAN)  
Die Virtual eXtensible Local Area Network (VXLAN) ([RFC 7348](http://www.rfc-editor.org/info/rfc7348)) Protokoll wurde umfassend im Markt, mit Unterstützung von Herstellern wie Cisco, Brocade, Arista, Dell, HP und andere übernommen. Das Protokoll VXLAN verwendet UDP als Transport. Die IANA zugeordnet wurde UDP-Zielport für VXLAN 4789 ist und der UDP-Quellport sollte ein Hash der Informationen aus dem inneren Paket für ECMP Zuweisung verwendet werden. Nach der UDP-Header wird eine Kopfzeile VXLAN auf das Paket angehängt enthält ein reserviertes 4-Byte-Feld, gefolgt von einem 3-Byte-Feld für die VXLAN Netzwerk Bezeichner (VNI7D) - VSID - gefolgt von einem anderen reservierten 1-Byte-Feld. Nach dem Header VXLAN wird der ursprüngliche Zertifizierungsstelle L2-Rahmen (ohne die CA-Ethernet-Frame FCS) angefügt.  
  
![VXLAN-Paket-header](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VXLAN-packet-header.png)  
  
### <a name="generic-routing-encapsulation-nvgre"></a>Generic Routing Encapsulation (NVGRE)  
Dieser Mechanismus zur Netzwerkvirtualisierung wird das Generic Routing Encapsulation (NVGRE) als Bestandteil des Tunnel-Headers verwendet. Bei NVGRE wird Paket des virtuellen Computers in einem anderen Paket gekapselt. Der Header dieses neuen Pakets hat die entsprechende Quelle und Ziel-PA-IP-Adressen zusätzlich zu den virtuellen Subnetz-ID, die im Key-Feld des GRE-Headers gespeichert ist, wie in Abbildung 7 dargestellt.  
  
![NVGRE-Kapselung](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF3.gif)  
  
Abbildung 7: Netzwerkvirtualisierung – NVGRE-Kapselung  
  
Das virtuelle Subnetz-ID können Hosts zur Identifizierung des Kunden virtuellen Computers für jedes angegebene Paket, obwohl der AAS und der Zertifizierungsstelle auf die Pakete des möglicherweise überlappen. Dadurch können alle virtuellen Maschinen auf dem gleichen Host eine einzige PA gemeinsam nutzen, wie in Abbildung 7 dargestellt.  
  
Freigabe PA hat großen Einfluss auf Netzwerk-Skalierbarkeit. Die Anzahl der IP- und MAC-Adressen von der Netzwerkinfrastruktur bekannt gegeben sein kann erheblich reduziert werden. Wenn jeder endhost durchschnittlich 30 virtuelle Computer, die Anzahl der IP- und MAC-Adressen, die durch die Netzwerkinfrastruktur erlernt werden müssen, wird reduziert, um den Faktor 30. eingebetteten Virtual Subnet IDs in den Paketen können Sie z. B. einfache Zuordnung der Pakete für die tatsächlichen Kunden.  
  
Die PA-Freigabe-Schema für Windows Server 2012 R2 ist eine AA pro VSID pro Host. Für Windows Server 2016 ist das Schema eine AA pro NIC-Team Member.  
  
Mit Windows Server 2016 und höher unterstützt Hyper-v-NVGRE und VXLAN vollständig ausgegeben. Es ist nicht erforderlich, ein Upgrade oder der Erwerb neuer Netzwerkhardware wie (Netzwerkkarten), Switches oder Router. Dies ist, da diese Pakete auf der Leitung normales IP-Paket im PA-Raum sind, die mit der Infrastruktur heutiger Netzwerke kompatibel ist.  Um optimale Leistung nutzen unterstützt NICs mit den neuesten Treibern, die Aufgabe abladungen unterstützen.  
  
## <a name="multi-tenant-deployment-example"></a>Beispiel für mehrinstanzenfähige Bereitstellung  
Das folgende Diagramm zeigt eine für beispielbereitstellung zweier Kunden befindet sich in einem clouddatencenter mit der CA-PA-Beziehung durch die Netzwerkrichtlinien definiert.  
  
![Beispiel für mehrinstanzenfähige Bereitstellung](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF5.png)  
  
Abbildung 8: Von Multi-Tenant-Bereitstellungsbeispiel  
  
Betrachten Sie das Beispiel in Abbildung 8. Vor dem Verschieben in den Hostinganbieter des freigegebenen IaaS-Dienst:  
  
-   Contoso corp. führte einen SQL-Server (mit dem Namen **SQL**) unter der IP-Adresse 10.1.1.11 und einen Webserver (namens **Web**) unter der IP-Adresse 10.1.1.12, der für Datenbanktransaktionen seinen SQL-Server verwendet.  
  
-   Fabrikam corp. führte einen SQL-Server, auch mit dem Namen **SQL** und zugewiesen sind, die IP-Adresse 10.1.1.11 und einen Webserver, die ebenfalls den Namen **Web** und auch der IP-Adresse 10.1.1.12 verwendet seinen SQL-Server für Datenbanktransaktionen.  
  
Wird davon ausgegangen, dass das hosting-Anbieter der Anbieter (PA) logisches Netzwerk über den Netzwerkcontroller physischen Netzwerktopologie entsprechen zuvor erstellt hat. Netzwerkcontroller weist zwei PA-IP-Adressen aus dem logischen Subnetz IP-Präfix, in dem die Hosts verbunden sind. Netzwerkcontroller gibt auch des entsprechenden VLAN-Tags, um die IP-Adressen zuzuweisen.  
  
Klicken Sie dann unter Verwendung der Netzwerk-Controller, Contoso Corp. und Fabrikam corp. erstellen ihre virtuellen Netzwerk und Subnetze der vom Anbieter (PA) logische Netzwerk gemäß der hosting-Anbieter unterstützt werden. Contoso corp. und Fabrikam corp. verschieben ihre jeweiligen SQL-Server und Webserver in der gleichen Hostinganbieters freigegebenen IaaS-Dienst, zufällig der **SQL** virtuellen Maschinen auf Hyper-V-Host 1 und der **Web** (IIS7) virtuellen Maschinen auf Hyper-V-Host 2. Alle virtuellen Computer behalten die ursprünglichen Intranet-IP-Adressen (CAs).  
  
Beide Unternehmen werden die folgenden ID VSID (Virtual Subnet) vom Netzwerkcontroller zugewiesen werden, wie unten angegeben.  Der Host-Agent auf jedem Hyper-V-Host empfängt die zugewiesenen PA-IP-Adressen von Netzwerkcontroller und erstellt zwei PA-Host-vNICs in einer nicht standardmäßigen netzwerkdepot. Jede dieser Host-vNICs ist eine Netzwerkschnittstelle zugewiesen, wo die PA-IP-Adresse zugewiesen ist, wie unten dargestellt:  
  
-   Contoso corp. virtuellen Maschinen VSID und PAs: **VSID** ist 5001, **SQL-PA** lautet 192.168.1.10, **Web PA** ist 192.168.2.20  
  
-   Fabrikam corp. virtuellen Maschinen VSID und PAs: **VSID** ist 6001, **SQL-PA** lautet 192.168.1.10, **Web PA** ist 192.168.2.20  
  
Netzwerkcontroller Verbindungsaufbau Richtlinie für alle Netzwerke (einschließlich der CA-PA-Zuordnung) zu den SDN-Agent für die die Richtlinie in einem permanenten Speicher (in Tabellen der OVSDB) beibehalten werden.  
  
Wenn die Contoso Corp. Web virtuelle Maschine (10.1.1.12) auf dem Hyper-V-Host 2 eine TCP-Verbindung zu SQL Server unter 10.1.1.11 erstellt, geschieht Folgendes:  
  
-   VM-ARPs für das Ziel-MAC-Adresse 10.1.1.11  
  
-   Die Erweiterung VFP-vSwitch fängt das Paket und sendet sie an den SDN-Host-Agent  
  
-   Der SDN-Agent sucht in den Speicher für die MAC-Adresse 10.1.1.11  
  
-   Wenn Sie ein MAC gefunden wird, fügt der Server-Agent eine ARP-Antwort zurück an den virtuellen Computer  
  
-   Wenn Sie ein MAC nicht gefunden wird, wird keine Antwort gesendet, und der ARP-Eintrag auf dem virtuellen Computer für 10.1.1.11 ist nicht erreichbar markiert.  
  
-   Der virtuelle Computer jetzt erstellt einen TCP-Paket mit der richtigen Zertifizierungsstelle Ethernet und IP-Header und sendet sie an der vSwitch  
  
-   Die VFP Markuperweiterung im vSwitch verarbeitet das Paket über die VFP-Ebenen (siehe unten), die Quelle vSwitch-Port auf dem das Paket empfangen wurde, und erstellt einen neuen fortlaufenden-Eintrag in der VFP einheitliche Flow-Tabelle zugewiesen  
  
-   Die VFP-Engine führt Regel entsprechen oder flusstabelle Lookup für jede Ebene (z. B. virtuelle Netzwerk Layer) basierend auf der IP- und Ethernet-Header.  
  
-   Die Regel in der Ebene des virtuellen Netzwerks verweist auf ein CA-PA-Zuordnung Leerzeichen und Kapselung führt.  
  
-   Die Kapselungstyp (VXLAN oder NVGRE) wird in der VNet Ebene zusammen mit der VSID angegeben.  
  
-   Im Fall von VXLAN Kapselung wird ein äußerer UDP-Header mit der VSID des 5001 in der Kopfzeile VXLAN erstellt.  
    Ein äußerer IP-Header wird mit der Quell- und Zielserver PA-Adresse zugewiesen, die Hyper-V-Host 2 (192.168.2.20) und Hyper-V-Host 1 (192.168.1.10) bzw. basierend auf der SDN-Agent-Richtlinie Store erstellt.  
  
-   Dieses Paket fließt dann in der PA-routing-Ebene in VFP.  
  
-   Die PA-routing-Ebene in der VFP-verweist der netzwerkdepot verwendet für den PA-Raum Datenverkehr und eine VLAN-ID und verwenden die TCP/IP-Stapel des Hosts das AA-Paket zu Hyper-V-Host 1 ordnungsgemäß weitergeleitet.  
  
-   Nach Erhalt des gekapselten Pakets Hyper-V-Host 1 empfängt das Paket in der PA-netzwerkdepot und übermittelt ihn vSwitch.  
  
-   Die VFP verarbeitet das Paket über die VFP-Ebenen und erstellen einen neuen fortlaufenden-Eintrag in der VFP einheitliche Flow-Tabelle.  
  
-   Das VFP-Modul Ingres Regeln in der Ebene des virtuellen Netzwerks entspricht und die äußere gekapselten Pakets Ethernet, IP und VXLAN Header streift.  
  
-   VFP-Modul leitet dann das Paket an den vSwitch-Port mit dem Ziel VM verbunden ist.  
  
Ein ähnlicher Prozess beim Datenverkehr zwischen den **Web** und **SQL** virtuellen Computer der Hyper-v-Einstellungen für Fabrikam Corp. verwendet Virtuelle Computer interagieren mit Hyper-v-Fabrikam corp. und Contoso Corp. daher, als befänden Sie sich auf ihren ursprünglichen Intranets. Sie können niemals miteinander interagieren, obwohl sie die gleichen IP-Adressen verwenden.  
  
Die separaten Adressen (CAs und PAs), die Richtlinieneinstellungen der Hyper-V-Hosts und die Adressübersetzung zwischen der Zertifizierungsstelle und der PA bei ein- und ausgehenden VM-Datenverkehr zu isolieren dieser Gruppen von Servern unter Verwendung der NVGRE-Schlüssel oder die VLXAN VNID. Darüber hinaus entkoppelt die virtualisierungszuordnungen und Transformation von der physischen Netzwerkinfrastruktur die virtuelle Netzwerkarchitektur. Obwohl Contoso **SQL** und **Web** und Fabrikam **SQL** und **Web** in jeweils eigenen KA-IP-Subnetzen (10.1.1/24) befinden, ihre physische Bereitstellung geschieht auf zwei Hosts in unterschiedlichen PA-Subnetze, 192.168.1/24 und 192.168.2/24,. Die Folge ist, dass subnetzübergreifende virtueller Computer und live-Migration mit Hyper-v-möglich werden.  
  
## <a name="hyper-v-network-virtualization-architecture"></a>Architektur der Hyper-V-Netzwerkvirtualisierung  
In Windows Server 2016 wird HNVv2 mithilfe der Azure virtuellen Filterung Plattform (VFP) ist eine Erweiterung des NDIS Filterung in Hyper-V-Switch implementiert. Das zentrale Konzept VFP ist, der eine Übereinstimmung Aktion bereits Fluss mit einer internen API verfügbar gemacht werden, auf den SDN-Host-Agent für die Programmierung von Netzwerkrichtlinie. Der SDN-Agent selbst empfängt Netzwerkrichtlinie von Netzwerkcontroller über Kommunikationskanäle OVSDB und WCF-SouthBound. Ist nicht nur die Richtlinie für virtuelle Netzwerke (z. B. CA-PA-Zuordnung) programmiert VFP jedoch zusätzliche Richtlinie wie Zugriffssteuerungslisten und QoS usw. verwenden.  
  
Die Hierarchie der Objekte für die vSwitch und VFP Markuperweiterung ist Folgendes:  
  
-   vSwitch  
  
    -   Externe NIC-Verwaltung  
  
    -   NIC-Hardware-Abladungen  
  
    -   Globale Weiterleitungsregeln  
  
    -   Port  
  
        -   Ausgehende Ebene für das Haare Anheften von Weiterleitung  
  
        -   Speicherplatz Listen für Zuordnungen und NAT-pools  
  
        -   Einheitliche Flow-Tabelle  
  
        -   VFP-Ebene  
  
            -   Flow-Tabelle  
  
            -   Gruppe  
  
            -   Regel  
  
                -   Regeln können Speicherplätze verweisen.  
  
In der VFP eine Ebene pro Richtlinie vom Typ (z. B. virtuelles Netzwerk) erstellt und ist ein generischer Satz von Regel und des Informationsflusses Tabellen. Sie besitzt keine systeminternen Funktionen, bis bestimmte Regeln auf dieser Ebene zugewiesen werden, um diese Funktionalität zu implementieren. Jede Ebene wird eine Priorität zugewiesen und Ebenen einen Port nach aufsteigender Priorität zugewiesen sind. Regeln werden in erster Linie auf die Richtung und IP-Adressfamilie basierend in Gruppen organisiert. Gruppen sind auch eine Priorität zugewiesen, und eine Regel aus einer Gruppe kann maximal einen bestimmten Ablauf übereinstimmen.  
  
Die Logik für die vSwitch mit VFP-Erweiterung ist wie folgt:  
  
-   /-Ausgang-Verarbeitung (/-Ausgang aus der Sicht des Pakets an einen Port)  
  
-   Weiterleitung  
  
-   Ausgehende Verarbeitung (ausgehende aus der Sicht des Pakets einen Port verlassen)  
  
Die VFP unterstützt interne MAC-Weiterleitung für NVGRE und VXLAN Kapselung Typen sowie äußeren MAC VLAN-basierte weiterleiten.  
  
Die VFP-Erweiterung verfügt über eine langsame und Fast-Path für Paket durchlaufen. Das erste Paket in einem Fluss durchlaufen Sie alle Regelgruppen in jeder Ebene und führen Sie eine Regel muss Suche bei der ein ressourcenintensiver Vorgang ist. Jedoch, sobald ein Fluss in die einheitliche Flow-Tabelle mit einer Liste von Aktionen (basierend auf den Regeln übereinstimmen) registriert ist werden alle nachfolgenden Pakete verarbeitet basierend auf Einträge in der einheitlichen Fluss.  
  
Hnv-Richtlinie wird durch den hostagent programmiert. Jeder Netzwerkadapter des virtuellen Computers wird mit einer IPv4-Adresse konfiguriert. Dies sind die CAs, die von den virtuellen Computern verwendet werden, die miteinander kommunizieren, und sie in die IP-Pakete von den virtuellen Computern ausgeführt werden. Hyper-v-kapselt die CA-Frame in einem PA-Frame basierend auf der Virtualization-Netzwerkrichtlinien, die in der hostagent-Datenbank gespeichert.  
  
![Hyper-v-Architektur](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF7.png)  
  
Abbildung 9: Hyper-v-Architektur  
  
## <a name="summary"></a>Zusammenfassung  
Cloudbasierte Datencenter bieten viele Vorteile, z. B. verbesserte Skalierbarkeit und ressourcenauslastung. Müssen eine Technologie, die im Wesentlichen der mehrinstanzenfähigen Skalierbarkeit in einer dynamischen Umgebung Probleme behandelt, um diese potenziellen Vorteile nutzen zu können. Hyper-v-wurde entwickelt, um diese Probleme behandeln und auch die betriebliche Effizienz von Datencentern verbessern, indem die Entkopplung von der Topologie des virtuellen Netzwerks für den physischen Netzwerktopologie. Basierend auf einem existierenden Standard wird Hyper-v-in heutigen Datencentern ausgeführt wird und mit Ihrer vorhandenen VXLAN-Infrastruktur. Kunden mit Hyper-v-jetzt ihre Rechenzentren in einer privaten Cloud oder ihrer Datencenter in einen Server Hostinganbieters Umgebung mit einer hybridcloud nahtlos zu erweitern.  
  
## <a name="BKMK_LINKS"></a>Siehe auch  
Finden Sie weitere Informationen zu HNVv2 unter den folgenden Links:  
  
|Inhaltstyp|Verweise|  
|----------------|--------------|  
|**Community-Ressourcen**|-   [Architektur von Private Clouds-Blog](http://blogs.technet.com/b/privatecloud)<br />– Stellen Sie Fragen:[cloudnetfb@microsoft.com](mailto:%20cloudnetfb@microsoft.com)|  
|**RFC**|-   [NVGRE Draft RFC](http://www.ietf.org/id/draft-sridharan-virtualization-nvgre-07.txt)<br />-   [VXLAN - RFC 7348](http://www.rfc-editor.org/info/rfc7348)|  
|**Verwandte Technologien**|-Hyper-V-Netzwerkvirtualisierung – technische Details in Windows Server 2012 R2, finden Sie unter [Hyper-V-Netzwerkvirtualisierung – technische Details](https://technet.microsoft.com/library/jj134174.aspx)<br />-   [Netzwerkcontroller](../../../sdn/technologies/network-controller/Network-Controller.md)|  
  


