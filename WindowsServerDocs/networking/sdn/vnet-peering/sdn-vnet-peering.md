---
title: Peering in virtuellen Netzwerken
manager: grcusanz
ms.topic: get-started-article
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/08/2018
ms.openlocfilehash: 21008268f14435852c7de78ce826bc380f9017a1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955817"
---
# <a name="virtual-network-peering"></a>Peering in virtuellen Netzwerken

>Gilt für: Windows Server

Das Peering virtueller Netzwerke ermöglicht das nahtlose Verbinden von zwei virtuellen Netzwerken. Nach dem Peer werden die virtuellen Netzwerke zu konnektivitätszwecken als eins angezeigt.

Die Verwendung von VNET-Peering bietet unter anderem folgende Vorteile:

-   Datenverkehr zwischen virtuellen Computern in den virtuellen Netzwerken mit virtuellen Netzwerken wird nur über die Backbone-Infrastruktur über *private* IP-Adressen geleitet. Die Kommunikation zwischen den virtuellen Netzwerken erfordert weder öffentliches Internet noch Gateways.

-   Niedrige Latenz, Verbindung mit hoher Bandbreite zwischen Ressourcen in unterschiedlichen virtuellen Netzwerken

-   Die Möglichkeit zur Kommunikation für Ressourcen in einem virtuellen Netzwerk mit Ressourcen in einem anderen virtuellen Netzwerk.

-   Keine Ausfallzeiten von Ressourcen in einem virtuellen Netzwerk beim Erstellen des Peerings.

## <a name="requirements-and-constraints"></a>Anforderungen und Einschränkungen

Beim Peering virtueller Netzwerke sind einige Anforderungen und Einschränkungen zu beachten:

- Virtuelle Netzwerke mit virtuellen Netzwerken müssen Folgendes ausführen:

  -   Nicht überlappende IP-Adressräume

  -   Verwaltung durch denselben Netzwerk Controller

- Wenn Sie ein virtuelles Netzwerk mit einem anderen virtuellen Netzwerk übertragen haben, können Sie Adressbereiche im Adressraum nicht hinzufügen oder löschen.

  >[!TIP]
  >Wenn Sie Adressbereiche hinzufügen müssen:<ol><li>Entfernen Sie das Peering.</li><li>Fügen Sie den Adressraum hinzu.</li><li>Fügen Sie das Peering erneut hinzu.</li></ol>

- Da das Peering virtueller Netzwerke zwischen zwei virtuellen Netzwerken besteht, besteht keine abgeleitete transitiv Beziehung zwischen Peerings. Wenn Sie z. b. virtualnetworka mit virtualnetworkb und virtualnetworkb mit virtualnetworkc verknüpfen, wird virtualnetworka nicht mit virtualnetworkc verknüpft.

## <a name="connectivity"></a>Konnektivität

Nachdem Sie virtuelle Netzwerke mittels Peering verbunden haben, können Ressourcen in beiden virtuellen Netzwerken direkt mit Ressourcen im mittels Peering verknüpften virtuellen Netzwerk verbunden werden.

-   Die Netzwerk Latenz zwischen virtuellen Computern in virtuellen Netzwerken mit virtuellen Netzwerken entspricht der Wartezeit innerhalb eines einzelnen virtuellen Netzwerks.

-   Der Netzwerk Durchsatz basiert auf der Bandbreite, die für den virtuellen Computer zulässig ist. Im Peering bestehen keine weiteren Bandbreiteneinschränkungen.

-   Der Datenverkehr zwischen virtuellen Computern in mittels PNS über ein virtuelles Netzwerk wird direkt über die Backbone-Infrastruktur und nicht über ein Gateway oder über das öffentliche Internet weitergeleitet.

-   Virtuelle Computer in einem virtuellen Netzwerk können auf den internen Load Balancer im per Peer-Board basierenden virtuellen Netzwerk zugreifen.

Sie können Zugriffs Steuerungs Listen (ACLs) in jedem virtuellen Netzwerk anwenden, um den Zugriff auf andere virtuelle Netzwerke oder Subnetze zu blockieren, wenn dies gewünscht wird. Wenn Sie die vollständige Konnektivität zwischen virtuellen Netzwerken mit virtuellen Netzwerken (Standardoption) öffnen, können Sie ACLs auf bestimmte Subnetze oder virtuelle Computer anwenden, um einen bestimmten Zugriff zu blockieren oder zu verweigern. Weitere Informationen zu ACLs finden Sie unter [Verwenden von Access Control Listen (ACLs) zum Verwalten des Netzwerk Datenverkehrs im Daten Center](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow).

## <a name="service-chaining"></a>Dienstverkettung

Sie können benutzerdefinierte Routen konfigurieren, die auf virtuelle Computer in per Peer fähigen virtuellen Netzwerken als IP-Adresse für den nächsten Hop verweisen, um die Dienst Verkettung zu aktivieren. Mithilfe der Dienst Verkettung können Sie den Datenverkehr von einem virtuellen Netzwerk über benutzerdefinierte Routen an ein virtuelles Gerät in einem mittels pvm gebundenen virtuellen Netzwerk weiterleiten.

Sie können Hub-und sprach Netzwerke bereitstellen, in denen das virtuelle Hub-Netzwerkinfrastruktur Komponenten (z. b. ein virtuelles Netzwerkgerät) hosten kann. Alle virtuellen Netzwerke, die sich mit dem virtuellen Hub-Netzwerk verbinden. Der Datenverkehr kann über virtuelle Netzwerkgeräte im virtuellen Hub-Netzwerk fließen.

Das Peering virtueller Netzwerke ermöglicht es dem nächsten Hop in einer benutzerdefinierten Route, die IP-Adresse eines virtuellen Computers im mittels Peering gebundenen virtuellen Netzwerk zu sein. Weitere Informationen zu benutzerdefinierten Routen finden Sie unter [Verwenden von virtuellen Netzwerkgeräten auf einem Virtual Network](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-network-virtual-appliances-on-a-vn).

## <a name="gateways-and-on-premises-connectivity"></a>Gateways und lokale Konnektivität

Jedes virtuelle Netzwerk kann unabhängig davon, ob es mit einem anderen virtuellen Netzwerk verbunden ist, weiterhin über ein eigenes Gateway verfügen, um eine Verbindung mit einem lokalen Netzwerk herzustellen. Beim Peering virtueller Netzwerke können Sie das Gateway im mittels Peering verknüpften virtuellen Netzwerk auch als Transitpunkt für ein lokales Netzwerk konfigurieren. In diesem Fall kann das virtuelle Netzwerk, das ein Remote Gateway verwendet, kein eigenes Gateway besitzen. Ein virtuelles Netzwerk kann nur über ein Gateway verfügen, bei dem es sich entweder um ein lokales Gateway oder um ein Remote Gateway (im virtuellen Netzwerk mit Peer) handeln kann.

## <a name="monitor"></a>Überwachen

Wenn Sie zwei virtuelle Netzwerke mittels Peering verknüpfen, müssen Sie für jedes virtuelle Netzwerk im Peering ein Peering konfigurieren.

Sie können den Status Ihrer Peeringverbindung überwachen, die sich in einem der folgenden Zustände befinden kann:

-   **Initiiert:** Wird angezeigt, wenn Sie das Peering vom ersten virtuellen Netzwerk mit dem zweiten virtuellen Netzwerk erstellen.

-   **Verbunden:** Wird angezeigt, nachdem Sie das Peering vom zweiten virtuellen Netzwerk mit dem ersten virtuellen Netzwerk erstellt haben. Der Peeringzustand für das erste virtuelle Netzwerk wechselt von Initiiert zu Verbunden. Beide Peers von virtuellen Netzwerken müssen den Status "verbunden" aufweisen, bevor das Peering virtueller Netzwerke erfolgreich hergestellt werden konnte.

-   **Getrennt:** Wird angezeigt, wenn ein virtuelles Netzwerk die Verbindung mit einem anderen virtuellen Netzwerk trennt.

[infographic der Zustände]

## <a name="next-steps"></a>Nächste Schritte
[Konfigurieren des Peerings virtueller](sdn-configure-vnet-peering.md)Netzwerke: in diesem Verfahren verwenden Sie Windows PowerShell, um das logische HNV-anbieternetzwerk zu suchen und zwei virtuelle Netzwerke mit jeweils einem Subnetz zu erstellen. Außerdem konfigurieren Sie das Peering zwischen den beiden virtuellen Netzwerken.

