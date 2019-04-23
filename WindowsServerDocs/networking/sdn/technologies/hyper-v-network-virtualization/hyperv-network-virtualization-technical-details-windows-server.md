---
title: Hyper-V-Netzwerkvirtualisierung – technische Details unter WindowsServer 2016
description: Dieses Thema enthält technische Informationen zu Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016
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
ms.openlocfilehash: 8db47479d0c6e6014a7df6cecd59b1e87920b76a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887551"
---
# <a name="hyper-v-network-virtualization-technical-details-in-windows-server-2016"></a>Hyper-V-Netzwerkvirtualisierung – technische Details unter WindowsServer 2016

>Gilt für:  Windows Server 2016

Mittels Servervirtualisierung können auf einem physischen Host mehrere Serverinstanzen parallel und voneinander isoliert ausgeführt werden. Jeder virtuelle Computer arbeitet im Prinzip so, als wäre er der einzige Server, der auf dem Computer ausgeführt wird.  
  
Netzwerkvirtualisierung bietet eine ähnliche Funktionalität, die in der mehrere virtuelle Netzwerke (u. u. mit überlappenden IP-Adressen) ausgeführt werden, auf dem gleichen physischen Netzwerkinfrastruktur und jedes virtuelle Netzwerk ausgeführt wird wie ist dies das einzige virtuelle Netzwerk unter der gemeinsam genutzten Netzwerkinfrastruktur. In Abbildung 1 wird diese Beziehung gezeigt.  
  
![Servervirtualisierung im Vergleich zur Netzwerkvirtualisierung](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF1.gif)  
  
Abbildung 1: Servervirtualisierung im Vergleich zur Netzwerkvirtualisierung  
  
## <a name="hyper-v-network-virtualization-concepts"></a>Erklärung der Begriffe für Hyper-V-Netzwerkvirtualisierung  
In Hyper-V-Netzwerkvirtualisierung (HNV), wird ein Kunde oder Mandant als der "Besitzer" einer Gruppe von IP-Subnetze, die in einer unternehmensumgebung oder Datencenter bereitgestellt werden definiert. Eine Organisation oder ein Unternehmen mit mehreren Abteilungen oder Geschäftseinheiten in einem privaten Rechenzentrum die Netzwerkisolation erfordern oder einen Mandanten in einem öffentlichen Datencenter, die durch einen Dienstanbieter gehostet wird, kann ein Kunde sein. Jeder Kunde kann über eine oder mehrere verfügen [virtuelle Netzwerke](#VirtualNetworks) im Datencenter, und jedes virtuelle Netzwerk besteht aus mindestens [virtuelle Subnetze](#VirtualSubnets).  
  
Es gibt zwei hnv-Implementierungen, die in Windows Server 2016 verfügbar: HNVv1 und HNVv2.  
  
-   **HNVv1**  
  
    HNVv1 ist kompatibel mit Windows Server 2012 R2 und System Center 2012 R2 Virtual Machine Manager (VMM). Konfiguration für HNVv1 basiert auf WMI-Verwaltung und Windows PowerShell-Cmdlets (bereitgestellt durch System Center VMM) zum Definieren von isolationseinstellungen und Kundenadressraum (CA) – virtuelles Netzwerk: physische Adresse (PA) Zuordnungen und routing. HNVv1 in Windows Server 2016 wurden keine zusätzlichen Features hinzugefügt, und es sind keine neuen Features geplant.  
    
    • Legen Sie Teamvorgänge und hnv-V1 sind nicht von der Plattform kompatibel.
    
    ein für Benutzer von hoher Verfügbarkeit NVGRE-Gateways verwenden, muss entweder LBFO-Team oder keine verwenden. Oder
    
    o mit Network Controller bereitgestellten Gateways mit Teaming-fähigen Switch.

  
-   **HNVv2**  
  
    Eine Vielzahl von neuen Features sind in HNVv2 enthalten, die mit der Azure virtuelle Filtern Plattform (VFP) weiterleitungserweiterung in Hyper-V-Switch implementiert wird. HNVv2 ist vollständig mit Microsoft Azure Stack integriert, einschließlich des neuen Netzwerkcontrollers im Stapel Software Defined Networking (SDN).  Virtuelles Netzwerk-Richtlinie wird definiert, über das Microsoft [Netzwerkcontroller](../../../sdn/technologies/network-controller/Network-Controller.md) einen RESTful NorthBound (NB) API verwenden und auf einem Host-Agent über mehrere SouthBound Intefaces (SBI) einschließlich OVSDB angewandten. Der Host-Agent-Richtlinie der Programme in die VFP-Erweiterung, der die Hyper-V-Switch, in denen sie erzwungen wird.  
  
    > [!IMPORTANT]  
    > Dieses Thema konzentriert sich auf HNVv2.  
  
### <a name="VirtualNetworks"></a>Virtuelles Netzwerk  
  
-   Jedes virtuelles Netzwerk besteht aus einem oder mehreren virtuellen Subnetzen. Ein virtuelles Netzwerk bildet eine isolationsbegrenzung, in dem können die virtuellen Computer innerhalb eines virtuellen Netzwerks nur miteinander kommunizieren. In der Vergangenheit wurde diese Isolation mit VLANs eine getrennte IP-Adressbereich und 802. 1Q erzwungen Tag oder VLAN-ID. Und HNV, Isolation wird jedoch erzwungen mit, dass entweder NVGRE oder VXLAN Kapselung um Overlay-Netzwerke mit überlappenden IP-Subnetzen zwischen Kunden oder Mandanten die Möglichkeit zu erstellen.  
  
-   Jedes virtuelles Netzwerk hat eine eindeutige Routing Domain ID (RDID) auf dem Host. Diese RDID ordnet ungefähr eine Ressourcen-ID, um das virtuelle Netzwerk im Netzwerkcontroller-REST-Ressource zu identifizieren. Das virtuelle Netzwerk-REST-Ressource enthält einen Verweis auf einen Uniform Resource Identifier (URI)-Namespace mit dem angefügten Ressourcen-ID  
  
### <a name="VirtualSubnets"></a>Virtuelle Subnetze  
  
-   Ein virtuelles Subnetz implementiert die Layer 3-IP-Subnet-Semantik für die virtuellen Computer, die sich im gleichen virtuellen Subnetz befinden. Das virtuelle Subnetz bildet eine Übertragungsdomäne (vergleichbar mit einem VLAN) und Isolation wird erzwungen, indem Sie die NVGRE-Mandanten Netzwerk-ID (TNI) oder VXLAN Netzwerk-ID (VNI) Feld.  
  
-   Jedes virtuelle Subnetz gehört zu einem einzelnen virtuellen Netzwerk (RDID), und es wird eine eindeutige VSID Virtual Subnet ID () mit der TNI oder VNI Schlüssel im Header gekapselten Pakets zugewiesen. Die VSID muss im Datencenter eindeutig sein und wird im Bereich von 4.096 bis 2 ^ 24-2.  
  
Ein wichtiger Vorteil der das virtuelle Netzwerk und Routingdomäne ist, dass Kunden können ihre eigenen Topologien (z. B. IP-Subnetze) können in der Cloud. In Abbildung 2 wird ein Beispiel gezeigt, in dem das Unternehmen Contoso Corp. über zwei separate Netzwerke verfügt: "F&E-Netzwerk" für Forschung und Entwicklung und "Vertriebsnetzwerk" für den Vertrieb. Da beide Netzwerke unterschiedliche Routingdomänen-IDs besitzen, sind keine Interaktionen zwischen den Netzwerken möglich. Das heißt, das "Contoso-F&E-Netzwerk" ist vom "Contoso-Vertriebsnetzwerk" isoliert, obwohl beide Subnetze im Besitz von Contoso Corp. sind. "Contoso-F&E-Netzwerk" enthält drei virtuelle Subnetze. Beachten Sie, dass sowohl die RDID als auch VSID innerhalb eines Datencenters eindeutig sind.  
  
![Kundennetzwerke und virtuelle Subnetze](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF6.gif)  
  
Abbildung 2: Kundennetzwerke und virtuelle Subnetze  
  
**Layer-2-Weiterleitung**  
  
In Abbildung 2 können die virtuellen Computer in der VSID 5001 ihre Pakete an virtuelle Computer, die auch in der VSID 5001 über den Hyper-V-Switch weitergeleitet haben. Die eingehende Pakete aus einem virtuellen Computer in der VSID 5001 werden an eine bestimmte VPort auf dem Hyper-V-Switch gesendet. Eingangsregeln (z. B. Encap) und Zuordnungen (z. B. Kapselung Header) werden vom Hyper-V-Switch für diese Pakete angewendet. Die Pakete werden dann weitergeleitet entweder auf einem anderen VPort auf Hyper-V-Switch (sofern es sich bei dem virtuellen Zielcomputer an dem gleichen Host angefügt ist) oder mit einem anderen Hyper-V-Switch auf einem anderen Host (wenn die Ziel-VM auf einem anderen Host befindet).  
  
**Layer 3-Routing**  
  
Auf ähnliche Weise haben die virtuellen Computer in der VSID 5001 seine Pakete, die auf virtuellen Computern in der VSID 5002 oder VSID 5003 weitergeleitet werden, indem der hnv-Router verteilten, der in jedem Hyper-V-Host-VSwitch vorhanden ist. Wechseln Sie nach der Übergabe des Pakets an den Hyper-V, aktualisiert HNV die VSID des eingehenden Pakets die VSID des virtuellen Zielcomputers. Dies geschieht nur dann, wenn sich beide VSIDs in der gleichen RDID befinden.  Aus diesem Grund können keine virtuelle Netzwerkadapter mit der rdid 1 keine Pakete an virtuelle Netzwerkadapter mit der rdid 2 senden, ohne einen Gateway durchlaufen.  
  
> [!NOTE]  
> In der Beschreibung des Paketflusses oben bedeutet der Begriff "virtueller Computer" tatsächlich den virtuellen Netzwerkadapter auf dem virtuellen Computer. Ein virtueller Computer verfügt üblicherweise nur über einen einzigen virtuellen Netzwerkadapter. In diesem Fall können die Wörter "virtueller Computer" und "virtuelle Netzwerkadapter" im Prinzip das gleiche gemeint.  
  
Jedes virtuelle Subnetz legt ein Layer-3-IP-Subnetz und eine Layer-2-(L2)-Übertragungsdomänenbegrenzung ähnlich einem VLAN fest. Wenn Sie ein virtuellen Computer ein Paket überträgt, verwendet HNV Unicast-Replikation (UR), erstellen Sie eine Kopie des ursprünglichen Pakets und dem Ziel-IP und dem MAC durch die Adressen der einzelnen virtuellen Computer, die in der gleichen VSID sind.  
  
> [!NOTE]  
> Windows Server 2016 geliefert wird, werden übertragen und das Subnetz Multicasts mit unicastreplikation implementiert werden. Subnetzübergreifende routing per multicast und IGMP werden nicht unterstützt.  
  
Neben ihrer Rolle als Übertragungsdomäne bewirkt die VSID auch die Isolation. Ein virtuellen Netzwerkadapter im hnv-ist mit einem Hyper-V-Switchport verbunden, die ACL-Regeln, die entweder direkt an den Port (VirtualNetworkInterface-REST-Ressourcen) oder das virtuelle Subnetz (VSID), das Mitglied er ist, angewendet hat.  
  
Der Hyper-V-Switchport benötigen eine ACL-Regel angewendet. Diese ACL konnte ermöglichen ALL, DENY ALL oder spezifischere um nur bestimmte Arten von Datenverkehr basierend auf übereinstimmenden 5-Tupel (Quell-IP, Ziel-IP, Quellport, Zielport, Protokoll) zuzulassen.  
  
> [!NOTE]  
> Hyper-V-Switcherweiterungen funktioniert nicht mit HNVv2 im neuen Stapel Software Defined Networking (SDN). HNVv2 wird implementiert, mit der Switcherweiterung von Azure Virtual Filtering Platform (VFP) die in Verbindung mit einer anderen 3rd-Party Switcherweiterung verwendet werden kann.  
  
## <a name="switching-and-routing-in-hyper-v-network-virtualization"></a>Wechseln und Routing in der Hyper-V-Netzwerkvirtualisierung  
HNVv2 implementiert wird, richtig switching-Layer-2 (L2) und Layer-3 (L3)-routing-Semantik funktioniert wie einen physischen Switch oder Router würde funktionieren. Beim Verbinden mit ein virtuellen Computer versucht, ein virtuelles Netzwerk mit hnv-herstellen eine Verbindung mit einem anderen virtuellen Computer im gleichen virtuellen Subnetz (VSID) sie zunächst die CA-MAC-Adresse des virtuellen Computers remote erfahren müssen. Wenn ein ARP-Eintrag für die Ziel-VM-IP-Adresse im ARP-Tabelle, des virtuellen Quellcomputers vorhanden ist, wird die MAC-Adresse aus folgendem Eintrag verwendet. Wenn Sie ein Eintrag nicht vorhanden ist, sendet der virtuellen Quellmaschine, dass ein ARP-broadcast, mit einer Anforderung für die MAC-Adresse für den virtuellen Zielcomputer der IP-Adresse zurückgegeben werden. Hyper-V-Switch wird diese Anforderung abfangen und an den Host-Agent zu senden. Der Host-Agent sucht in der lokalen Datenbank eine entsprechende MAC-Adresse für das angeforderte Ziel-VM-IP-Adresse.  
  
> [!NOTE]  
> Der Host-Agent, wie des Servers OVSDB fungiert verwendet eine Variante des Schemas VTEP zum Speichern von CA-PA-Zuordnungen, MAC-Tabelle und So weiter.  
  
Wenn eine MAC-Adresse verfügbar ist, wird der Host-Agent fügt eine ARP-Antwort, und sendet wieder an den virtuellen Computer. Nach der VM Netzwerkstapel alle erforderlichen L2-Headerinformationen verfügt, wird der Frame an den entsprechenden Hyper-V-Port auf dem V-Switch gesendet. Intern wird die Hyper-V-Switch testet dieses Rahmens für N-Tupel-Abgleichsregeln, die die V-Port zugewiesen und bestimmte Transformationen auf den Frame auf Grundlage dieser Regeln angewendet. Wichtiger ist, wird eine Reihe von Kapselung Transformationen angewendet, um der Kapselung-Header, die mithilfe von NVGRE oder VXLAN, abhängig von der Richtlinie definiert die dem Netzwerkcontroller zu erstellen. Basierend auf der Richtlinie, die durch den Host-Agent so programmiert, wird eine CA-PA-Zuordnung verwendet um zu bestimmen, die IP-Adresse der Hyper-V-Host befindet, in dem auf dem virtuellen Zielcomputer. Hyper-V-Switch wird sichergestellt, die richtige Routingregeln und VLAN-Tags auf das äußere Paket angewendet werden, damit sie die remote-PA-Adresse erreicht.  
  
Wenn eine VM mit einem virtuellen HNV-Netzwerk verbunden, erstellen Sie eine Verbindung mit einem virtuellen Computer in einem anderen virtuellen Subnetz VSID (), muss das Paket entsprechend weitergeleitet werden. HNV geht davon aus einem Stern-Topologie mit nur einer IP-Adresse in den kundenadressraum, die als Nächster Hop verwendet, um alle IP-Adresspräfixe (Bedeutung einer Route/Standardgateway) zu erreichen. Derzeit Dies erzwingt eine Einschränkung für eine einzelne Standardroute und nicht standardmäßige Routen werden nicht unterstützt.  
  
### <a name="routing-between-virtual-subnets"></a>Routing zwischen virtuellen Subnetzen  
In einem physischen Netzwerk ist ein IP-Subnetz eine Layer-2 (L2)-Domäne, in dem (virtuellen oder physischen) Computer direkt miteinander kommunizieren können. Die L2-Domäne ist eine Broadcastdomäne, in dem ARP-Einträge (IP:MAC-Adresszuordnung) werden über ARP-Anfragen, die auf allen Schnittstellen übertragen werden gelernt und ARP-Antworten an den anfordernden Host gesendet werden. Der Computer verwendet die MAC-Informationen aus der Antwort ARP gelernt, einschließlich der Header des Ethernet-Frames L2 vollständig zu erstellen. Jedoch ist eine IP-Adresse in einem anderen L3-Subnetz, wird die ARP-Anforderung nicht diese L3-Grenze nicht überschreiten. Stattdessen muss eine L3-Routerschnittstelle (nächsten Hop oder ein Standard-Gateway) mit einer IP-Adresse im quellsubnetz auf diese ARP-Anfragen mit seiner eigenen MAC-Adresse reagieren.  
  
Ein Administrator kann im standard-Windows-Netzwerke, statische Routen zu erstellen und Zuweisen einer Netzwerkschnittstelle. Darüber hinaus ist "Standardgateway" in der Regel konfiguriert die Next-Hop-IP-Adresse für eine Schnittstelle, in dem Pakete für die Standardroute (0.0.0.0/0) gesendet werden. Pakete werden mit diesem Standardgateway gesendet, wenn keine spezifischen Routen vorhanden sind. Dies ist normalerweise der Router für das physische Netzwerk.  HNV verwendet integrierte Router, der Bestandteil jedes Hosts und verfügt über eine Schnittstelle in jeder VSID um einen verteilten Router für die virtuelle Netzwerke zu erstellen.  
  
Da HNV Sterntopologie davon ausgeht, fungiert der hnv-verteilte Router, als einzelne Standardgateway für den gesamten Datenverkehr, die zwischen virtuellen Subnetzen vor sich geht, die Teil der gleichen VSID-Netzwerks sind. Die Adresse als der Standard-Gateway wird standardmäßig die niedrigste IP-Adresse der VSID verwendet und das hnv-verteilter Router zugewiesen wird. Diese verteilte Router ermöglicht eine sehr effiziente Möglichkeit für den gesamten Datenverkehr in einem Netzwerk VSID entsprechend weitergeleitet werden, da jeder Host direkt Weiterleiten des Datenverkehrs an den richtigen Host kann ohne Einbeziehung einer zwischengeschalteten Instanz.  Dies gilt insbesondere dann, wenn sich zwei virtuelle Computer im gleichen VM-Netzwerk befinden, während auf dem gleichen physischen Host verschiedene virtuelle Subnetze vorhanden sind.  Weiter unten in diesem Abschnitt wird darauf eingegangen, dass das Paket den physischen Host nie verlassen muss.  
  
### <a name="routing-between-pa-subnets"></a>Routing zwischen den PA-Subnetzen  
Im Gegensatz zu HNVv1 eine PA-IP-Adresse für die einzelnen VSID (Virtual Subnet) zugeordnet, verwendet die HNVv2 jetzt eine PA-IP-Adresse pro Teammitglied Switch-Embedded Teaming (SET)-NIC. Die standardmäßige Bereitstellung geht davon aus einem zwei-NIC-Team und weist zwei PA-IP-Adressen pro Host. Ein einzelner Host hat PA-IP-Adressen aus dem gleichen logischen Anbieter (PA)-Subnetz in demselben VLAN zugewiesen. Zwei Mandanten-VMs im gleichen virtuellen Subnetz kann tatsächlich auf zwei unterschiedlichen Hosts befinden die mit zwei anderen Anbieter logische Subnetzen verbunden sind. HNV werden die äußeren IP-Header für das gekapselte Paket basierend auf der CA-PA-Zuordnung erstellen. Allerdings es basiert auf dem Host TCP/IP-Stapel an ARP für das Standardgateway für den PA und erstellt dann anhand der ARP-Antwort den äußeren Ethernet-Headers. In der Regel stammen diese Antwort ARP SVI Schnittstelle am physischen Switch oder L3-Router, in der Host verbunden ist. HNV basiert daher auf der L3-Router für routing der gekapselte Pakete zwischen Anbieter logische Subnetze / VLANs.  
  
### <a name="routing-outside-a-virtual-network"></a>Routing außerhalb eines virtuellen Netzwerks  
Bei den meisten Kundenbereitstellungen wird es erforderlich sein, dass aus der Hyper-V-Netzwerkvirtualisierungsumgebung heraus mit Ressourcen kommuniziert werden kann, die nicht zur Hyper-V-Netzwerkvirtualisierungsumgebung gehören. Damit eine Kommunikation zwischen diesen beiden Umgebungen möglich ist, sind Netzwerkvirtualisierungsgateways erforderlich. Infrastrukturen, erfordern eine hnv-Gateway enthalten die Private Cloud und Hybrid Cloud. Hnv-Gateways müssen sich im Grunde für Schicht 3-routing zwischen internen und externen (physischen) Netzwerken (einschließlich NAT) oder zwischen verschiedenen Standorten bzw. in Clouds (privat oder öffentlich), die einen IPSec-VPN oder GRE-Tunnel verwenden.  
  
Gateways sind in verschiedenen Formfaktoren erhältlich. Sie können erstellt werden, auf Windows Server 2016 integriert, eine Top von Rack (TOR) Switch als fungiert, VXLAN Gateway Zugriff auf die über eine virtuelle IP (VIP) angekündigt werden, indem Sie einen Load Balancer, anderen vorhandenen Netzwerkgeräten integriert, oder ein neues eigenständiges Netzwerkgerät vorliegen .  
  
Weitere Informationen zu Windows RAS-Gateway-Optionen finden Sie unter [RAS-Gateway](../../../../remote/remote-access/ras-gateway/RAS-Gateway.md).  
  
## <a name="packet-encapsulation"></a>Paketkapselung  
Jedem virtuellen Netzwerkadapter werden bei der Hyper-V-Netzwerkvirtualisierung zwei IP-Adressen zugeordnet:  
  
-   **Kundenadresse** (CA) die IP-Adresse, die vom Kunden basierend auf der Intranetinfrastruktur zugewiesen. Diese Adresse kann der Kunde zum Austauschen von Netzwerkdatenverkehr mit dem virtuellen Computer, als wäre es nicht in einer öffentlichen oder privaten Cloud verlagert worden wäre. Die Kundenadresse (CA) ist für den virtuellen Computer sichtbar und für den Kunden zugänglich.  
  
-   **Anbieteradresse** (PA) die IP-Adresse zugewiesen, die vom Hostinganbieter oder den datencenteradministratoren, die basierend auf deren physischer Netzwerkinfrastruktur. Die PA steht in den Netzwerkpaketen, die mit dem Hyper-V-Server ausgetauscht werden, der als Host für den virtuellen Computer dient. Die PA ist im physischen Netzwerk, jedoch nicht für den virtuellen Computer sichtbar.  
  
Mit den CAs wird die Netzwerktopologie des Kunden abgebildet, die virtualisiert und von der eigentlichen, darunter befindlichen physischen Netzwerktopologie mit ihren Adressen gemäß der Implementierung der PAs (Anbieteradressen) entkoppelt wird. In der folgenden Abbildung wird gezeigt, welche konzeptionelle Beziehung zwischen den CAs des virtuellen Computers und den PAs der Netzwerkinfrastruktur bei einer Netzwerkvirtualisierung besteht.  
  
![Konzeptionelle Darstellung der Netzwerkvirtualisierung über eine physische Infrastruktur](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF2.gif)  
  
Abbildung 6: Konzeptionelle Darstellung der Netzwerkvirtualisierung über eine physische Infrastruktur  
  
In der Abbildung senden virtuelle Computer Datenpakete in den kundenadressraum, die durchlaufen die physischen Netzwerkinfrastruktur über ihre eigenen virtuellen Netzwerke oder "Tunnel". Im obigen Beispiel können die Tunnel als "Briefumschläge" um die Contoso- und Fabrikam-Datenpakete mit grünen Adressaufklebern (PA-Adressen), die vom Quellhost auf der linken Seite an den Zielhost rechts übermittelt werden betrachtet werden. Der Schlüssel ist, wie ermittelt die Hosts, die "Lieferadressen" (PAS) entspricht der Contoso und der Fabrikam-Zertifizierungsstelle, wie die Pakete "Umschläge" eingepackt werden und wie die Zielhosts die Pakete wieder Auspacken können und an den Contoso und Fabrikam übermitteln Ziel der virtuellen Computer ordnungsgemäß.  
  
Diese einfache Analogie verdeutlicht die wichtigsten Aspekte bei der Netzwerkvirtualisierung:  
  
-   Jede CA eines virtuellen Computers ist einer PA eines physischen Hosts zugeordnet. Einer PA können mehrere CAs zugeordnet sein.  
  
-   Virtuelle Computer senden Datenpakete in die CA-Räume, die in einer "Umschlag" mit einem PA-Quelle und Ziel-Paar basierend auf der Zuordnung abgelegt werden.  
  
-   Anhand der CA-PA-Zuordnungen müssen die Hosts unterscheiden können, welche Pakete für welchen virtuellen Kundencomputer bestimmt sind.  
  
Die Virtualisierung des Netzwerks wird also dadurch realisiert, indem die von den virtuellen Computern verwendeten Netzwerkadressen virtualisiert werden. Der Netzwerkcontroller ist verantwortlich für die Adresszuordnung, und der hostagent verwaltet die Datenbank mit dem Schema MS_VTEP. Der zur Adressvirtualisierung eingesetzte Mechanismus wird im nächsten Abschnitt beschrieben.  
  
## <a name="network-virtualization-through-address-virtualization"></a>Netzwerkvirtualisierung durch Adressvirtualisierung  
Hnv-implementiert überlagern mandantennetzwerke mit Network Virtualization Generic Routing Encapsulation (NVGRE) oder die Virtual eXtensible Local Area Network (VXLAN).  VXLAN ist die Standardeinstellung.  
  
### <a name="virtual-extensible-local-area-network-vxlan"></a>(Virtual eXtensible Local Area Network, VXLAN)  
Die Virtual eXtensible Local Area Network VXLAN () ([RFC 7348](https://www.rfc-editor.org/info/rfc7348)) Protokoll auf dem Markt, mit Unterstützung von Herstellern wie Cisco, Brocade, Arista, Dell, HP und andere häufig übernommen wurde. Das VXLAN-Protokoll verwendet UDP als Transport. Der IANA zugeordnet UDP-Zielport für VXLAN ist 4789 und der UDP-Quellport sollte ein Hash der Informationen aus dem inneren Paket für ECMP Zuweisung verwendet werden soll. Nach der UDP-Header wird ein VXLAN-Header auf das Paket angefügt, gefolgt von einem 3-Byte-Feld für die VXLAN Netzwerk Bezeichner (VNI) - VSID - gefolgt von einem anderen reserviert 1-Byte-Feld ein reserviertes 4-Byte-Feld enthält. Nach dem Header VXLAN wird der ursprüngliche Zertifizierungsstelle L2-Frame (ohne die CA-Ethernet-Frame FCS) angefügt.  
  
![VXLAN-Paket-header](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VXLAN-packet-header.png)  
  
### <a name="generic-routing-encapsulation-nvgre"></a>Generic Routing Encapsulation (NVGRE)  
Dieser Mechanismus zur Netzwerkvirtualisierung verwendet das Generic Routing Encapsulation (NVGRE) als Bestandteil des Tunnel-Headers. Der VM Paket wird bei der NVGRE in einem anderen Paket gekapselt. Der Header dieses neuen Pakets enthält neben der virtuellen Subnetz-ID (Virtual Subnet ID) – die im Key-Feld des GRE-Headers gespeichert ist (siehe Abbildung 7) – auch die entsprechenden PA-IP-Quell- und -Zieladressen.  
  
![NVGRE-Kapselung](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF3.gif)  
  
Abbildung 7: Netzwerkvirtualisierung – NVGRE-Kapselung  
  
Die virtuelle Subnetz-ID können Hosts den Kunden virtuelle Computer für jedes angegebene Paket zu identifizieren, obwohl der PAS und die Zertifizierungsstelle auf die Pakete des überlappen sich möglicherweise. Daher kann auch für alle virtuellen Computer auf dem gleichen Host eine einzige PA gemeinsam genutzt werden (siehe Abbildung 7).  
  
Diese gemeinsame Nutzung spielt bei der Netzwerkskalierbarkeit eine große Rolle. So kann die Anzahl der IP- und MAC-Adressen, die der Netzwerkinfrastruktur bekannt sein müssen, beträchtlich reduziert werden. Wenn zum Beispiel jeder Endhost durchschnittlich 30 virtuelle Computer beherbergt, wird die Anzahl der IP- und Mac-Adressen in diesem Fall um den Faktor 30 gesenkt. Außerdem ermöglichen die in den Paketen eingebetteten Virtual Subnet IDs eine einfache Zuordnung der Pakete zu den Kunden.  
  
Die PA-Freigabe-Schema für Windows Server 2012 R2 ist eine AA pro VSID pro Host. Für Windows Server 2016 ist das Schema eine AA pro NIC-Teammitglied.  
  
Mit Windows Server 2016 und höher unterstützt HNV NVGRE-gekapselten und VXLAN vollständig standardmäßig; Es ist nicht erforderlich, ein Upgrade oder der Erwerb neuer Netzwerkhardware wie (Netzwerkkarten), Switches oder Router. Dies ist, da diese Pakete bei der Übertragung normales IP-Paket im PA-Raum sind die mit der Infrastruktur heutiger Netzwerke kompatibel ist.  Jedoch unterstützt, um die beste Leistung nutzen NICs mit den neuesten Treiber, die die Aufgabe abladungen zu unterstützen.  
  
## <a name="multi-tenant-deployment-example"></a>Beispiel für mehrinstanzenfähige Bereitstellung  
Das folgende Diagramm zeigt eine beispielbereitstellung des zwei Kunden in einem clouddatencenter mit der CA-PA-Beziehung, die durch die Netzwerkrichtlinien definiert.  
  
![Beispiel für mehrinstanzenfähige Bereitstellung](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF5.png)  
  
Abbildung 8: Beispiel für mehrinstanzenfähige Bereitstellung  
  
Betrachten Sie das Beispiel in Abbildung 8. Vor dem Verschieben in den freigegebenen IaaS-Dienst des Hostinganbieters:  
  
-   Contoso Corp. führte unter der IP-Adresse 10.1.1.11 einen SQL-Server (mit dem Namen **SQL**) und unter der IP-Adresse 10.1.1.12 einen Webserver (mit dem Namen **Web**) aus, für dessen Datenbanktransaktionen der zugehörige SQL-Server verwendet wurde.  
  
-   Auch Fabrikam Corp. führte einen SQL-Server (**SQL**) unter der zugewiesenen IP-Adresse 10.1.1.11 und einen Webserver (**Web**) unter der IP-Adresse 10.1.1.12 aus, für dessen Datenbanktransaktionen der zugehörige SQL-Server verwendet wurde.  
  
Wird davon ausgegangen, dass das logische Netzwerk der Anbieter-(PA) über den Netzwerkcontroller zur Anpassung an ihre physische Netzwerktopologie zuvor in der hosting-Anbieter erstellt hat. Der Netzwerkcontroller weist zwei PA-IP-Adressen aus dem logischen Subnetz-IP-Adresspräfix, auf den Hosts verbunden sind. Die Netzwerkcontroller gibt auch an die entsprechenden VLAN-Tags, um die IP-Adressen zu übernehmen.  
  
Erstellen Sie mithilfe der Netzwerk-Controller, Contoso Corp. und Fabrikam corp. Klicken Sie dann ihre virtuelle Netzwerke und Subnetze, die von der Anbieter-(PA) logische Netzwerk gemäß der hosting-Anbieter unterstützt werden. Contoso Corp. und Fabrikam Corp. verschieben ihre jeweiligen SQL-Server und Webserver in den freigegebenen IaaS-Dienst des gleichen Hostinganbieters. Dort wird zufällig der virtuelle Computer **SQL** auf dem Hyper-V Host 1 und der virtuelle Computer **Web** (IIS7) auf dem Hyper-V-Host 2 ausgeführt. Alle virtuellen Computer behalten die ursprünglichen Intranet-IP-Adressen (CAs) bei.  
  
Beider Unternehmen werden die folgenden VSID Virtual Subnet ID () durch den Netzwerkcontroller zugewiesen werden, wie unten angegeben.  Der Host-Agent auf jedem Hyper-V-Host empfängt die zugeordneten PA-IP-Adressen aus dem Netzwerkcontroller und erstellt zwei PA-Host-vNICs in einer nicht standardmäßigen netzwerkdepot. Eine Netzwerkschnittstelle ist jede dieser Host-vNICs zugewiesen, wo die PA-IP-Adresse zugewiesen ist, wie unten dargestellt:  
  
-   Contoso corp. virtuelle Computer VSID und PAs: **VSID** ist 5001, **SQL PA** lautet 192.168.1.10, und **Web PA** ist 192.168.2.20  
  
-   Fabrikam corp. virtuelle Computer VSID und PAs: **VSID** ist 6001, **SQL PA** lautet 192.168.1.10, und **Web PA** ist 192.168.2.20  
  
Der Netzwerkcontroller Verbindungsaufbau alle Netzwerkrichtlinie (einschließlich der CA-PA-Zuordnung) auf den SDN-Host-Agent die die Richtlinie in einem permanenten Speicher (in OVSDB Datenbanktabellen) beibehalten werden.  
  
Wenn Contoso Corp. %%amp;quot;Web%%amp;quot;) virtuelle Maschine (10.1.1.12) auf Hyper-V-Host 2 eine TCP-Verbindung mit SQL Server unter 10.1.1.11 richtet erstellt, geschieht Folgendes:  
  
-   VM-ARPs für das Ziel-MAC-Adresse 10.1.1.11  
  
-   Die VFP-Erweiterung in die vSwitch dieses Paket abfängt und sendet sie an den SDN-Host-Agent  
  
-   Der SDN-Host-Agent sucht in seinem Richtlinienspeicher für die MAC-Adresse 10.1.1.11  
  
-   Wenn Sie ein MAC gefunden wird, fügt der Host-Agent eine ARP-Antwort zurück an den virtuellen Computer  
  
-   Wenn Sie ein MAC nicht gefunden wird, wird keine Antwort gesendet, und die ARP-Eintrag auf dem virtuellen Computer für 10.1.1.11 ist nicht erreichbar markiert.  
  
-   Der virtuelle Computer ist jetzt erstellt ein TCP-Paket mit der richtigen Zertifizierungsstelle Ethernet und IP-Header und sendet sie an der vSwitch  
  
-   Die VFP-Erweiterung in die vSwitch Weiterleitung verarbeitet dieses Paket durch die VFP Ebenen (siehe unten), Quelle vSwitch-Port auf dem das Paket empfangen wurde, und erstellt einen neuen Flow-Eintrag in der Tabelle der VFP-einheitliche Flow zugewiesen  
  
-   Die VFP-Engine führt die Suche nach Regeln entsprechendes oder Flow-Tabelle für jede Ebene (z. B. virtuelles Netzwerk-Layer), basierend auf den IP- und Ethernet-Überschriften.  
  
-   Die übereinstimmende Regel in der Ebene des virtuellen Netzwerks verweist auf ein Leerzeichen der CA-PA-Zuordnung und Kapselung führt.  
  
-   Die Kapselungstyp (VXLAN oder NVGRE) wird in der VNet-Ebene zusammen mit der VSID angegeben.  
  
-   Im Fall von VXLAN Kapselungsschichten kommt wird ein äußerer UDP-Header mit der VSID 5001 im VXLAN Header erstellt.  
    Ein äußerer IP-Header wird erstellt, mit der Quelle und Ziel PA-Adresse, die Hyper-V-Host 2 (192.168.2.20) und Hyper-V Host 1 (192.168.1.10) basieren auf der SDN-Hostagent-Richtlinienspeicher zugewiesen.  
  
-   Dieses Paket fließt dann in der PA-routing-Ebene in VFP.  
  
-   Die PA-routing-Ebene im VFP verweist die netzwerkdepot zum PA-Raum Datenverkehr und eine VLAN-ID und den TCP/IP-Stapel mit dem Host verwenden, die PA-Paket auf Hyper-V Host 1 ordnungsgemäß weitergeleitet.  
  
-   Bei Erhalt des gekapselten Pakets Hyper-V Host 1 empfängt das Paket im PA-Netzwerk-Depots und an die vSwitch weiterleiten.  
  
-   Die VFP verarbeitet das Paket über die VFP-Ebenen, und erstellen einen neuen Flow-Eintrag in die VFP-einheitliche Flow-Tabelle.  
  
-   Die VFP-Engine entspricht die Ingres Regeln in der Ebene des virtuellen Netzwerks und das äußere gekapselten Paket Ethernet, IP- und VXLAN Header entfernt.  
  
-   Die VFP-Engine klicken Sie dann Datenpaket das auf den vSwitch-Port, den die Ziel-VM verbunden ist.  
  
Bei einem ähnlichen Prozess für den Datenverkehr zwischen den virtuellen Computern **Web** und **SQL** von Fabrikam Corp. werden die Hyper-V-Netzwerkvirtualisierungseinstellungen für Fabrikam Corp. verwendet. Mit der Hyper-V-Netzwerkvirtualisierung interagieren die virtuellen Computer von Fabrikam Corp. und Contoso Corp. daher so, als befänden sie sich in ihren ursprünglichen Intranets. Mit den virtuellen Computern des jeweils anderen Unternehmens findet keine Interaktion statt, auch wenn für diese die gleichen IP-Adressen verwendet werden.  
  
Die separaten Adressen (CAs und PAs), die die Richtlinieneinstellungen der Hyper-V-Hosts und die Adressübersetzung zwischen der Zertifizierungsstelle und der PA bei ein- und ausgehenden VM-Datenverkehr isolieren diese Gruppen von Servern, die mit der NVGRE-Schlüssel oder den VLXAN VNID aus. Außerdem wird die virtuelle Netzwerkarchitektur durch die Virtualisierungszuordnungen und -umwandlungen von der physischen Netzwerkarchitektur entkoppelt. Obwohl sich Contoso **SQL** und **Web** sowie Fabrikam **SQL** und **Web** in jeweils eigenen CA-IP-Subnetzen befinden (10.1.1/24), werden sie physisch auf zwei Hosts in unterschiedlichen PA-Subnetzen bereitgestellt: 192.168.1/24 bzw. 192.168.2/24. Dies bringt mit sich, dass durch Hyper-V-Netzwerkvirtualisierung subnetzübergreifende Bereitstellungen virtueller Computer und Livemigrationen möglich werden.  
  
## <a name="hyper-v-network-virtualization-architecture"></a>Architektur der Hyper-V-Netzwerkvirtualisierung  
In Windows Server 2016 wird die HNVv2 mithilfe der Azure virtuelle Filtern Plattform (VFP) ist eine Filterung NDIS-Erweiterung innerhalb des Hyper-V-Switches implementiert. Das Kernkonzept der VFP ist, die von einer Match-Action-Datenfluss-Engine mit einer internen API, die für den SDN-Host-Agent für die Netzwerkrichtlinie Programmierung verfügbar gemacht. Der SDN-Host-Agent selbst empfängt Netzwerkrichtlinie aus dem Netzwerkcontroller über die OVSDB und WCF-SouthBound-Kommunikationskanäle. Ist nicht nur die Richtlinie des virtuellen Netzwerks (z. B. KA-AA-Zuordnung) programmiert VFP jedoch zusätzliche Richtlinien wie z. B. ACLs, QoS und So weiter.  
  
Die Objekthierarchie für die vSwitch und VFP weiterleitungserweiterung lautet wie folgt:  
  
-   vSwitch  
  
    -   Externe NIC-Verwaltung  
  
    -   NIC-Hardwareoffloads  
  
    -   Globale Regeln für Weiterleitung  
  
    -   Port  
  
        -   Ausgehende Daten, die Ebene für das Fixieren von Haar Weiterleitung  
  
        -   Listen von Speicherplatz für Zuordnungen und NAT-pools  
  
        -   Einheitliche Flow-Tabelle  
  
        -   VFP Layer  
  
            -   Flow-Tabelle  
  
            -   Gruppieren  
  
            -   Regel  
  
                -   Regeln können Leerzeichen verweisen.  
  
In den VFP eine Ebene wird pro Richtlinie (z. B. Virtual Network) erstellt und einen allgemeinen Satz von Regelfluss/Tabellen ist. Es muss keine systeminternen Funktionen, bis bestimmte Regeln für die entsprechende Ebene zugewiesen werden, um diese Funktionalität zu implementieren. Jede Ebene wird eine Priorität zugewiesen, und Ebenen werden an einen Port durch aufsteigender Priorität zugewiesen. Regeln werden in erster Linie auf die Richtung und IP-Adressfamilie basierend in Gruppen organisiert. Gruppen werden auch eine Priorität zugewiesen, und eine Regel aus einer Gruppe kann höchstens einen vorhandener Flow übereinstimmen.  
  
Die Logik für die vSwitch mit VFP-Erweiterung lautet wie folgt aus:  
  
-   Eingehende Verarbeitung (Eingang aus Sicht des Pakets an einen Port)  
  
-   Weiterleitung  
  
-   Ausgehende Verarbeitung (ausgehend aus Sicht des Pakets verlassen eines Ports)  
  
Die VFP unterstützt interne MAC-Weiterleitung für die NVGRE-gekapselten und VXLAN Kapselung Typen sowie die äußere VLAN-basierten Macintosh-Weiterleitung an.  
  
Die VFP-Erweiterung verfügt über eine langsame und schnelle-Pfad für das Durchlaufen des Pakets. Das erste Paket in einem Flow durchlaufen alle Regelgruppen in jeder Schicht muss, und führen Sie eine Regel Suche bei der ein aufwändiger Vorgang ist. Jedoch nach der Registrierung eines Flows in der Tabelle einheitliche Flow mit einer Liste von Aktionen (basierend auf den Regeln abgeglichen) werden alle nachfolgenden Pakete verarbeitet basierend auf Einträge in der einheitlichen Flow.  
  
Hnv-Richtlinie wird vom hostagent programmiert. Jeder Netzwerkadapter des virtuellen Computers wird mit einer IPv4-Adresse konfiguriert. Das sind die CAs, mit deren Hilfe die virtuellen Computer miteinander kommunizieren, und sie sind in den aus den virtuellen Computern abgehenden Paketen enthalten. HNV kapselt den CA-Frame in einem PA-Frame, die basierend auf den netzwerkvirtualisierungsrichtlinien in den Host-Agent-Datenbank gespeichert.  
  
![HNV-Architektur](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF7.png)  
  
Abbildung 9: HNV-Architektur  
  
## <a name="summary"></a>Zusammenfassung  
Cloudbasierte Datencenter bieten viele Vorteile, wie zum Beispiel eine bessere Skalierbarkeit und Ressourcenauslastung. Um diese potenziellen Vorteile praktisch nutzen zu können, ist eine Technologie erforderlich, die sich um die Problematik der mehrinstanzenfähigen Skalierbarkeit in einer dynamischen Umgebung kümmert. Hyper-V-Netzwerkvirtualisierung wurde für diese Problematik entworfen. Außerdem wird die Effizienz von Datencentern erhöht, indem die virtuelle von der physischen Netzwerktopologie entkoppelt wird. Basierend auf einem existierenden Standard wird HNV heute in Datencentern ausgeführt wird und mit Ihrer vorhandenen VXLAN-Infrastruktur ausgeführt wird. Kunden und HNV können jetzt ihre Datencenter in einer privaten Cloud zusammenlegen oder nahtlos auf einem Server Hostinganbieters-Umgebung mit einer hybridcloud ausweiten.  
  
## <a name="BKMK_LINKS"></a>Siehe auch  
Finden Sie weitere Informationen zu HNVv2 die folgenden Links:  
  
|Inhaltstyp|Verweise|  
|----------------|--------------|  
|**Community-Ressourcen**|-   [Architektur von Private Clouds-Blog](https://blogs.technet.com/b/privatecloud)<br />-Stellen Sie Fragen: [cloudnetfb@microsoft.com](mailto:%20cloudnetfb@microsoft.com)|  
|**RFC**|-   [NVGRE Draft RFC](https://www.ietf.org/id/draft-sridharan-virtualization-nvgre-07.txt)<br />-   [VXLAN - RFC 7348](https://www.rfc-editor.org/info/rfc7348)|  
|**Verwandte Technologien**|-Hyper-V-Netzwerkvirtualisierung – technische Details unter Windows Server 2012 R2, finden Sie unter [Hyper-V-Netzwerkvirtualisierung – technische Details](https://technet.microsoft.com/library/jj134174.aspx)<br />-   [Netzwerkcontroller](../../../sdn/technologies/network-controller/Network-Controller.md)|  
  


