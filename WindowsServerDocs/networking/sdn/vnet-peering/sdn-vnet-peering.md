---
title: Virtuelles Netzwerk peering
description: ''
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: 58596387d79f3f212a472f00c2785bacc278e855
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821911"
---
# <a name="virtual-network-peering"></a>Virtuelles Netzwerk peering

>Gilt für: Windows Server

Peering in virtuellen Netzwerken können Sie die nahtlose Verbindung von zwei virtuellen Netzwerken. Nach für verbindungszwecke, dem Peering werden die virtuellen Netzwerke als eine angezeigt. 

Die Verwendung von vnet-peering bietet folgende Vorteile:

-   Datenverkehr zwischen virtuellen Computern in mittels Peering verknüpften virtuellen Netzwerke über das Backbone-Infrastruktur über weitergeleitet *private* IP-Adressen nur. Die Kommunikation zwischen den virtuellen Netzwerken ist nicht öffentliche Internet oder Gateways erforderlich.

-   Eine niedrige Latenz und hoher Bandbreite der Verbindung zwischen Ressourcen in verschiedenen virtuellen Netzwerken.

-   Die Fähigkeit für Ressourcen in einem virtuellen Netzwerk mit Ressourcen in einem anderen virtuellen Netzwerk kommunizieren.

-   Keine Ausfallzeiten auf Ressourcen in beiden virtuellen Netzwerken, die beim Erstellen des peerings.

## <a name="requirements-and-constraints"></a>Anforderungen und Einschränkungen

Vnet-peering verfügt über einige Anforderungen und Einschränkungen:

-   Mittels Peering verknüpften virtuellen Netzwerke müssen Schritte ausführen:

    -   IP-Adressräume ohne überschneidungen verfügen

    -   Durch den gleichen Netzwerkcontroller verwaltet werden

-   Nachdem Sie ein virtuelles Netzwerk mit einem anderen virtuellen Netzwerk per Peering verknüpfen, können nicht Sie hinzufügen oder löschen in den Adressraum-Adressbereiche.

   >[!TIP]
   >Wenn Sie die Adressbereiche hinzufügen möchten:<ol><li>Das peering zu entfernen.</li><li>Fügen Sie den Adressraum hinzu.</li><li>Fügen Sie das peering wieder hinzu.</li></ol>

-   Da die vnet-peering zwischen zwei virtuellen Netzwerken ist, besteht es keine abgeleitete transitive Beziehung zwischen Peerings. Z. B. Wenn Sie ein VirtualNetworkA mit VirtualNetworkB und VirtualNetworkB mit virtualnetworkc verknüpft Peering, klicken Sie dann VirtualNetworkA nicht mit virtualnetworkc verknüpft Peering zu erhalten.

    [Hier Image]

## <a name="connectivity"></a>Verbindung

Nach dem Peering virtueller Netzwerke können Ressourcen in beiden virtuellen Netzwerken direkt mit Ressourcen im mittels Peering verknüpften virtuellen Netzwerk verbinden.

-   Die Netzwerklatenz zwischen virtuellen Computern in mittels Peering verknüpften virtuellen Netzwerken ist identisch mit der Netzwerklatenz in einem einzelnen virtuellen Netzwerk.

-   Netzwerkdurchsatz basiert auf der Bandbreite für den virtuellen Computer zulässig. Es ist keine zusätzliche Einschränkung auf die Bandbreite im peering ein.

-   Datenverkehr zwischen virtuellen Computern in mittels Peering verknüpften virtuellen Netzwerken wird direkt über das Backbone-Infrastruktur nicht über ein Gateway oder über das öffentliche Internet weitergeleitet.

-   Virtuelle Computer in einem virtuellen Netzwerk können über den internen Lastenausgleich im mittels Peering verknüpften virtuellen Netzwerk zugreifen.

Sie können die Zugriffssteuerungslisten (ACLs) in beiden virtuellen Netzwerken den Zugriff auf andere virtuelle Netzwerke oder Subnetze zu blockieren, bei Bedarf anwenden. Wenn Sie Öffnen der vollständigen Konnektivität zwischen den mittels Peering verknüpften virtuellen Netzwerken (die Standardoption), können Sie die ACLs auf bestimmten Subnetzen oder virtuellen Computern zu blockieren oder zu verweigern den Zugriff jeweils spezifisch anwenden. Weitere Informationen zu ACLs finden Sie unter [verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Datencenter-Netzwerk fließt der Datenverkehr](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow).

## <a name="service-chaining"></a>Dienstverkettung

Sie können benutzerdefinierte Routen konfigurieren, die auf virtuellen Computern in mittels Peering verknüpften virtuellen Netzwerken, als der nächste Hop IP-Adresse verweisen, um die dienstverkettung zu aktivieren. Dienstverkettung können Sie leiten Sie Datenverkehr von einem virtuellen Netzwerk an ein virtuelles Gerät, in einem mittels Peering verknüpften virtuellen Netzwerk, über benutzerdefinierte Routen.

Sie können die Hub-Spoke-Netzwerke bereitstellen, in dem das virtuelle hubnetzwerk Infrastrukturkomponenten wie etwa ein virtuelles Netzwerkgerät gehostet werden können. Alle virtuellen Spoke-Netzwerke mittels Peering mit dem virtuellen hubnetzwerk. Datenverkehr kann virtuelle Netzwerkgeräte in das virtuelle hubnetzwerk durchlaufen.

Vnet-peering ermöglicht den nächsten Hop in einer benutzerdefinierten Route, die IP-Adresse eines virtuellen Computers im mittels Peering verknüpften virtuellen Netzwerk. Weitere Informationen zu benutzerdefinierten Routen finden Sie unter [verwenden virtueller Netzwerkgeräte in einem virtuellen Netzwerk](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-network-virtual-appliances-on-a-vn).

## <a name="gateways-and-on-premises-connectivity"></a>Gateways und lokale Konnektivität

Jedes virtuelles Netzwerk kann unabhängig davon, ob ein Peering mit einem anderen virtuellen Netzwerk eingerichtet haben immer noch ein eigenes Gateway eine Verbindung mit einem lokalen Netzwerk herstellen. Beim Peering virtueller Netzwerke können Sie auch das Gateway im mittels Peering verknüpften virtuellen Netzwerk als transitpunkt zu einem lokalen Netzwerk konfigurieren. In diesem Fall kann nicht das virtuelle Netzwerk, das ein Remotegateway verwendet ein eigenes Gateway verfügen. Ein virtuelles Netzwerk haben nur ein Gateway, das entweder als ein Gateway für lokales oder remote (im mittels Peering verknüpften virtuellen Netzwerk).

## <a name="monitor"></a>Überwachen

Wenn Sie sich mit zwei virtuelle Netzwerken per Peering verknüpfen, müssen Sie konfigurieren, ein peering für jedes virtuelle Netzwerk im peering.

Sie können den Status Ihrer Peeringverbindung, überwachen, die in einem der folgenden Status möglich:

-   **Initiiert:** Angezeigt, wenn Sie das peering vom ersten virtuellen Netzwerk mit dem zweiten virtuellen Netzwerk erstellen.

-   **Verbunden:** Angezeigt, nachdem Sie das peering vom zweiten virtuellen Netzwerk mit dem ersten virtuellen Netzwerk erstellt haben. Der peeringstatus für das erste virtuelle Netzwerk wird nun aus initiiert verbunden. Beide Peers des virtuellen Netzwerks müssen den Status der verbunden haben, vor dem Einrichten einer vnet-Peering erfolgreich.

-   **Getrennt:** Angezeigt, wenn ein anderes virtuelles Netzwerk ein virtuelles Netzwerk trennt.

[INFOGRAFIK der Zustände]

## <a name="next-steps"></a>Nächste Schritte
[Konfigurieren Sie das peering in virtuellen Netzwerken](sdn-configure-vnet-peering.md): In diesem Verfahren Sie Windows PowerShell verwenden, um den HNV finden Anbieter logischen Netzwerk zwei virtuelle Netzwerke erstellen, jeweils mit einem Subnetz. Außerdem konfigurieren Sie das peering zwischen den beiden virtuellen Netzwerken.

