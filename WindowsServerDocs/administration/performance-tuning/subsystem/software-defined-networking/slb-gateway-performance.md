---
title: Leistungsoptimierung des SLB-Gateways in Software definierten Netzwerken
description: Leitfaden zur Leistungsoptimierung für SLB-Gateways in Sdn-Netzwerken
ms.topic: article
ms.author: grcusanz; anpaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 64d045a270b8762d0d269055c8c65d1e40a71d63
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895932"
---
# <a name="slb-gateway-performance-tuning-in-software-defined-networks"></a>Leistungsoptimierung des SLB-Gateways in Software definierten Netzwerken

Der Software Lastenausgleich wird durch eine Kombination aus einem Load Balancer Manager in den virtuellen Netzwerk Controller Computern, dem virtuellen Hyper-V-Switch und einer Reihe von Load Balancer virtuellen Computern mit mehreren xplexor-VMS (MUX) bereitgestellt.

Es ist keine zusätzliche Leistungsoptimierung erforderlich, um den Netzwerk Controller oder den Hyper-V-Host für den Lastenausgleich zu konfigurieren, der über die im Abschnitt [Software Defined Networking](index.md) beschriebenen Komponenten hinausgeht, es sei denn, Sie verwenden SR-IOV für die muxes, wie unten beschrieben.

## <a name="slb-mux-vm-configuration"></a>SLB MUX-VM-Konfiguration

Virtuelle SLB MUX-Computer werden in einer aktiv/aktiv-Konfiguration bereitgestellt.  Dies bedeutet, dass jeder virtuelle MUX-Computer, der dem Netzwerk Controller bereitgestellt und hinzugefügt wird, eingehende Anforderungen verarbeiten kann.  Folglich wird der gesamte aggregierte Durchsatz aller Verbindungen nur durch die Anzahl der von Ihnen bereitgestellten MUX-VMS beschränkt.

Eine einzelne Verbindung mit einer virtuellen IP-Adresse (VIP) wird immer an dieselbe MUX-Adresse gesendet, wobei angenommen wird, dass die Anzahl der Mux konstant bleibt. Infolgedessen wird der Durchsatz auf den Durchsatz einer einzelnen MUX-VM beschränkt.  Muxes verarbeiten nur den eingehenden Datenverkehr, der an eine VIP-Adresse gerichtet ist.  Antwort Pakete gelangen direkt von der VM, die die Antwort an den physischen Switch sendet, der Sie an den Client weiterleitet.

In einigen Fällen, in denen die Quelle der Anforderung von einem Sdn-Host stammt, der demselben Netzwerk Controller hinzugefügt wird, der die VIP verwaltet, wird auch die weitere Optimierung des eingehenden Pfads für die Anforderung ausgeführt, sodass die meisten Pakete direkt vom Client zum Server übertragen werden können, wobei der Mux-VM vollständig umgangen wird.  Es ist keine zusätzliche Konfiguration erforderlich, damit diese Optimierung stattfindet.

Jeder SLB MUX-VM muss gemäß den Richtlinien, die im Abschnitt [Planen einer Software definierten Netzwerkinfrastruktur](../../../../networking/sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md) beschrieben werden, gemäß den Richtlinien für die Rollenanforderungen für virtuelle Computer in Sdn-Infrastruktur angegeben werden.

## <a name="single-root-io-virtualization-sr-iov"></a>Single-root-e/a-Virtualisierung (SR-IOV)

Bei Verwendung von 40Gbit Ethernet wird die Möglichkeit des virtuellen Switches zum Verarbeiten von Paketen für die MUX-VM zum einschränkenden Faktor für den MUX-VM-Durchsatz.  Aus diesem Grund wird empfohlen, SR-IOV auf dem VM-Netzwerk Adapter der SLB-VM zu aktivieren, um sicherzustellen, dass der virtuelle Switch nicht der Engpass ist.

Wenn Sie SR-IOV aktivieren möchten, müssen Sie es auf dem virtuellen Switch aktivieren, wenn der virtuelle Switch erstellt wird.  In diesem Beispiel erstellen wir einen virtuellen Switch mit Switch Embedded Team Vorgang (Set) und SR-IOV:
``` syntax
    new-vmswitch -Name SDNSwitch -EnableEmbeddedTeaming $true -NetAdapterName @("NIC1", "NIC2") -EnableIOV $true
```
Anschließend muss Sie auf den virtuellen Netzwerkadaptern der SLB MUX-VM aktiviert werden, die den Datenverkehr verarbeiten.  In diesem Beispiel wird SR-IOV auf allen Adaptern aktiviert:
``` syntax
    get-vmnetworkadapter -VMName SLBMUX1 | set-vmnetworkadapter -IovWeight 50
```
