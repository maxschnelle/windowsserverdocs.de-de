---
title: Leistungsoptimierung für Software-Defined Networking (SDN)
description: 'Software-Defined Networking (SDN): Richtlinien zur Leistungsoptimierung'
ms.topic: article
ms.author: grcusanz; anpaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 9c097d9b777676da1caef062e8aee4267d2e4dac
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895943"
---
# <a name="performance-tuning-software-defined-networks"></a>Leistungsoptimierung für Software-Defined Networking (SDN)

Software-Defined Networking (SDN) unter Windows Server 2016 besteht aus einer Kombination aus einem Netzwerkcontroller, Hyper-V-Hosts, Software Load Balancer-Gateways und HNV-Gateways.  Die folgenden Abschnitte enthalten Informationen zu den einzelnen Komponenten:

## <a name="network-controller"></a>Netzwerkcontroller

Der Netzwerkcontroller ist eine Windows Server-Rolle, die auf virtuellen Computern auf Hosts aktiviert sein muss, für die die SDN-Nutzung konfiguriert ist und die vom Netzwerkcontroller gesteuert werden.

Drei für Netzwerkcontroller geeignete VMs sind ausreichend, um Hochverfügbarkeit und die maximale Leistung zu erzielen.  Die Größe jeder VM muss gemäß den Richtlinien ausgelegt sein, die im Thema [Planen einer Software-Defined Networking-Infrastruktur](../../../../networking/sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md) im Abschnitt zu den Rollenanforderungen von virtuellen Computern der SDN-Infrastruktur beschrieben sind.

### <a name="sdn-quality-of-service-qos"></a>SDN-Dienstqualität

Um sicherzustellen, dass der VM-Datenverkehr effektiv und fair priorisiert wird, wird empfohlen, die SDN-Dienstqualität auf den virtuellen Workloadcomputern zu konfigurieren.  Weitere Informationen zum Konfigurieren der SDN-Dienstqualität finden Sie unter dem Thema [Konfigurieren der Dienstqualität für den Netzwerkadapter einer Mandanten-VM](../../../../networking/sdn/manage/Configure-QoS-for-Tenant-VM-Network-Adapter.md).

## <a name="hyper-v-host-networking"></a>Hyper-V-Hostnetzwerk

Die Anleitung im Abschnitt zur Hyper-V-Netzwerk-E/A-Leistung unter [Leistungsoptimierung für Hyper-V-Server](../../role/remote-desktop/session-hosts.md) gilt, wenn SDN verwendet wird. In diesem Abschnitt werden aber auch weitere Richtlinien beschrieben, die eingehalten werden müssen, um bei Verwendung von SDN die bestmögliche Leistung sicherzustellen.

### <a name="physical-network-adapter-nic-teaming"></a>NIC-Teamvorgang (Physischer Netzwerkadapter)

Um die beste Leistung zu erzielen und die besten Failoverfunktionen zu erhalten, wird empfohlen, für die physischen Netzwerkadapter den Teamvorgang zu konfigurieren.  Bei Verwendung von SDN müssen Sie das Team per Switch Embedded Teaming (SET) erstellen.

Die optimale Anzahl von Teammitgliedern ist 2, da der virtualisierte Datenverkehr für die ein- und ausgehende Richtung auf beide Teammitglieder verteilt wird.  Sie können auch mehr als zwei Teammitglieder verwenden. Der eingehende Datenverkehr wird aber auf maximal zwei Adapter verteilt.  Der Datenverkehr in ausgehender Richtung wird immer auf alle Adapter verteilt, wenn die Standardeinstellung für den dynamischen Lastenausgleich auf dem virtuellen Switch konfiguriert bleibt.


### <a name="encapsulation-offloads"></a>Abladevorgänge bei der Kapselung

Für SDN wird die Kapselung von Paketen zum Virtualisieren des Netzwerks verwendet.  Zur Erzielung der optimalen Leistung ist es wichtig, dass der Netzwerkadapter Hardwareabladungen für das verwendete Kapselungsformat unterstützt.  Keines der Kapselungsformate weist gegenüber den anderen Formaten einen signifikanten Leistungsvorteil auf.  Bei Verwendung des Netzwerkcontrollers lautet das Standardformat für die Kapselung „VXLAN“.

Sie können ermitteln, welches Kapselungsformat verwendet wird, indem Sie den Netzwerkcontroller mit dem folgenden PowerShell-Cmdlet nutzen:

``` syntax
    (Get-NetworkControllerVirtualNetworkConfiguration -connectionuri $uri).properties.networkvirtualizationprotocol
```

Die beste Leistung bei Rückgabe von VXLAN erzielen Sie, indem Sie sicherstellen, dass für Ihre physischen Netzwerkadapter VXLAN-Taskabladungen unterstützt werden.  Wenn NVGRE zurückgegeben wird, müssen Ihre physischen Netzwerkadapter die NVGRE-Taskabladung unterstützen.

### <a name="mtu"></a>MTU

Die Kapselung führt dazu, dass jedem Paket zusätzliche Byte hinzugefügt werden.  Um die Fragmentierung dieser Pakete zu vermeiden, muss das physische Netzwerk für die Verwendung von Großrahmen konfiguriert werden.  Ein MTU-Wert von 9234 ist die empfohlene Größe für VXLAN oder NVGRE und muss auf dem physischen Switch für die physischen Schnittstellen der Hostports (L2) und der Routerschnittstellen (L3) der VLANs konfiguriert werden, über die die gekapselten Pakete gesendet werden.  Dies schließt die Übertragungs-, HNV-Anbieter- und Verwaltungsnetzwerke ein.

Die maximale Übertragungseinheit (MTU) auf dem Hyper-V-Host wird über den Netzwerkadapter konfiguriert. Der Netzwerkcontroller-Host-Agent, der auf dem Hyper-V-Host ausgeführt wird, wird automatisch für den Mehraufwand der Kapselung angepasst, wenn dies vom Netzwerkadaptertreiber unterstützt wird.

Wenn Datenverkehr aus dem virtuellen Netzwerk über ein Gateway fließt, wird die Kapselung entfernt und die ursprüngliche MTU verwendet, die von der VM gesendet wird.

### <a name="single-root-io-virtualization-sr-iov"></a>E/A-Virtualisierung mit Einzelstamm (Single Root I/O Virtualization, SR-IOV)

SDN wird auf dem Hyper-V-Host implementiert, indem auf dem virtuellen Switch eine Switcherweiterung für die Weiterleitung verwendet wird.  Damit mit dieser Switcherweiterung Pakete verarbeitet werden können, darf SR-IOV nicht auf virtuellen Netzwerkschnittstellen verwendet werden, die für die Nutzung mit dem Netzwerkcontroller konfiguriert sind. Der Grund ist, dass VM-Datenverkehr hierbei am virtuellen Switch vorbeigeleitet wird.

Bei Bedarf kann SR-IOV trotzdem auf dem virtuellen Switch aktiviert und von VM-Netzwerkadaptern verwendet werden, die nicht vom Netzwerkcontroller gesteuert werden.  Diese SR-IOV-VMs können gleichzeitig auf demselben virtuellen Switch als VMs mit Steuerung durch den Netzwerkcontroller vorhanden sein, für die SR-IOV nicht genutzt wird.

Bei Verwendung von 40-GBit-Netzwerkadaptern wird empfohlen, SR-IOV auf dem virtuellen Switch für die SLB-Gateways (Software Load Balancing) zu aktivieren, um den maximalen Durchsatz zu erzielen.  Dies ist im Abschnitt zu den [Software Load Balancer-Gateways](slb-gateway-performance.md) ausführlicher beschrieben.

## <a name="hnv-gateways"></a>HNV-Gateways

Informationen zur Optimierung von HNV-Gateways für die Nutzung mit SDN finden Sie im Abschnitt [HVN-Gateways](hnv-gateway-performance.md).

## <a name="software-load-balancer-slb"></a>Softwarelastenausgleich (Software Load Balancer, SLB)

SLB-Gateways können nur mit dem Netzwerkcontroller und SDN genutzt werden.  Weitere Informationen zum Optimieren von SDN für die Nutzung mit SLB-Gateways finden Sie im Abschnitt zu [Software Load Balancer-Gateways](slb-gateway-performance.md).
