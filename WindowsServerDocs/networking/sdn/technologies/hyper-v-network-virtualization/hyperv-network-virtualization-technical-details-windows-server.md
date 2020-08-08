---
title: Technische Informationen zur Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016
description: Dieses Thema enthält technische Informationen zur Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016.
manager: grcusanz
ms.topic: article
ms.assetid: 9efe0231-94c1-4de7-be8e-becc2af84e69
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: 5341dfe03a85e192ce18baec44f5213a52a43fd7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952507"
---
# <a name="hyper-v-network-virtualization-technical-details-in-windows-server-2016"></a>Technische Informationen zur Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016

>Gilt für: Windows Server 2016

Mittels Servervirtualisierung können auf einem physischen Host mehrere Serverinstanzen parallel und voneinander isoliert ausgeführt werden. Jeder virtuelle Computer arbeitet im Prinzip so, als wäre er der einzige Server, der auf dem Computer ausgeführt wird.

Die Netzwerkvirtualisierung bietet eine ähnliche Funktion, bei der mehrere virtuelle Netzwerke (potenziell mit überlappenden IP-Adressen) in derselben physischen Netzwerkinfrastruktur ausgeführt werden und jedes virtuelle Netzwerk so funktioniert, als wäre es das einzige virtuelle Netzwerk, das in der gemeinsam genutzten Netzwerkinfrastruktur ausgeführt wird. In Abbildung 1 wird diese Beziehung gezeigt.

![Servervirtualisierung im Vergleich zur Netzwerkvirtualisierung](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF1.gif)

Abbildung 1: Vergleich von Servervirtualisierung und Netzwerkvirtualisierung

## <a name="hyper-v-network-virtualization-concepts"></a>Erklärung der Begriffe für Hyper-V-Netzwerkvirtualisierung
In Hyper-v-Netzwerkvirtualisierung (HNV) wird ein Kunde oder Mandant als "Besitzer" eines Satzes von IP-Subnetzen definiert, die in einem Unternehmen oder einem Rechenzentrum bereitgestellt werden. Ein Kunde kann ein Unternehmen oder ein Unternehmen mit mehreren Abteilungen oder Geschäftseinheiten in einem privaten Daten Center sein, die eine Netzwerk Isolation erfordern, oder ein Mandant in einem öffentlichen Rechenzentrum, das von einem Dienstanbieter gehostet wird. Jeder Kunde kann über ein oder mehrere [virtuelle Netzwerke](#VirtualNetworks) im Daten Center verfügen, und jedes virtuelle Netzwerk besteht aus einem oder mehreren [virtuellen Subnetzen](#VirtualSubnets).

Es gibt zwei HNV-Implementierungen, die in Windows Server 2016 verfügbar sein werden: HNVv1 und HNVv2.

-   **HNVv1**

    HNVv1 ist kompatibel mit Windows Server 2012 R2 und System Center 2012 R2 Virtual Machine Manager (VMM). Die Konfiguration für HNVv1 basiert auf der WMI-Verwaltung und den Windows PowerShell-Cmdlets (durch System Center VMM ermöglicht), um Isolations Einstellungen und Kundenadressen (ca), PA-Zuordnungen und Routing zu definieren. In Windows Server 2016 wurden keine zusätzlichen Features zu HNVv1 hinzugefügt, und es sind keine neuen Features geplant.

    *   Set Teaming und HNV v1 sind nicht nach Plattform kompatibel.

    o zur Verwendung von ha nvgre-Gateways müssen Benutzer entweder das LBFO-Team oder kein Team verwenden. oder

    o verwenden Sie vom Netzwerk Controller bereitgestellte Gateways mit Set-kombinierter Switch.


-   **HNVv2**

    In HNVv2 ist eine große Anzahl neuer Features enthalten, die mithilfe der Azure Virtual Filtering Platform (VFP)-Weiterleitungs Erweiterung im Hyper-V-Switch implementiert wird. HNVv2 ist vollständig in Microsoft Azure Stack integriert, einschließlich des neuen Netzwerk Controllers im SDN-Stapel (Software Defined Networking).  Die Richtlinie für virtuelle Netzwerke wird über den Microsoft- [Netzwerk Controller](../../../sdn/technologies/network-controller/Network-Controller.md) über eine Rest-Northbound-API (NB Northbound, NB) definiert und auf einen Host-Agent über mehrere Southbound-Gesichter (SBI), einschließlich ovsdb, abgestürzt. Die Richtlinie "Host-Agent-Programme" in der VFP-Erweiterung des Hyper-V-Switches, in der Sie erzwungen wird.

    > [!IMPORTANT]
    > Dieses Thema konzentriert sich auf HNVv2.

### <a name="virtual-network"></a><a name="VirtualNetworks"></a>Virtual Network

-   Jedes virtuelle Netzwerk besteht aus einem oder mehreren virtuellen Subnetzen. Ein virtuelles Netzwerk bildet eine Isolations Grenze, bei der die virtuellen Computer in einem virtuellen Netzwerk nur miteinander kommunizieren können. Normalerweise wurde diese Isolation mithilfe von VLANs mit einem getrennten IP-Adressbereich und einem 802.1 q-Tag oder einer VLAN-ID erzwungen. Mit HNV wird die Isolation jedoch entweder mithilfe von nvgre oder vxlan-Kapselung erzwungen, um Überlagerungs Netzwerke zu erstellen, die sich überlappende IP-Subnetze zwischen Kunden oder Mandanten befinden.

-   Jedes virtuelle Netzwerk verfügt über eine eindeutige Routing Domänen-ID (rdid) auf dem Host. Diese rdid ist ungefähr einer Ressourcen-ID zugeordnet, um die Rest-Ressource des virtuellen Netzwerks im Netzwerk Controller zu identifizieren. Auf die Rest-Ressource des virtuellen Netzwerks wird mithilfe eines Uniform Resource Identifier (URI)-Namespace mit der angefügten Ressourcen-ID verwiesen.

### <a name="virtual-subnets"></a><a name="VirtualSubnets"></a>Virtuelle Subnetze

-   Ein virtuelles Subnetz implementiert die Layer 3-IP-Subnet-Semantik für die virtuellen Computer, die sich im gleichen virtuellen Subnetz befinden. Das virtuelle Subnetz bildet eine Broadcast Domäne (ähnlich wie ein VLAN), und die Isolation wird durch die Verwendung des Felds nvgre-Mandanten Netzwerk-ID (TNI) oder vxlan-netzwerkbezeichnerfeld (vni) erzwungen.

-   Jedes virtuelle Subnetz gehört zu einem einzelnen virtuellen Netzwerk (rdid), und ihm wird eine eindeutige vsid (Virtual Subnetz ID) zugewiesen. dabei wird entweder der TNI-oder der vni-Schlüssel im Header für gekapselte Pakete verwendet. Die vsid muss innerhalb des Rechenzentrums eindeutig sein und liegt im Bereich von 4096 bis 2 ^ 24-2.

Ein wichtiger Vorteil des virtuellen Netzwerks und der Routing Domäne besteht darin, dass Kunden ihre eigenen Netzwerktopologien (z. b. IP-Subnetze) in die Cloud bringen können. In Abbildung 2 wird ein Beispiel gezeigt, in dem das Unternehmen Contoso Corp. über zwei separate Netzwerke verfügt: "F&E-Netzwerk" für Forschung und Entwicklung und "Vertriebsnetzwerk" für den Vertrieb. Da beide Netzwerke unterschiedliche Routingdomänen-IDs besitzen, sind keine Interaktionen zwischen den Netzwerken möglich. Das heißt, das "Contoso-F&E-Netzwerk" ist vom "Contoso-Vertriebsnetzwerk" isoliert, obgleich beide Subnetze mit Contoso Corp. den gleichen Besitzer haben. "Contoso-F&E-Netzwerk" enthält drei virtuelle Subnetze. Beachten Sie, dass sowohl die RDID als auch VSID innerhalb eines Datencenters eindeutig sind.

![Kundennetzwerke und virtuelle Subnetze](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF6.gif)

Abbildung 2: Kundennetzwerke und virtuelle Subnetze

**Layer 2-Weiterleitung**

In Abbildung 2 können die Pakete der virtuellen Computer in vsid 5001 an virtuelle Computer weitergeleitet werden, die auch in der vsid 5001 über den Hyper-V-Switch vorhanden sind. Die eingehenden Pakete von einem virtuellen Computer in vsid 5001 werden an einen bestimmten VPort auf dem Hyper-V-Switch gesendet. Eingangs Regeln (z. b. ENCAP) und Zuordnungen (z. b. Kapselungs Header) werden vom Hyper-V-Switch für diese Pakete angewendet. Die Pakete werden dann entweder an einen anderen VPort auf dem Hyper-v-Switch (sofern der virtuelle Zielcomputer an denselben Host angefügt ist) oder an einen anderen Hyper-v-Switch auf einem anderen Host weitergeleitet (wenn sich der virtuelle Zielcomputer auf einem anderen Host befindet).

**Layer 3-Routing**

Entsprechend können die virtuellen Computer in vsid 5001 die Pakete an virtuelle Maschinen in vsid 5002 oder vsid 5003 durch den verteilten HNV-Router weiterleiten, der in den vSwitches des Hyper-v-Hosts vorhanden ist. Bei der Übermittlung des Pakets an den Hyper-V-Switch wird die vsid des eingehenden Pakets von HNV auf die vsid des virtuellen Ziel Computers aktualisiert. Dies geschieht nur dann, wenn sich beide VSIDs in der gleichen RDID befinden.  Daher können von virtuellen Netzwerkadaptern mit rdid 1 keine Pakete an virtuelle Netzwerkadapter mit rdid 2 senden gesendet werden, ohne dass ein Gateway durchlaufen wird.

> [!NOTE]
> In der obigen Beschreibung des Paket Flusses bedeutet der Begriff "virtueller Computer" tatsächlich den virtuellen Netzwerkadapter auf dem virtuellen Computer. Ein virtueller Computer verfügt üblicherweise nur über einen einzigen virtuellen Netzwerkadapter. In diesem Fall können die Wörter "virtueller Computer" und "virtueller Netzwerkadapter" konzeptionell dasselbe bedeuten.

Jedes virtuelle Subnetz legt ein Layer-3-IP-Subnetz und eine Layer-2-(L2)-Übertragungsdomänenbegrenzung ähnlich einem VLAN fest. Wenn ein virtueller Computer ein Paket überträgt, verwendet HNV die unicastreplikation (UR), um eine Kopie des ursprünglichen Pakets zu erstellen und die Ziel-IP und den Mac durch die Adressen der einzelnen virtuellen Computer zu ersetzen, die sich in derselben vsid befinden.

> [!NOTE]
> Wenn Windows Server 2016 ausgeliefert wird, werden Broadcast-und subnetzmulticasts mithilfe der unicastreplikation implementiert. Subnetzübergreifende Multicast Routing und IGMP werden nicht unterstützt.

Neben ihrer Rolle als Übertragungsdomäne bewirkt die VSID auch die Isolation. Ein virtueller Netzwerkadapter in HNV ist mit einem Hyper-v-Switchport verbunden, für den ACL-Regeln entweder direkt auf den Port (virtualnetworkinterface-Rest-Ressource) oder auf das virtuelle Subnetz (vsid) angewendet werden, zu dem es gehört.

Für den Hyper-V-Switchport muss eine ACL-Regel angewendet werden. Diese ACL kann alle zulassen, alle ablehnen oder spezifischer sein, um nur bestimmte Arten von Datenverkehr basierend auf 5-Tupel (Quell-IP, Ziel-IP, Quellport, Zielport, Protokoll) abzugleichen.

> [!NOTE]
> Hyper-V-switcherweiterungen können im neuen Sdn-Stapel (Software Defined Networking) nicht mit HNVv2 verwendet werden. HNVv2 wird mithilfe der Azure Virtual Filtering Platform (VFP)-Switcherweiterung implementiert, die nicht in Verbindung mit anderen switcherweiterungen von Drittanbietern verwendet werden kann.

## <a name="switching-and-routing-in-hyper-v-network-virtualization"></a>Wechseln und Routing in der Hyper-V-Netzwerkvirtualisierung
HNVv2 implementiert korrekte Layer 2 (L2)-Wechsel und Layer 3 (L3)-Routing Semantik, um so wie ein physischer Switch oder Router funktionieren zu können. Wenn ein virtueller Computer, der mit einem virtuellen HNV-Netzwerk verbunden ist, versucht, eine Verbindung mit einem anderen virtuellen Computer im gleichen virtuellen Subnetz (vsid) herzustellen, muss zunächst die Mac-Adresse der Zertifizierungsstelle des virtuellen Remote Computers erlernt werden. Wenn für die IP-Adresse des virtuellen Ziel Computers in der ARP-Tabelle des Quell Computers ein ARP-Eintrag vorhanden ist, wird die Mac-Adresse dieses Eintrags verwendet. Wenn kein Eintrag vorhanden ist, sendet die virtuelle Quell Maschine eine ARP-Broadcast mit einer Anforderung für die Mac-Adresse, die der zurück zugegenden IP-Adresse des virtuellen Ziel Computers entspricht. Mit dem Hyper-V-Switch wird diese Anforderung abgefangen und an den Host-Agent gesendet. Der Host-Agent sucht in der lokalen Datenbank nach einer entsprechenden MAC-Adresse für die IP-Adresse der angeforderten virtuellen Zielmaschine.

> [!NOTE]
> Der Host-Agent, der als ovsdb-Server fungiert, verwendet eine Variante des vtep-Schemas, um ca-PA-Zuordnungen, Mac-Tabellen usw. zu speichern.

Wenn eine Mac-Adresse verfügbar ist, fügt der Host-Agent eine ARP-Antwort ein und sendet diese an den virtuellen Computer zurück. Nachdem der Netzwerk Stapel des virtuellen Computers über alle erforderlichen L2-Header Informationen verfügt, wird der Frame an den entsprechenden Hyper-V-Port auf dem V-Switch gesendet. Intern testet der Hyper-V-Switch diesen Frame mit N-Tupel-abgleichsregeln, die dem V-Port zugewiesen sind, und wendet bestimmte Transformationen auf den Frame basierend auf diesen Regeln an. Vor allem wird ein Satz von Kapselungs Transformationen angewendet, um den Kapselungs Header mithilfe von nvgre oder vxlan zu erstellen, abhängig von der Richtlinie, die auf dem Netzwerk Controller definiert ist. Basierend auf der vom Host-Agent programmierten Richtlinie wird eine ca-PA-Zuordnung verwendet, um die IP-Adresse des Hyper-V-Hosts zu ermitteln, auf dem sich die virtuelle Zielmaschine befindet. Mit dem Hyper-V-Switch wird sichergestellt, dass die richtigen Routing Regeln und VLAN-Tags auf das äußere Paket angewendet werden, sodass die Remote-PA-Adresse erreicht wird.

Wenn ein virtueller Computer, der mit einem virtuellen HNV-Netzwerk verbunden ist, eine Verbindung mit einer virtuellen Maschine in einem anderen virtuellen Subnetz (vsid) herstellen möchte, muss das Paket entsprechend weitergeleitet werden. HNV geht von einer Sterntopologie aus, bei der nur eine IP-Adresse im Zertifizierungsstellen Bereich vorhanden ist, die als nächster Hop verwendet wird, um alle IP-Präfixe zu erreichen (d.h. eine Standardroute/ein Standard Gateway). Derzeit erzwingt dies eine Einschränkung für eine einzelne Standardroute, und nicht standardmäßige Routen werden nicht unterstützt.

### <a name="routing-between-virtual-subnets"></a>Routing zwischen virtuellen Subnetzen
In einem physischen Netzwerk ist ein IP-Subnetz eine Layer 2-Domäne (L2), in der Computer (virtuell und physisch) direkt miteinander kommunizieren können. Die L2-Domäne ist eine Broadcast Domäne, bei der ARP-Einträge (IP: Mac Address Map) durch ARP-Anforderungen erlernt werden, die auf allen Schnittstellen übertragen werden, und ARP-Antworten an den anfordernden Host zurückgesendet werden. Der Computer verwendet die von der ARP-Antwort gewonnenen Mac-Informationen, um den L2-Frame einschließlich Ethernet-Headern vollständig zu konstruieren. Wenn sich eine IP-Adresse jedoch in einem anderen L3-Subnetz befindet, überschreitet die ARP-Anforderung diese L3-Grenze nicht. Stattdessen muss eine L3-Routerschnittstelle (nächster Hop oder Standard Gateway) mit einer IP-Adresse im quellsubnetz auf diese ARP-Anforderungen mit ihrer eigenen Mac-Adresse antworten.

In standardmäßigen Windows-Netzwerken kann ein Administrator statische Routen erstellen und diese einer Netzwerkschnittstelle zuweisen. Außerdem wird in der Regel ein "Standard Gateway" als IP-Adresse für den nächsten Hop an einer Schnittstelle konfiguriert, auf der für die Standardroute (0.0.0.0/0) bestimmte Pakete gesendet werden. Pakete werden an dieses Standard Gateway gesendet, wenn keine bestimmten Routen vorhanden sind. Dies ist normalerweise der Router für das physische Netzwerk.  HNV verwendet einen integrierten Router, der Teil jedes Hosts ist und über eine Schnittstelle in jeder vsid verfügt, um einen verteilten Router für die virtuellen Netzwerke zu erstellen.

Da HNV eine Sterntopologie annimmt, fungiert der verteilte HNV-Router als einzelnes Standard Gateway für den gesamten Datenverkehr zwischen virtuellen Subnetzen, die Teil desselben vsid-Netzwerks sind. Die als Standard Gateway verwendete Adresse wird standardmäßig auf die niedrigste IP-Adresse in der vsid festgelegt und dem verteilten HNV-Router zugewiesen. Dieser verteilte Router ermöglicht eine sehr effiziente Methode für den gesamten Datenverkehr in einem vsid-Netzwerk, da jeder Host den Datenverkehr direkt an den entsprechenden Host weiterleiten kann, ohne dass ein Vermittler erforderlich ist.  Dies gilt insbesondere dann, wenn sich zwei virtuelle Computer im gleichen VM-Netzwerk befinden, während auf dem gleichen physischen Host verschiedene virtuelle Subnetze vorhanden sind.  Weiter unten in diesem Abschnitt wird darauf eingegangen, dass das Paket den physischen Host nie verlassen muss.

### <a name="routing-between-pa-subnets"></a>Routing zwischen PA-Subnetzen
Im Gegensatz zu HNVv1, die eine PA-IP-Adresse für jedes virtuelle Subnetz (vsid) zugeordnet haben, verwendet HNVv2 nun eine PA-IP-Adresse pro Switch-Embedded Teaming (Set) NIC Team-Mitglied. Bei der Standard Bereitstellung wird von einem zwei-NIC-Team ausgegangen und zwei PA-IP-Adressen pro Host zugewiesen. Einem einzelnen Host sind PA-IP-Adressen aus dem logischen Subnetz des Anbieters (PA) im gleichen VLAN zugewiesen. Zwei Mandanten-VMS im gleichen virtuellen Subnetz können sich tatsächlich auf zwei verschiedenen Hosts befinden, die mit zwei verschiedenen logischen Anbieter-Subnetzen verbunden sind. HNV erstellt die äußeren IP-Header für das gekapselte Paket basierend auf der ca-PA-Zuordnung. Er basiert jedoch auf dem TCP/IP-Host Stapel für das Standard-PA-Gateway und erstellt dann die äußeren Ethernet-Header basierend auf der ARP-Antwort. In der Regel stammt diese ARP-Antwort von der SVI-Schnittstelle auf dem physischen Switch oder dem L3-Router, mit dem der Host verbunden ist. HNV basiert daher auf dem L3-Router zum Weiterleiten der gekapselten Pakete zwischen logischen Subnetzen/VLANs des Anbieters.

### <a name="routing-outside-a-virtual-network"></a>Routing außerhalb eines virtuellen Netzwerks
Bei den meisten Kundenbereitstellungen wird es erforderlich sein, dass aus der Hyper-V-Netzwerkvirtualisierungsumgebung heraus mit Ressourcen kommuniziert werden kann, die nicht zur Hyper-V-Netzwerkvirtualisierungsumgebung gehören. Damit eine Kommunikation zwischen diesen beiden Umgebungen möglich ist, sind Netzwerkvirtualisierungsgateways erforderlich. Infrastrukturen, die ein HNV-Gateway erfordern, umfassen die Private Cloud und die hybride Cloud. Im Grunde sind HNV-Gateways für das Layer 3-Routing zwischen internen und externen (physischen) Netzwerken (einschließlich NAT) oder zwischen unterschiedlichen Standorten und/oder Clouds (privat oder öffentlich) erforderlich, die ein IPSec-VPN oder einen GRE-Tunnel verwenden.

Gateways sind in verschiedenen Formfaktoren erhältlich. Sie können auf Windows Server 2016 erstellt werden, das in einen Tor-Switch (Top of Rack) integriert ist, der als vxlan-Gateway fungiert, auf das über eine virtuelle IP-Adresse (VIP) zugegriffen wird, die von einem Load Balancer angekündigt wird, in andere vorhandene Netzwerkgeräte eingefügt wird oder ein neues eigenständiges Netzwerkgerät sein kann.

Weitere Informationen zu den Optionen des Windows RAS-Gateways finden Sie unter [RAS-Gateway](../../../../remote/remote-access/ras-gateway/RAS-Gateway.md).

## <a name="packet-encapsulation"></a>Paketkapselung
Jedem virtuellen Netzwerkadapter werden bei der Hyper-V-Netzwerkvirtualisierung zwei IP-Adressen zugeordnet:

-   **Kundenadresse (Customer Address** , ca) die IP-Adresse, die vom Kunden basierend auf der Intranetinfrastruktur zugewiesen wird. Diese Adresse ermöglicht es dem Kunden, Netzwerk Datenverkehr mit dem virtuellen Computer so auszutauschen, als ob er nicht zu einem öffentlichen oder Private Cloud verschoben worden wäre. Die Kundenadresse (CA) ist für den virtuellen Computer sichtbar und für den Kunden zugänglich.

-   **Anbieter Adresse (Provider Address** , PA) die IP-Adresse, die vom Hostinganbieter oder den Daten Center Administratoren basierend auf der physischen Netzwerkinfrastruktur zugewiesen wird. Die PA steht in den Netzwerkpaketen, die mit dem Hyper-V-Server ausgetauscht werden, der als Host für den virtuellen Computer dient. Die PA ist im physischen Netzwerk, jedoch nicht für den virtuellen Computer sichtbar.

Mit den CAs wird die Netzwerktopologie des Kunden abgebildet, die virtualisiert und von der eigentlichen, darunter befindlichen physischen Netzwerktopologie mit ihren Adressen gemäß der Implementierung der PAs (Anbieteradressen) entkoppelt wird. In der folgenden Abbildung wird gezeigt, welche konzeptionelle Beziehung zwischen den CAs des virtuellen Computers und den PAs der Netzwerkinfrastruktur bei einer Netzwerkvirtualisierung besteht.

![Konzeptionelle Darstellung der Netzwerkvirtualisierung über eine physische Infrastruktur](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF2.gif)

Abbildung 6: Konzeptionelle Darstellung der Netzwerkvirtualisierung über eine physische Infrastruktur

Im Diagramm senden Kunden virtuelle Computer Datenpakete im Zertifizierungsstellen Bereich, die die physische Netzwerkinfrastruktur über ihre eigenen virtuellen Netzwerke oder "Tunnel" durchlaufen. Im obigen Beispiel können die Tunnel als "Umschläge" um die Datenpakete von "ca" und "Fabrikam" mit grünen Versand Bezeichnungen (PA-Adressen) betrachtet werden, die vom Quellhost auf der linken Seite an den Zielhost rechts übermittelt werden sollen. Der Schlüssel ist, wie die Hosts die "Lieferadressen" (PA-Adressen) bestimmen, die der Zertifizierungsstelle von "ca" und der Fabrikam-Zertifizierungsstelle entsprechen, wie der "Umschlag" die Pakete umschließt und wie die Ziel Hosts die Pakete entpacken und an die virtuellen Zielcomputer von "subtoso" und "Fabrikam" übermitteln können.

Diese einfache Analogie verdeutlicht die wichtigsten Aspekte bei der Netzwerkvirtualisierung:

-   Jede CA eines virtuellen Computers ist einer PA eines physischen Hosts zugeordnet. Einer PA können mehrere CAs zugeordnet sein.

-   Virtuelle Computer senden Datenpakete in den ZS-Leerzeichen, die in einem "Umschlag" mit einem PA-Quell-und zielpaar auf der Grundlage der Zuordnung abgelegt werden.

-   Anhand der CA-PA-Zuordnungen müssen die Hosts unterscheiden können, welche Pakete für welchen virtuellen Kundencomputer bestimmt sind.

Die Virtualisierung des Netzwerks wird also dadurch realisiert, indem die von den virtuellen Computern verwendeten Netzwerkadressen virtualisiert werden. Der Netzwerk Controller ist für die Adress Zuordnung zuständig, und der Host-Agent verwaltet die Zuordnungs Datenbank mit dem MS_VTEP Schema. Der zur Adressvirtualisierung eingesetzte Mechanismus wird im nächsten Abschnitt beschrieben.

## <a name="network-virtualization-through-address-virtualization"></a>Netzwerkvirtualisierung durch Adressvirtualisierung
HNV implementiert Überlagerungs Mandanten Netzwerke entweder mithilfe der generischen Routing Kapselung für die Netzwerkvirtualisierung (nvgre) oder über das virtuelle erweiterbare lokale Netzwerk (vxlan).  Vxlan ist die Standardeinstellung.

### <a name="virtual-extensible-local-area-network-vxlan"></a>Virtuelles erweiterbares LAN (Local Area Network, vxlan)
Das vxlan (Virtual Extensible Local Area Network)-Protokoll ([RFC 7348](https://www.rfc-editor.org/info/rfc7348)) wurde auf dem Marktplatz weit verbreitet und bietet Unterstützung von Anbietern wie Cisco, Brocade, Arista, Dell, HP und anderen. Das vxlan-Protokoll verwendet UDP als Transport. Der IANA-zugewiesene UDP-Zielport für vxlan ist 4789, und der UDP-Quellport muss ein Hash der Informationen aus dem inneren Paket sein, das für die ECMP-Verteilung verwendet werden soll. Nach dem UDP-Header wird ein vxlan-Header an das Paket angehängt, das ein reserviertes 4-Byte-Feld enthält, gefolgt von einem 3-Byte-Feld für die vxlan-Netzwerk Kennung (vni)-vsid, gefolgt von einem anderen reservierten 1-Byte-Feld. Nach dem vxlan-Header wird der ursprüngliche ca-L2-Frame (ohne die ca-Ethernet-Frame-FCS) angefügt.

![Vxlan-Paket Header](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VXLAN-packet-header.png)

### <a name="generic-routing-encapsulation-nvgre"></a>Generische Routing Kapselung (nvgre)
Dieser netzwerkvirtualisierungstechnmechanismus verwendet die generische Routing Kapselung (nvgre) als Teil des Tunnel Headers. In nvgre wird das Paket des virtuellen Computers in einem anderen Paket gekapselt. Der Header dieses neuen Pakets enthält neben der virtuellen Subnetz-ID (Virtual Subnet ID) – die im Key-Feld des GRE-Headers gespeichert ist (siehe Abbildung 7) – auch die entsprechenden PA-IP-Quell- und -Zieladressen.

![NVGRE-Kapselung](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF3.gif)

Abbildung 7: Netzwerkvirtualisierung – NVGRE-Kapselung

Die ID des virtuellen Subnetzes ermöglicht Hosts die Identifizierung des virtuellen Kunden Computers für ein beliebiges Paket, obwohl sich die PA-und die Zertifizierungsstellen in den Paketen möglicherweise überlappen. Daher kann auch für alle virtuellen Computer auf dem gleichen Host eine einzige PA gemeinsam genutzt werden (siehe Abbildung 7).

Diese gemeinsame Nutzung spielt bei der Netzwerkskalierbarkeit eine große Rolle. So kann die Anzahl der IP- und MAC-Adressen, die der Netzwerkinfrastruktur bekannt sein müssen, beträchtlich reduziert werden. Wenn zum Beispiel jeder Endhost durchschnittlich 30 virtuelle Computer beherbergt, wird die Anzahl der IP- und Mac-Adressen in diesem Fall um den Faktor 30 gesenkt. Außerdem ermöglichen die in den Paketen eingebetteten Virtual Subnet IDs eine einfache Zuordnung der Pakete zu den Kunden.

Das PA-Freigabe Schema für Windows Server 2012 R2 ist eine PA pro vsid pro Host. Für Windows Server 2016 ist das Schema eine PA pro NIC-Teammitglied.

Mit Windows Server 2016 und höher unterstützt HNV nvgre und vxlan standardmäßig vollständig. das Upgrade oder der Erwerb neuer Netzwerkhardware (z. b. NICs (Netzwerkadapter), Switches oder Router) ist nicht erforderlich. Dies liegt daran, dass es sich bei diesen Paketen im Netzwerk um ein reguläres IP-Paket im PA-Raum handelt, das mit der heutigen Netzwerkinfrastruktur kompatibel ist.  Um die optimale Leistung zu erzielen, verwenden Sie jedoch die unterstützten NICs mit den neuesten Treibern, die Aufgaben Offloads unterstützen.

## <a name="multi-tenant-deployment-example"></a>Beispiel für mehrinstanzenfähige Bereitstellung
Das folgende Diagramm zeigt ein Beispiel für die Bereitstellung von zwei Kunden, die sich in einem cloudrechenzentrum mit der von den Netzwerk Richtlinien definierten ca-PA-Beziehung befinden.

![Beispiel für mehrinstanzenfähige Bereitstellung](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF5.png)

Abbildung 8: Beispiel für eine mehrinstanzenfähige Bereitstellung

Betrachten Sie das Beispiel in Abbildung 8. Vor dem Verschieben in den freigegebenen IaaS-Dienst des Hostinganbieters:

-   Contoso Corp. führte unter der IP-Adresse 10.1.1.11 einen SQL-Server (mit dem Namen **SQL**) und unter der IP-Adresse 10.1.1.12 einen Webserver (mit dem Namen **Web**) aus, für dessen Datenbanktransaktionen der zugehörige SQL-Server verwendet wurde.

-   Auch Fabrikam Corp. führte einen SQL-Server (**SQL**) unter der zugewiesenen IP-Adresse 10.1.1.11 und einen Webserver (**Web**) unter der IP-Adresse 10.1.1.12 aus, für dessen Datenbanktransaktionen der zugehörige SQL-Server verwendet wurde.

Wir gehen davon aus, dass der hostingdienstanbieter zuvor das logische Netzwerk des Anbieters (PA) über den Netzwerk Controller erstellt hat, damit er der physischen Netzwerktopologie entspricht. Der Netzwerk Controller ordnet zwei PA-IP-Adressen aus dem IP-Präfix des logischen Subnetzes an, in dem die Hosts verbunden sind. Der Netzwerk Controller gibt auch das entsprechende VLAN-Tag zum Anwenden der IP-Adressen an.

Mit dem Netzwerk Controller werden von "Configuration Manager" und "Fabrikam Corp" dann das virtuelle Netzwerk und die Subnetze erstellt, die vom logischen Netzwerk des Anbieters (PA) unterstützt werden, das vom hostingdienstanbieter angegeben wird. Contoso Corp. und Fabrikam Corp. verschieben ihre jeweiligen SQL-Server und Webserver in den freigegebenen IaaS-Dienst des gleichen Hostinganbieters. Dort wird zufällig der virtuelle Computer **SQL** auf dem Hyper-V Host 1 und der virtuelle Computer **Web** (IIS7) auf dem Hyper-V-Host 2 ausgeführt. Alle virtuellen Computer behalten die ursprünglichen Intranet-IP-Adressen (CAs) bei.

Beiden Unternehmen wird die folgende vsid (Virtual Subnet ID) vom Netzwerk Controller zugewiesen, wie unten angegeben.  Der Host-Agent auf allen Hyper-V-Hosts empfängt die zugeordneten PA-IP-Adressen vom Netzwerk Controller und erstellt zwei PA-Host-vNICs in einem nicht standardmäßigen Netzwerk Depot. Jeder dieser Host-vNICs wird eine Netzwerkschnittstelle zugewiesen, wobei die PA-IP-Adresse wie unten dargestellt zugewiesen wird:

-   Die virtuellen Computer der virtuellen Computer von "vsid" und "Pas: **vsid** " von "Configuration Manager" sind 5001, **SQL PA** ist 192.168.1.10, **Web PA** ist 192.168.2.20

-   Die vsid für die virtuellen Computer von Fabrikam Corp und Pas: **vsid** ist 6001, **SQL PA** ist 192.168.1.10, **Web PA** ist 192.168.2.20

Der Netzwerk Controller führt die gesamte Netzwerk Richtlinie (einschließlich der ZS-PA-Zuordnung) zum Sdn-Host-Agent aus, der die Richtlinie in einem permanenten Speicher (in den ovsdb-Datenbanktabellen) beibehält.

Wenn der virtuelle Computer "Web-so Corp." (10.1.1.12) auf dem Hyper-V-Host 2 eine TCP-Verbindung mit dem SQL Server unter 10.1.1.11 erstellt, geschieht Folgendes:

-   VM-Arps für die MAC-Zieladresse von 10.1.1.11

-   Die VFP-Erweiterung im Vswitch fängt dieses Paket ab und sendet es an den Sdn-Host-Agent.

-   Der Sdn-Host-Agent sucht in seinem Richtlinien Speicher nach der Mac-Adresse für 10.1.1.11

-   Wenn ein Mac gefunden wird, fügt der Host-Agent eine ARP-Antwort zurück an den virtuellen Computer.

-   Wenn ein Mac nicht gefunden wird, wird keine Antwort gesendet, und der ARP-Eintrag auf dem virtuellen Computer für 10.1.1.11 wird als nicht erreichbar markiert.

-   Der virtuelle Computer erstellt nun ein TCP-Paket mit dem richtigen Zertifizierungsstellen-Ethernet und IP-Headern und sendet es an den Vswitch.

-   Die VFP-Weiterleitungs Erweiterung im Vswitch verarbeitet dieses Paket über die VFP-Schichten (siehe unten), die dem Quell-Vswitch-Port zugewiesen sind, auf dem das Paket empfangen wurde, und erstellt einen neuen Flow-Eintrag in der Tabelle "vereinheitlichte Tabelle" von VFP.

-   Die VFP-Engine führt auf der Grundlage der IP-und Ethernet-Header für jede Schicht (z. b. virtuelle Netzwerkebene) eine Regel Übereinstimmung oder eine Fluss Tabellen Suche aus.

-   Die übereinstimmende Regel auf der Ebene des virtuellen Netzwerks verweist auf einen Zertifizierungsbereich der Zertifizierungsstellen-PA und führt Kapselung durch.

-   Der Kapselungstyp (vxlan oder nvgre) wird in der vnet-Ebene zusammen mit der vsid angegeben.

-   Im Fall der vxlan-Kapselung wird ein äußerer UDP-Header mit der vsid 5001 im vxlan-Header erstellt.
    Ein äußerer IP-Header wird mit der Quell-und Ziel-PA-Adresse erstellt, die dem Hyper-v-Host 2 (192.168.2.20) bzw. dem Hyper-v-Host 1 (192.168.1.10) zugewiesen ist, basierend auf dem Richtlinien Speicher des SDN-Host-Agents.

-   Dieses Paket wird dann zur PA-Routing Schicht in VFP weiterleiten.

-   Die PA-Routing Schicht in VFP verweist auf das Netzwerk Depot, das für den Datenverkehr im PA-Bereich und eine VLAN-ID verwendet wird, und verwendet den TCP/IP-Stapel des Hosts, um das PA-Paket ordnungsgemäß an den Hyper-V-Host zu über

-   Nach dem Empfang des gekapselten Pakets empfängt der Hyper-V-Host 1 das Paket im PA-Netzwerk Depot und weiter an den Vswitch.

-   Der VFP verarbeitet das Paket über seine VFP-Schichten und erstellt einen neuen Flow-Eintrag in der Tabelle "Unified Flow" von VFP.

-   Die VFP-Engine gleicht die Ingres-Regeln in der Ebene des virtuellen Netzwerks ab und entfernt die Ethernet-, IP-und vxlan-Header des äußeren gekapselten Pakets.

-   Die VFP-Engine leitet das Paket dann an den Vswitch-Port weiter, mit dem der virtuelle Zielcomputer verbunden ist.

Ein ähnlicher Prozess beim Datenverkehr zwischen den virtuellen Computern **Web** und **SQL** von Fabrikam Corp. verwendet die Hyper-V-Netzwerkvirtualisierungs-Richtlinieneinstellungen für Fabrikam Corp. Dies hat zur Folge, dass die virtuellen Computer von Fabrikam Corp. und Contoso Corp. dank Hyper-V-Netzwerkvirtualisierung so miteinander interagieren, als befänden sie sich noch in den ursprünglichen Intranets. Mit den virtuellen Computern des jeweils anderen Unternehmens findet keine Interaktion statt, auch wenn für diese die gleichen IP-Adressen verwendet werden.

Die separaten Adressen (CAS und PAS), die Richtlinien Einstellungen der Hyper-V-Hosts und die Adressübersetzung zwischen der Zertifizierungsstelle und der PA für eingehenden und ausgehenden Datenverkehr für virtuelle Computer isolieren diese Server Gruppen mithilfe des nvgre-Schlüssels oder des vlxan-VNID. Außerdem wird die virtuelle Netzwerkarchitektur durch die Virtualisierungszuordnungen und -umwandlungen von der physischen Netzwerkarchitektur entkoppelt. Obwohl sich Contoso **SQL** und **Web** sowie Fabrikam **SQL** und **Web** in jeweils eigenen CA-IP-Subnetzen befinden (10.1.1/24), werden sie physisch auf zwei Hosts in unterschiedlichen PA-Subnetzen bereitgestellt: 192.168.1/24 bzw. 192.168.2/24. Dies bringt mit sich, dass durch Hyper-V-Netzwerkvirtualisierung subnetzübergreifende Bereitstellungen virtueller Computer und Livemigrationen möglich werden.

## <a name="hyper-v-network-virtualization-architecture"></a>Architektur der Hyper-V-Netzwerkvirtualisierung
In Windows Server 2016 wird HNVv2 mit der Azure Virtual Filtering Platform (VFP) implementiert, bei der es sich um eine NDIS-Filter Erweiterung innerhalb des Hyper-V-Switches handelt. Das Hauptkonzept von VFP ist die eines abgleichsaktions-Laufwerks mit einer internen API, die dem SDN-Host-Agent zum Programmieren der Netzwerk Richtlinie zur Verfügung gestellt wird. Der Sdn-Host-Agent selbst empfängt eine Netzwerk Richtlinie vom Netzwerk Controller über die ovsdb-und WCF Southbound-Kommunikationskanäle. Nicht nur die Richtlinie für virtuelle Netzwerke (z. b. ca-PA-Zuordnung), die mithilfe von VFP programmiert wurde, sondern auch zusätzliche Richtlinien wie ACLs, QoS usw.

Die Objekthierarchie für die Vswitch-und VFP-Weiterleitungs Erweiterung lautet wie folgt:

-   Vswitch

    -   Externe NIC-Verwaltung

    -   Nic-Hardware Abladungen

    -   Globale Weiterleitungs Regeln

    -   Port

        -   Ausgehende Weiterleitungs Ebene für das Haar schwenken

        -   Speicherplatz Listen für Zuordnungen und NAT-Pools

        -   Unified Flow-Tabelle

        -   VFP-Ebene

            -   Fluss Tabelle

            -   Group

            -   Regel

                -   Regeln können auf Leerzeichen verweisen

Im VFP wird eine Ebene pro Richtlinientyp erstellt (z. b. Virtual Network) und ist ein generischer Satz von Regel-/Fluss Tabellen. Sie besitzt keine intrinsische Funktionalität, bis dieser Ebene bestimmte Regeln zugewiesen sind, um diese Funktionalität zu implementieren. Jeder Ebene wird eine Priorität zugewiesen, und Ebenen werden einem Port durch aufsteigender Priorität zugewiesen. Regeln sind in Gruppen organisiert, die in erster Linie auf Richtung und IP-Adressfamilie basieren. Gruppen wird außerdem eine Priorität zugewiesen, und höchstens eine Regel aus einer Gruppe kann einem bestimmten Flow entsprechen.

Die Weiterleitungs Logik für den Vswitch mit VFP-Erweiterung lautet wie folgt:

-   Eingangs Verarbeitung (Eingang von der Sicht des Pakets, das in einen Port kommt)

-   Mittelt

-   Ausgehende Verarbeitung (ausgehend von der Sicht eines Pakets, das einen Port verlässt)

Der VFP unterstützt die interne Mac-Weiterleitung für nvgre-und vxlan-Kapselungs Typen sowie die externe Mac-VLAN-basierte Weiterleitung.

Die VFP-Erweiterung weist einen langsamen Pfad und einen schnellen Pfad für den Paket Durchlauf auf. Das erste Paket in einem Flow muss alle Regel Gruppen in jeder Ebene durchlaufen und eine Regel Suche durchführen, bei der es sich um einen teuren Vorgang handelt. Sobald jedoch ein Flow in der Unified Flow-Tabelle mit einer Liste von Aktionen (basierend auf den übereinstimmenden Regeln) registriert wird, werden alle nachfolgenden Pakete auf der Grundlage der vereinheitlichten Datenfluss Tabelleneinträge verarbeitet.

Die HNV-Richtlinie wird vom Host-Agent programmiert. Jeder Netzwerkadapter für virtuelle Computer ist mit einer IPv4-Adresse konfiguriert. Das sind die CAs, mit deren Hilfe die virtuellen Computer miteinander kommunizieren, und sie sind in den aus den virtuellen Computern abgehenden Paketen enthalten. HNV kapselt den ZS-Frame in einem PA-Frame, der auf den in der Datenbank des Host-Agents gespeicherten netzwerkvirtualisierungsrichtlinien basiert.

![HNV-Architektur](../../../media/hyper-v-network-virtualization-technical-details-in-windows-server/VNetF7.png)

Abbildung 9: Architektur der Hyper-V-Netzwerkvirtualisierung

## <a name="summary"></a>Zusammenfassung
Cloudbasierte Datencenter bieten viele Vorteile, wie zum Beispiel eine bessere Skalierbarkeit und Ressourcenauslastung. Um diese potenziellen Vorteile praktisch nutzen zu können, ist eine Technologie erforderlich, die sich um die Problematik der mehrinstanzenfähigen Skalierbarkeit in einer dynamischen Umgebung kümmert. Hyper-V-Netzwerkvirtualisierung wurde für diese Problematik entworfen. Außerdem wird die Effizienz von Datencentern erhöht, indem die virtuelle von der physischen Netzwerktopologie entkoppelt wird. Wenn Sie auf einem vorhandenen Standard aufbauen, wird HNV im heutigen Rechenzentrum ausgeführt und arbeitet mit Ihrer vorhandenen vxlan-Infrastruktur. Kunden mit HNV können Ihre Rechenzentren nun in einem Private Cloud konsolidieren oder Ihre Rechenzentren nahtlos auf die Umgebung eines Host Server Anbieters mit einem Hybrid Cloud ausdehnen.

## <a name="see-also"></a><a name="BKMK_LINKS"></a>Siehe auch
Weitere Informationen zu HNVv2 finden Sie unter den folgenden Links:


|       Inhaltstyp       |                                                                                                                                              Referenzen                                                                                                                                              |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Communityressourcen**  |                                                                -   [Blog der Private Cloud-Architektur](https://blogs.technet.com/b/privatecloud)<br />-Fragen stellen:[cloudnetfb@microsoft.com](mailto:%20cloudnetfb@microsoft.com)                                                                |
|         **RFC**          |                                                                   -   [Nvgre Draft RFC](https://www.ietf.org/id/draft-sridharan-virtualization-nvgre-07.txt)<br />-   [Vxlan: RFC 7348](https://www.rfc-editor.org/info/rfc7348)                                                                    |
| **Verwandte Technologien** | -Technische Details zur Hyper-v-Netzwerkvirtualisierung unter Windows Server 2012 R2 finden Sie unter [Technische Details zur Hyper-v-Netzwerkvirtualisierung](https://technet.microsoft.com/library/jj134174.aspx) .<br />-   [Netzwerk Controller](../../../sdn/technologies/network-controller/Network-Controller.md) |

